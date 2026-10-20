# Natural Upbringing 1.2 - Retours techniques CODE / LOGIQUE

> Document de retour d'expérience sur les problèmes rencontrés pendant le développement et les playtests de la 1.2.
>
> Objectif : conserver les symptômes, causes, mauvaises pistes et solutions afin d'éviter de reproduire les mêmes erreurs dans Natural Upbringing ou d'autres mods CK3.

## 1. Règle générale : toujours vérifier le ROOT réel

### Symptôme

Plusieurs outils debug semblaient fonctionner dans l'interface mais n'appliquaient aucun effet réel :

- "Forcer une année d'exposition" s'ouvrait mais le score ne progressait pas.
- "Forcer une fugue" était cliquable mais ne lançait pas l'arc.
- Certains calculs dépendant du tuteur ou de la cour ne retrouvaient pas leurs scopes.

### Cause

Les scripted effects concernés avaient été conçus avec l'hypothèse suivante :

```
ROOT = enfant
```

Or, dans une character interaction :

```
ROOT = actor
scope:recipient = enfant
```

Exécuter directement un effet child-root depuis l'interaction produisait donc des triggers et recherches de relations sur le mauvais personnage.

### Mauvaise piste

Ajouter toujours plus de conditions dans `is_valid_showing_failures_only` rendait le bouton disponible, mais ne corrigeait pas le contexte d'exécution.

### Solution

Passer par un événement caché déclenché sur le recipient :

```
scope:recipient = {
    trigger_event = nu_debug.XXXX
}
```

L'enfant devient alors réellement ROOT avant d'exécuter l'effet.

### Leçon

Avant de corriger un trigger CK3, vérifier d'abord :

1. quel personnage est ROOT ;
2. où se trouve actor ;
3. où se trouve recipient ;
4. si les saved scopes existent encore au moment où l'effet est exécuté.

Un bouton cliquable ne prouve pas que l'effet s'exécute dans le bon scope.

---

## 2. Scopes temporaires perdus entre deux pipelines

### Symptôme

Le debug d'assimilation religieuse pouvait connaître la Foi cible mais ne retrouvait pas correctement le Rite du tuteur.

### Cause

Le scope temporaire `nu_guardian` créé pendant le calcul annuel d'exposition n'existe plus lorsqu'un outil debug séparé force ensuite une assimilation.

Les temporary scopes ne doivent pas être traités comme un état persistant.

### Solution

Reconstruire le contexte depuis des données persistantes :

- relation guardian actuelle ;
- court owner actuel ;
- Foi cible enregistrée ;
- fallback vers le main Rite de la Foi uniquement pour le debug si le contexte original n'est plus disponible.

### Leçon

Un `save_temporary_scope_as` sert à un pipeline local. Pour une action différée ou indépendante, reconstruire le scope ou enregistrer explicitement une variable persistante.

---

## 3. Variables locales de réaction parentale mal lues

### Symptôme

Les réactions parentales d'assimilation donnaient des résultats incohérents ou tombaient sur le mauvais profil malgré des traits parentaux valides.

### Cause

Le système de sélection alimentait des variables locales suffixées comme :

```
nu_cultural_reaction_reaction
nu_religious_reaction_reaction
```

mais une partie de la sélection lisait encore d'anciens noms :

```
nu_cultural_reaction
nu_religious_reaction
```

Le calcul des scores fonctionnait, mais le résultat lu ensuite n'était pas celui réellement écrit.

### Solution

Aligner tous les lecteurs sur les variables effectivement produites par le système de réaction.

### Leçon

Lorsqu'un système en plusieurs étapes fonctionne partiellement, inspecter les noms de variables entre :

1. préparation ;
2. comparaison ;
3. sélection ;
4. affichage.

Un bug de nom peut donner l'impression que toute la logique de pondération est mauvaise alors que seul le transfert du résultat est cassé.

---

## 4. Réactions parentales trop négatives à cause des égalités

### Symptôme

Un parent Juste + Diligent + Colérique produisait trop régulièrement une réaction négative, donnant l'impression d'un système biaisé.

### Cause

La première famille initialisée était Rejet. En cas d'égalité parfaite, les familles suivantes ne remplaçaient le résultat que si leur score était strictement supérieur.

Le système n'était donc pas aléatoirement biaisé, mais les égalités favorisaient mécaniquement la première famille.

### Solution

- Ajouter Diligent à la famille Réflexion.
- Revoir les poids pour mieux représenter les traits mixtes.
- Ne pas transformer chaque nouvelle éducative ordinaire en gain de stress passif.

### Leçon

Avec un système de "winner takes all", définir explicitement une politique d'égalité. L'ordre des comparaisons est lui-même une règle de gameplay.

---

## 5. Les nouvelles ordinaires devenaient un moteur de stress passif

### Symptôme

Les événements d'éducation provoquaient trop régulièrement du stress chez le parent, même pour des nouvelles mineures.

### Cause

Les familles Réjection, Méfiance et Acceptation avaient chacune un effet générique de stress en plus des conséquences propres aux événements.

Sur une campagne longue, l'accumulation devenait disproportionnée.

### Solution

Supprimer le stress générique des réactions aux nouvelles ordinaires.

Le stress reste réservé aux situations qui le justifient réellement :

- trait identique ou opposé ;
- choix narratif important ;
- fugue ;
- événement explicitement stressant.

### Leçon

Un effet cohérent pris isolément peut devenir mauvais lorsqu'il est appliqué par un système fréquent. Toujours tester la cadence réelle, pas seulement l'événement unitaire.

---

## 6. Valeurs de stress affichées différentes des valeurs codées

### Symptôme

Une perte codée à `-30` donnait par exemple `-15` en jeu, et un gain de `+30` pouvait donner `+38`.

### Cause

CK3 applique ensuite ses multiplicateurs vanilla de gain et de perte de stress :

- traits ;
- perks ;
- modificateurs ;
- autres effets du personnage.

### Solution

Conserver `-30 / +30` comme valeurs de base et accepter que le résultat final affiché varie.

### Leçon

Ne pas confondre valeur d'effet de base et résultat final après modificateurs vanilla. Avant de "corriger" une différence numérique, vérifier les multiplicateurs natifs.

---

## 7. Acceptation culturelle : mauvaise unité

### Symptôme

Le design initial utilisait :

```
+0.01 par enfant et par an
cap +0.10
```

En jeu, l'effet était presque imperceptible.

### Cause

`change_cultural_acceptance` travaille directement en points d'acceptation, pas dans une échelle 0 à 1.

`0.01` représentait donc 0,01 point, pas 1 %.

### Solution

Passage à :

```
+1 point par enfant et par année complète
cap +10 points par paire de cultures et par an
```

### Leçon

Ne jamais déduire l'unité d'une valeur CK3 depuis son nom. Vérifier le comportement vanilla ou tester directement l'effet.

---

## 8. "Recent Changes" n'est pas une source fiable pour compter l'acceptation

### Symptôme

Pendant un test avec plusieurs enfants, seuls quelques changements récents étaient visibles dans l'UI culturelle, ce qui pouvait laisser penser que certaines contributions n'étaient pas appliquées.

### Cause

L'interface "Recent Changes" est limitée dans ce qu'elle affiche et n'est pas le registre complet des contributions internes.

### Solution

Le plafond +10 est suivi par le système NU lui-même. Ne pas utiliser la liste visuelle vanilla comme compteur de vérité.

### Leçon

Une UI vanilla peut être une vue partielle d'un état. Pour tester une mécanique cumulative, instrumenter le système ou vérifier la valeur finale plutôt que compter les lignes affichées.

---

## 9. Assimilations simultanées suspectes avec plusieurs pupilles

### Symptôme

Deux enfants se sont assimilés culturellement presque au même moment après seulement une ou deux années, malgré des probabilités individuelles très faibles.

### Hypothèse initiale

Possible conflit de scopes, état partagé entre enfants ou double roll.

### Audit

- un seul roll naturel par anniversaire et par enfant ;
- variables d'exposition stockées sur chaque enfant ;
- aucun état d'assimilation partagé entre pupilles ;
- plusieurs enfants historiques testés avaient exactement le même anniversaire vanilla, notamment le 1er janvier.

### Conclusion

Aucun bug démontré. Événement considéré comme un coup de chance rare tant qu'il ne se reproduit pas anormalement.

### Leçon

Avant de rééquilibrer une probabilité après un résultat improbable :

1. vérifier le nombre réel de rolls ;
2. vérifier si les rolls sont synchronisés par une date commune ;
3. vérifier l'indépendance des variables ;
4. attendre une reproduction.

Ne pas modifier la balance pour masquer un bug qui n'existe peut-être pas.

---

## 10. Mal du pays actif bloqué par la Game Rule de portée

### Symptôme

Le mal du pays pouvait apparaître, mais sa durée active ne progressait plus dans certains cas.

### Cause

La progression était attachée au pipeline anniversaire général de NU, lui-même filtré par `nu_is_in_simulation_scope_trigger`.

Un état persistant déjà créé pouvait donc cesser de vieillir simplement parce que le personnage sortait du scope sélectionné.

### Solution

Créer un on_action anniversaire dédié :

```
nu_on_active_homesickness_birthday
```

Il avance un mal du pays déjà actif indépendamment de la Game Rule.

Le pipeline général évite ensuite le double incrément pour les enfants encore inclus dans le scope normal.

### Leçon

Une Game Rule de portée peut contrôler la création d'un état, mais ne doit pas nécessairement interrompre la progression d'un état persistant déjà existant.

Séparer :

- éligibilité initiale ;
- progression ;
- nettoyage.

---

## 11. Confusion entre durée et sévérité du mal du pays

### Symptôme

Pendant le test, la "sévérité" semblait ne pas progresser chaque année.

### Cause

Ce n'était pas un bug de logique.

Le design final distingue :

- durée : augmente avec le temps ;
- sévérité : augmente uniquement lorsque la situation empire, par exemple refus du retour ou renvoi chez le tuteur après une fugue.

### Solution

Clarifier le debug inspector pour expliquer ce comportement.

### Leçon

Les outils debug doivent exposer non seulement une valeur, mais aussi son sens. Une valeur qui ne bouge pas peut être correcte si sa règle de progression n'est pas temporelle.

---

## 12. Foi et Rite : ne pas utiliser un seul concept religieux

### Problème de logique

L'ajout des Rites dans Crozier rendait l'ancien modèle religieux insuffisant.

Deux cas doivent être strictement séparés :

1. Foi différente : exposition à la Foi uniquement.
2. Même Foi mais Rite différent : exposition au Rite uniquement.

L'enfant ne doit jamais accumuler les deux expositions pour le même environnement.

### Risque rencontré

Les anciennes variables de 1.1 stockaient la cible religieuse comme une Foi. En 1.2, une partie du système utilise un Rite lorsque la Foi est identique.

Réutiliser silencieusement l'ancien état aurait produit des comparaisons de scopes incompatibles.

### Solution

- Foi prioritaire sur Rite.
- Variables distinctes pour l'exposition à une Foi étrangère et au Rite.
- Migration de compatibilité : supprimer l'ancien `nu_faith_exposure_target` lorsqu'il est rencontré et reconstruire proprement l'exposition moderne.

### Leçon

Quand une mise à jour vanilla subdivise un concept ancien en plusieurs objets de données, ne pas seulement ajouter des conditions. Revoir aussi le type réel stocké dans les variables persistantes et prévoir la migration des sauvegardes.

---

## 13. Conversion de Foi et Rite : éviter la double assimilation

### Problème de logique

Lorsqu'un enfant adopte une Foi étrangère, CK3 doit aussi lui attribuer un Rite appartenant à cette Foi.

Si NU continuait ensuite à résoudre son exposition au Rite comme une seconde assimilation, le même changement religieux pouvait être traité deux fois.

### Solution

Lors d'une assimilation de Foi :

- choisir le Rite cohérent avec le tuteur ou la cour lorsque possible ;
- utiliser la conversion vanilla vers ce Rite ;
- nettoyer immédiatement l'exposition au Rite précédente ;
- ne jamais lancer une seconde assimilation de Rite pour le même changement.

### Leçon

Quand une action de haut niveau implique déjà une action de bas niveau, nettoyer l'état dérivé au même endroit.

---

## 14. Événements en format lettre avec mauvais point de vue

### Symptôme

Plusieurs événements affichaient des formulations absurdes :

- le tuteur parlait de lui-même à la troisième personne ;
- une lettre disait "my child" alors que l'expéditeur était le tuteur ;
- le contexte visuel laissait croire que l'expéditeur était celui qui pensait le texte alors que le texte venait du parent.

### Cause

Le type `letter_event` impose un expéditeur narratif fort. Certains textes avaient pourtant été écrits depuis le point de vue du parent.

### Solution

Pour les nouvelles parentales concernées :

- passer en `character_event` ;
- utiliser les portraits de l'enfant et du tuteur ;
- réserver `letter_event` aux textes réellement écrits par l'expéditeur.

Cela a notamment été appliqué aux notifications de traits et à plusieurs nouvelles d'éducation.

### Leçon

Le type d'event fait partie de la narration. Avant d'écrire le texte, décider explicitement : qui parle, qui pense et qui reçoit.

---

## 15. Échec de fugue affiché comme lettre alors que le texte était parental

### Symptôme

Une résolution négative de fugue affichait une lettre du tuteur alors que le texte disait en substance "mon enfant".

### Cause

Même erreur de perspective : `letter_event` ne correspondait pas au narrateur réel.

### Solution

Convertir la résolution en événement parental classique avec enfant et tuteur visibles.

### Leçon

Une cohérence mécanique correcte ne suffit pas. Les scopes narratifs doivent correspondre aux scopes techniques.

---

## 16. Localisations multi-lignes écrites directement sur plusieurs lignes

### Symptôme

Certaines localisations pouvaient être mal interprétées ou fragiles, notamment dans les descriptions longues et le Story Cycle.

### Cause

Des retours à la ligne réels étaient placés dans les valeurs YAML au lieu d'utiliser les séquences CK3 prévues.

### Solution

Remplacer les retours physiques par :

```
\n
\n\n
```

dans les chaînes de localisation.

### Leçon

Dans les fichiers `.yml` CK3, conserver chaque valeur de localisation sur une ligne et encoder les retours avec `\n`.

---

## 17. Story Cycle : scope dynamique absent dans la description courte

### Symptôme

Le Story Cycle de fugue affichait une description du type :

```
disappeared from the guardian's court...
```

avec le nom de l'enfant manquant au début.

### Cause

Le scope stocké dans `Story.MakeScope.Var(...)` n'était pas fiable dans ce contexte précis de description courte.

### Solution

Utiliser une formulation statique relative au propriétaire du Story :

```
Votre enfant a disparu de la cour de son tuteur...
```

Les informations détaillées continuent à utiliser les scopes du Story là où ils sont correctement résolus.

### Leçon

Un scope qui fonctionne dans le panneau détaillé d'un Story Cycle n'est pas garanti dans tous ses champs de localisation.

Tester séparément :

- titre ;
- description courte ;
- practical information ;
- custom loc.

---

## 18. Custom localization exécutée avec un ROOT différent de l'event

### Symptôme

Le dénouement de fugue affichait :

```
ERROR:[nu_runaway_child.GetFirstName]
```

dans le résumé dépendant du focus.

### Cause

`NU_RunawayJourneySummary` est une customizable localization de type `character`.

Dans ce custom loc, ROOT est déjà le personnage sur lequel la custom loc est appelée, donc les saved scopes de l'événement parent ne sont pas nécessairement disponibles.

### Solution

Utiliser :

```
[ROOT.Char.GetFirstName]
```

dans les clés appelées par la customizable localization.

### Leçon

Une custom loc possède son propre contexte. Ne pas supposer qu'elle hérite du scope de l'événement appelant.

---

## 19. Notification d'assimilation du tuteur joueur réutilisait l'event parental

### Symptôme

En switchant sur le tuteur joueur, celui-ci recevait exactement le même gros événement RP que le parent.

### Cause

Les événements d'assimilation complets ne vérifiaient pas eux-mêmes que ROOT était réellement parent de l'enfant.

Le pipeline normal les appelait correctement, mais un autre contexte pouvait les ouvrir avec un destinataire incorrect.

### Solution

Ajouter sur chacun des événements parentaux complets un trigger explicite :

```
scope:nu_assimilated_child = {
    is_child_of = root
}
```

Le tuteur joueur distinct reçoit uniquement la notification légère dédiée.

### Leçon

Un event important doit défendre ses propres invariants. Ne pas compter uniquement sur le code appelant pour garantir que ROOT est du bon type.

---

## 20. Retour de fugue : série de corrections symptomatiques avant la vraie cause

### Symptôme initial

Après une fugue réussie et le choix "reste à la maison" :

- la tutelle se terminait ;
- l'enfant était physiquement proche du parent ;
- mais il restait parfois dans la cour du tuteur, ou devenait sans cour et devait être invité manuellement.

### Tentative 1 : `move_to_pool_at = root.location`

Résultat :

- bonne position apparente ;
- mauvais état de cour.

### Tentative 2 : `set_employer = parent`

Résultat :

- changement partiel d'appartenance ;
- position et statut encore incohérents.

### Tentative 3 : `set_employer + return_to_court`

Résultat :

- l'enfant pouvait être considéré comme appartenant à la cour du parent tout en restant physiquement à l'ancienne cour.

### Tentative 4 : `add_courtier = enfant`

Résultat :

- toujours incorrect.

### Preuve décisive dans error.log

CK3 a signalé que `add_courtier` essayait d'ajouter l'enfant à la cour du parent alors qu'il y était **déjà**.

Donc le rattachement à la cour n'était pas le problème.

### Cause racine

L'effet exécuté ensuite était :

```
move_to_pool_at = ...
```

Or cet effet signifie précisément placer le personnage dans le pool à une localisation donnée.

Il faisait donc sortir l'enfant de sa cour juste après son retour correct.

Cela expliquait exactement le symptôme final :

- physiquement dans le comté du parent ;
- personnage sans cour ;
- bouton "Inviter à la cour" disponible.

### Solution finale

Après suppression de la tutelle :

```
return_to_court = yes
```

pour laisser vanilla nettoyer l'état de pupille / invité étranger, puis :

```
set_location_to_default = yes
```

pour restaurer la localisation normale sans éjecter le personnage dans le pool.

Aucun `set_employer`, `add_courtier` ou `move_to_pool_at` n'est nécessaire.

### Leçon majeure

Après plusieurs corrections successives d'un même bug, arrêter de modifier les symptômes et inspecter :

1. le log ;
2. le sens exact des effets vanilla ;
3. l'état du personnage avant ET après chaque effet.

`move_to_pool_at` ressemble à un simple déplacement géographique, mais il modifie aussi l'état de cour du personnage.

---

## 21. Tooltip violet de `set_location_to_default`

### Symptôme

Après correction du retour, le tooltip du choix affichait :

```
BUG: missing localization 'set_location_to_default_global'
```

en violet.

### Cause

L'effet fonctionnait correctement, mais il était placé directement dans l'option visible.

CK3 essayait donc de générer automatiquement un tooltip pour cet effet interne, sans localisation globale correspondante.

### Solution

Exécuter l'effet dans :

```
hidden_effect = {
    set_location_to_default = yes
}
```

### Leçon

Un "missing localization" dans un tooltip d'effet ne signifie pas nécessairement que la mécanique est cassée.

Si l'effet est purement technique, le cacher plutôt que créer artificiellement une localisation joueur.

---

## 22. Majorité pendant une fugue et cleanup d'adulte

### Problème de logique

Un enfant pouvait atteindre l'âge adulte pendant une fugue. Le cleanup standard de la tutelle risquait alors de supprimer des états sans résoudre proprement le Story Cycle.

### Solution

Ajouter une résolution spécifique avant le cleanup générique :

- détecter `nu_runaway_active` au passage à l'âge adulte ;
- fermer l'arc ;
- supprimer mal du pays et état de fugue ;
- terminer la tutelle ;
- ne pas forcer le personnage adulte à retourner chez l'ancien tuteur ;
- afficher un événement dédié au parent.

### Leçon

Les cleanups génériques ne doivent pas effacer silencieusement un arc narratif actif. Résoudre d'abord l'état spécial, nettoyer ensuite.

---

## 23. Trait identique / opposé : événement différé nécessaire

### Problème

Une notification envoyée immédiatement sur `on_trait_gained` peut annoncer un trait qui sera remplacé quelques instants plus tard par un autre système vanilla.

### Solution

- écouter `on_trait_gained` ;
- attendre 3 jours ;
- vérifier que le trait existe toujours ;
- seulement ensuite envoyer la notification au parent.

### Leçon

Un on_action signale qu'un changement vient de se produire, pas forcément qu'il est définitivement stabilisé.

Pour les systèmes vanilla susceptibles d'enchaîner plusieurs modifications, utiliser un léger délai puis revalider l'état.

---

## 24. Warnings de variables "inutilisées" mais volontairement conservées

### Warnings observés

Le log peut signaler notamment :

```
nu_homesickness_cooldown
nu_faith_exposure_target
```

comme lus ou supprimés sans création actuelle correspondante.

### Cause

Ce sont des reliquats volontairement gérés pour la compatibilité :

- `nu_homesickness_cooldown` : ancien état 1.1 / early 1.2 ;
- `nu_faith_exposure_target` : ancienne représentation de l'exposition religieuse avant séparation Foi / Rite.

### Décision

Les conserver dans les cleanups / migrations.

### Leçon

Un warning statique n'est pas automatiquement du dead code. Lorsqu'un mod doit rester compatible avec des sauvegardes précédentes, certains lecteurs ou `remove_variable` peuvent être intentionnellement orphelins du côté écriture.

Documenter ces exceptions pour qu'un futur nettoyage ne les supprime pas par erreur.

---

## 25. Problèmes observés mais attribués à vanilla ou non reproduits comme bugs NU

### 25.1 Lettre d'arrivée `char_interaction.0084`

Symptôme observé :

```
frugaleERROR:[second.Custom('FR_E')]
```

dans la lettre vanilla d'arrivée d'un pupille.

Conclusion : problème vanilla, ne pas override globalement l'événement pour le masquer dans NU.

### 25.2 Blessure de fugue soignée immédiatement

Une enfant a reçu une blessure correcte après un mauvais dénouement, puis le trait a disparu presque immédiatement.

Cause plausible : médecin de cour / traitement vanilla.

Conclusion : l'effet NU a bien été appliqué, ne pas forcer artificiellement la durée du trait.

### 25.3 Assimilation simultanée de plusieurs enfants

Aucun double roll ni état partagé trouvé.

Conclusion : surveiller sur le long terme avant de modifier la logique.

### 25.4 Protection religieuse contractuelle

Contexte de test trop pénible à reproduire proprement.

Conclusion : laisser la validation finale aux parties naturelles et retours joueurs plutôt que créer une simulation artificielle qui pourrait tester un contexte non représentatif.

---

# Checklist de diagnostic CK3 issue de la 1.2

Lorsqu'un système ne fonctionne pas, suivre cet ordre avant de modifier le code :

1. **ROOT / actor / recipient**
   - Qui est réellement ROOT à cet instant ?
   - L'effet appelé suppose-t-il un autre ROOT ?

2. **Scopes**
   - Temporary scope encore vivant ?
   - Saved scope persistant ?
   - Variable scope stockée sur le bon personnage ?

3. **État avant effet**
   - Relation guardian présente ?
   - Court / host / liege actuels ?
   - Personnage déjà dans la cour cible ?

4. **Sémantique exacte de l'effet vanilla**
   - Un effet "move" change-t-il seulement la position ?
   - Un effet de court change-t-il également host / liege / pool ?
   - Existe-t-il un pipeline vanilla déjà prévu pour ce cas ?

5. **Logs**
   - Lire `error.log` avant la quatrième tentative.
   - Une erreur peut prouver que l'état est déjà correct avant notre propre effet.

6. **UI vs état réel**
   - Tooltip, Recent Changes et portraits ne sont pas nécessairement des représentations complètes de l'état interne.

7. **Valeurs**
   - Vérifier l'unité.
   - Vérifier les multiplicateurs vanilla.
   - Vérifier le nombre réel de rolls.

8. **Narration**
   - Qui parle ?
   - Qui reçoit ?
   - Le type `letter_event` / `character_event` correspond-il au point de vue ?

9. **Compatibilité**
   - Une variable apparemment inutilisée sert-elle à nettoyer une ancienne sauvegarde ?
   - Un nouveau type de scope vanilla remplace-t-il l'ancien ?

10. **Après trois tentatives infructueuses**
    - arrêter les rustines ;
    - rechercher la cause racine ;
    - comparer avec le code vanilla ;
    - instrumenter ou lire le log avant toute nouvelle modification.

---

# Résultat final de la passe 1.2

La passe pré-release a confirmé :

- 48 events sans ID dupliqué ;
- 561 clés de localisation anglaises et 561 françaises sans doublon ;
- accolades équilibrées ;
- fichiers CK3 contrôlés en UTF-8 avec BOM ;
- retour de fugue validé sans expulsion de cour ;
- smoke test sans debug validé.

Ce document doit être enrichi si un problème déjà considéré comme aléatoire ou contextuel se reproduit en partie longue.
