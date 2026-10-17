# Natural Upbringing 1.2 - Validation générale

> Ce document est la synthèse de validation avant implémentation finale et campagne de tests groupés.
> Il ne remplace pas `DEV_ROADMAP_1.2.md`.
> Statuts utilisés :
> - **VALIDÉ** : décision déjà approuvée.
> - **VALIDÉ** : valeur ou détail proposé pour la dernière relecture.
> - **À TESTER** : fonctionnement approuvé mais encore non validé en jeu.
> - **1.2.1** : volontairement reporté après la 1.2.

## 1. Périmètre de la 1.2

**VALIDÉ**

La 1.2 doit contenir :
- les réactions parentales aux assimilations ;
- les notifications de traits de personnalité acquis à l'étranger ;
- les 8 événements généraux d'éducation étrangère ;
- les 10 événements normaux liés aux 5 domaines d'éducation ;
- le mal du pays persistant ;
- l'arc rare de fugue ;
- la distinction Crozier entre Foi et Rite ;
- l'influence extrêmement légère de l'éducation étrangère sur l'acceptation culturelle ;
- la catégorie de Game Rules Natural Upbringing et les règles de portée ;
- les corrections liées à l'accompagnement des pupilles et aux notifications du tuteur.

**1.2.1**
- arcs rares à fort impact autres que la fugue ;
- seconde fugue possible après renvoi chez le tuteur ;
- découverte ultérieure d'un béguin secret ;
- extensions plus larges de changement culturel hors éducation.

## 2. Architecture générale des réactions

**VALIDÉ**

Les réactions parentales utilisent six familles :
1. Rejet / Colère
2. Inquiétude / Méfiance
3. Acceptation / Empathie
4. Réflexion / Retenue
5. Pragmatisme / Opportunisme
6. Détachement / Adaptation

Principes :
- une réaction dominante unique ;
- poids différents selon culture, foi ou rite ;
- les traits du joueur n'interdisent normalement pas une option logique ;
- agir à contre-caractère peut générer du stress ;
- les conséquences restent modestes et cohérentes avec vanilla ;
- aucun gain artificiel d'or, de prestige, de piété ou de statistique pour une simple réaction ;
- Insensible réduit ou supprime le stress lorsque cohérent ;
- Sadique peut durcir les conséquences relationnelles ;
- Courageux peut réduire l'inquiétude ;
- Zélé pèse très fortement sur la religion.

Pour un changement religieux :
- conversion de **Foi** : réaction plus forte ;
- changement de **Rite** : mêmes familles, mais intensité généralement réduite d'un niveau.

## 3. Foi et Rite, système Crozier

**VALIDÉ**

Ordre strict :
1. comparer la Foi ;
2. seulement si la Foi est identique, comparer le Rite.

Conséquences :
- Foi différente : exposition à la Foi uniquement ;
- même Foi mais Rite différent : exposition au Rite uniquement ;
- même Foi et même Rite : aucune exposition religieuse étrangère ;
- jamais d'exposition simultanée Foi + Rite pour un même environnement ;
- une conversion vers une Foi différente adopte forcément aussi un Rite de cette Foi, en priorité celui du tuteur ou de l'environnement éducatif ;
- ce changement de Rite est une conséquence de la conversion de Foi, pas une seconde assimilation.

Les événements qui ajoutent ou retirent de l'exposition religieuse suivent exactement la même hiérarchie.

L'accompagnement religieux protège Foi et Rite avec la même puissance actuelle, soit un multiplicateur d'exposition de **x0,4**.

La protection religieuse contractuelle bloque les deux assimilations.

### Chances d'assimilation

**VALIDÉ comme point de départ**

| Score d'exposition | Conversion de Foi | Changement de Rite |
| ---: | ---: | ---: |
| 5+ | 1 % | 2 % |
| 15+ | 2 % | 4 % |
| 30+ | 5 % | 8 % |
| 45+ | 10 % | 15 % |
| 60+ | 18 % | 25 % |
| 75+ | 28 % | 38 % |
| 90+ | 40 % | 55 % |

Modificateurs :

| Trait | Foi | Rite |
| --- | ---: | ---: |
| Zélé | x0,55 | x0,75 |
| Cynique | x1,35 | x1,20 |
| Obstiné | x0,80 | x0,90 |
| Inconstant | x1,20 | x1,15 |
| Confiant | x1,10 | x1,10 |
| Paranoïaque | x0,85 | x0,90 |

La vitesse normale d'exposition reste la même. C'est l'assimilation du Rite qui est plus facile, pas son accumulation.

## 4. Notifications des traits de personnalité

**VALIDÉ, À TESTER**

- écouter `on_trait_gained` sans override des scènes vanilla ;
- uniquement pour un enfant réellement élevé à l'étranger ;
- notification différée de 3 jours ;
- vérifier que le trait existe toujours après les éventuels remplacements vanilla ;
- 36 variantes FR/EN, une pour chaque trait vanilla ;
- fallback générique pour les traits ajoutés par des mods ;
- la scène décrit le comportement ayant révélé le trait, sans rejouer l'événement vanilla ;
- le parent réagit selon : même trait, opposition vanilla, puis familles générales ;
- la majorité des réactions sont RP, avec stress uniquement si émotionnellement cohérent.

## 5. Huit événements généraux

**VALIDÉ**

### Information affichée au joueur

**VALIDÉ**

- distinguer systématiquement ce qui relève de la narration visible de ce qui relève du moteur interne de NU ;
- les gains ou pertes d'exposition culturelle, de Foi ou de Rite existent mécaniquement mais ne sont pas affichés au joueur dans les options ou résultats lorsqu'ils représentent une évolution interne que le personnage ne peut pas quantifier ;
- même principe pour les points d'éducation, pondérations, jets cachés, seuils, progression interne et autres valeurs purement systémiques ;
- n'afficher directement que les conséquences que le personnage peut raisonnablement constater ou comprendre : relation créée ou détériorée, blessure, stress lorsqu'il est vécu par le personnage concerné, retour au foyer, changement effectif de culture/Foi/Rite, etc. ;
- les tooltips ne doivent pas transformer une scène RP en tableau de statistiques cachées ;
- ce principe s'applique également aux 10 événements de focus et, plus largement, à tous les événements NU de la 1.2.


### Des nouvelles de mon enfant
- Très intégré : +5 exposition culturelle, +20 opinion mutuelle enfant/tuteur pendant 5 ans.
- Sociable : +2 exposition culturelle, +10 opinion mutuelle pendant 5 ans.
- Réservé : -2 exposition culturelle.
- Difficile : -3 exposition culturelle, -5 opinion mutuelle pendant 5 ans, 1 % de tentative de fugue si éligible, sinon 10 % de mal du pays.
- Fallback : aucun effet.

### Une amitié inattendue
- crée l'amitié si valide ;
- Réservé : +1 exposition culturelle ;
- Sociable : +3 ;
- fallback : +2 ;
- 10 % de passage à meilleur ami ;
- 5 % de Béguin si attirance valide.

### L'étranger de la cour
- Repli : -6 exposition culturelle + stress mineur ;
- Défi : -3 exposition culturelle ;
- Adaptation : +2 ;
- fallback : -1.

**VALIDÉ**
- branche Défi : **10 %** de chance de créer une Rivalité avec l'enfant impliqué.

### Une coutume étrange
- Résistance : -2 culture et -2 exposition religieuse ;
- Curiosité avec Curieux : +2 culture et +2 exposition religieuse ;
- Cynique seul : neutre sur l'exposition ;
- Enthousiasme : +3 culture et +3 exposition religieuse ;
- fallback : neutre.

L'exposition religieuse est automatiquement dirigée vers Foi ou Rite selon la hiérarchie Crozier.

### Quelques mots familiers
- fonctionnement actuel conservé ;
- nécessite une exposition culturelle déjà sensible.

### Entre deux mondes
- fonctionnement actuel conservé ;
- exposition plus profonde ;
- une seule fois par enfance.

### Le Béguin
- orientation vanilla déjà définie ;
- âge compatible ;
- pas de proche parent ;
- cible de l'environnement étranger ;
- attraction compatible ;
- pour une relation homosexuelle, vérifier les doctrines des deux Rites ;
- si au moins un Rite réprouve ou criminalise, le Béguin existe mais reste secret au parent.

### Le Rival
Base :
- Rivalité inchangée : 60 ;
- Ami : 20 ;
- Némésis : 15 ;
- Béguin : 5 si attirance valide.

Rival -> Ami supprime Rival.
Rival -> Némésis remplace Rival.
Rival -> Béguin conserve Rival + Béguin.

Les pondérations de personnalité déjà définies dans la roadmap sont conservées.

## 6. Dix événements de focus

**VALIDÉ sur le fond**

Chaque événement dépend du focus actuel, de la personnalité, des aptitudes et du contexte de cour. Les points d'éducation sont typiquement :
- +2 : résultat formateur ;
- +1 : expérience utile ;
- 0 : échec ou scène sans bénéfice éducatif.

Aucun malus d'éducation direct pour un événement normal.

### Diplomatie
**Entre deux querelles**
- médiation réussie : +2 ;
- imparfaite : +1 ;
- aggravation : 0.

**VALIDÉ**
- progression relationnelle positive si cible persistante et valide : **10 %**.

**Un visage venu d'ailleurs**
- aisance sociale : +1 Diplomatie, +1 culture ;
- interaction instructive : +1 ;
- fermeture : 0.

**VALIDÉ**
- relation positive avec le visiteur : **7 %** si la cible peut rester pertinente.

### Martial
**Le terrain plutôt que les livres**
- réussite forte : +2 Martial ;
- normale : +1 ;
- mauvaise discipline : 0.

**VALIDÉ**
- +1 Prouesse sur réussite forte : **10 %** si progrès physique crédible ;
- +1 Prouesse sur branche normale : **3 %**.

**Un coup de trop**
- retenue : +1 ;
- confrontation assumée : +1 ;
- domination sadique : +1 possible, mais conséquences relationnelles plus dures.

**VALIDÉ**
- progression amicale après retenue : **10 %** ;
- Rivalité après confrontation : **10 %** ;
- Rivalité avec Sadique : **20 %** ;
- +1 Prouesse : **7 %** uniquement si la scène représente réellement un progrès physique.

### Intendance
**Quelque chose ne compte pas**
- trouve l'erreur : +2 ;
- intuition partielle : +1 ;
- accusation précipitée : 0.
- variantes de contexte : féodal/administratif/républicain, tribal, nomade.

**Faire durer les réserves**
- bonne gestion : +2 et +1 culture ;
- apprentissage : +1 et +1 culture ;
- mauvaise gestion : 0.

### Intrigue
**Ce n'était pas destiné à ses oreilles**
- conserve intelligemment l'information : +2 ;
- révèle au tuteur : +1 ;
- se fait prendre : 0.

**VALIDÉ**
- hook faible pour l'enfant en cas de véritable levier : **12 %** ;
- hook faible pour le tuteur si l'enfant lui révèle une information exploitable : **8 %** ;
- jamais de hook si la scène ne justifie pas réellement un levier.

**Je sais quelque chose que tu ignores**
- manipulation réussie : +2 ;
- manipulation subtile : +1 ;
- retour de bâton : 0.

**VALIDÉ**
- hook faible, réussite forte : **15 %** ;
- hook faible, réussite subtile : **8 %** ;
- Rivalité après manipulation ou retour de bâton : **10 %**.

### Érudition
**Deux enseignements, deux vérités**
- compréhension des deux : +2, +1 culture, +1 exposition religieuse si contradiction religieuse ;
- acceptation locale : +1 et +1 exposition pertinente ;
- rejet : +1 et -1 exposition étrangère.

**Pourquoi ?**
- questionnement fertile : +2 ;
- curiosité correcte : +1 ;
- contestation : +1 avec possible perte d'opinion du tuteur.

### Réactions parentales aux 10 événements
**VALIDÉ**
- mêmes six familles ;
- réactions plus légères que les grandes assimilations ;
- beaucoup de réponses purement RP ;
- stress ou opinion uniquement lorsque la scène le justifie ;
- aucune récompense automatique supplémentaire.

## 7. Mal du pays persistant

**VALIDÉ**

Le mal du pays devient un état réel et persistant.

- il est enregistré avec sa durée ;
- le parent est prévenu une seule fois par la demande de retour ;
- aucune nouvelle demande périodique n'est envoyée tant que le même état persiste ;
- un refus du parent conserve et renforce émotionnellement le mal du pays ;
- l'intégration culturelle ou religieuse ne le fait pas disparaître naturellement ;
- retour définitif au foyer, fin de la tutelle concernée ou âge adulte mettent fin à cet état ;
- si l'enfant rentre après une fugue puis est renvoyé chez son tuteur, le mal du pays est renforcé ;
- aucune seconde fugue en 1.2 ;
- l'actuel cooldown de demandes répétées tous les 3 ans devient obsolète.

La fugue est possible après **au moins 1 an de mal du pays actif**.

## 8. Arc de fugue

**VALIDÉ**

Prérequis :
- 12 ans minimum ;
- mal du pays actif depuis au moins 1 an ;
- focus d'éducation ;
- une seule fugue réelle maximum en 1.2.

Déclenchement spontané :
- base 5 % ;
- un seul jet spontané lorsque l'enfant devient éligible ;
- les événements contextuels peuvent avoir leurs propres chances très faibles.

### Personnalité

**VALIDÉ**

Proposition pour le jet spontané :
- Brave : x1,50 ;
- Obstiné : x1,35 ;
- Colérique : x1,25 ;
- Ambitieux : x1,20 ;
- Inconstant : x1,15 ;
- Lâche : x0,25 ;
- Timide : x0,70 ;
- Satisfait : x0,75 ;
- Confiant : x0,85 ;
- Calme : x0,90.

Les multiplicateurs peuvent se cumuler, avec une chance finale plafonnée à **12 %** et un minimum de **0,5 %**.

### Progression cachée mensuelle

| Niveau de compétence du focus | Échec | Neutre | Réussite |
| --- | ---: | ---: | ---: |
| Exécrable, 0-3 | 50 % | 35 % | 15 % |
| Mauvais, 4-6 | 35 % | 40 % | 25 % |
| Moyen, 7-9 | 25 % | 35 % | 40 % |
| Bon, 10-13 | 15 % | 30 % | 55 % |
| Excellent, 14+ | 8 % | 22 % | 70 % |

Score initial : 0.
Réussite : +1.
Échec : -1.
Neutre : 0.
Le niveau est recalculé chaque mois.

+4 : réussite critique et retour anticipé.
-4 : échec critique avec sous-jet de gravité.

### Sous-jet d'échec critique

| Focus | Sain et sauf | Aggravé | Sévère | Mort |
| --- | ---: | ---: | ---: | ---: |
| Diplomatie | 80 % | 18 % | 2 % | 0 % |
| Martial | 55 % | 30 % | 12 % | 3 % |
| Intendance | 70 % | 25 % | 4 % | 1 % |
| Intrigue | 75 % | 21 % | 3 % | 1 % |
| Érudition | 65 % | 27 % | 6 % | 2 % |

Résolution normale après 5 à 9 mois :
- +3 : retour réussi ;
- +2 : retour réussi avec aide sur la fin ;
- +1 : presque arrivé, puis aidé/escorté au foyer ;
- 0 : retrouvé et ramené au tuteur ;
- -1 : retrouvé en difficulté et ramené au tuteur ;
- -2 : échec sérieux avec conséquence mineure possible ;
- -3 : échec sévère adapté au focus, puis retour au tuteur.

La tutelle reste active pendant l'arc sauf résolution qui ramène réellement l'enfant au foyer.

Certaines branches spécifiques peuvent déroger au retour chez le tuteur, par exemple une prise en otage avec rançon puis récupération directe par la famille.

La mort utilise les conséquences vanilla de deuil et de stress. NU fournit surtout le contexte narratif et ne double pas artificiellement ces pénalités.

### Retour réussi

**VALIDÉ**

Proposition :
- parent accepte que l'enfant reste : +20 opinion de l'enfant envers le parent, fin de la tutelle étrangère, fin du mal du pays ;
- parent le renvoie chez le tuteur : -25 opinion, stress moyen pour l'enfant, mal du pays renforcé, tutelle maintenue ;
- traits du parent modulent surtout le stress et la formulation ;
- aucune seconde fugue en 1.2.

Prestige :
- retour réussi normal : gain mineur ;
- +4 critique : gain moyen ;
- échec : perte mineure ;
- mort : aucun malus de prestige supplémentaire.

### Story Cycle

**VALIDÉ**
- visible dans l'onglet Situations ;
- affiche l'enfant, le temps écoulé, le focus, l'état qualitatif et la dernière information ;
- n'affiche jamais le score caché brut ;
- se termine à la résolution de la fugue.

## 9. Acceptation culturelle

**VALIDÉ**

- +0,01 par année complète et par enfant réellement élevé dans une autre culture ;
- plafond +0,10 par an pour une même paire de cultures ;
- cesse si l'enfant adopte la culture locale ;
- cesse s'il quitte la cour ou n'est plus réellement élevé à l'étranger ;
- mécanique toujours active ;
- Game Rule dédiée uniquement à sa portée.

Portées :
- suivre la portée générale de NU, défaut ;
- famille proche ;
- cour du joueur ;
- royaume du souverain ;
- royaume + royaumes voisins ;
- monde entier.

## 10. Game Rules

**VALIDÉ**

Créer la catégorie vanilla **Natural Upbringing**.

Y placer au minimum :
- Portée de la simulation ;
- Portée de l'acceptation culturelle.

Les systèmes centraux d'éducation ne deviennent pas des toggles individuels.

## 11. Accompagnement et notifications

**VALIDÉ, À TESTER**

- l'interaction d'accompagnement d'une tutelle existante est limitée aux enfants réellement pertinents, notamment famille proche, et ne doit plus apparaître sur des otages étrangers sans lien ;
- serviteurs culturels : protection culturelle ;
- instruction de qualité : système existant conservé ;
- accompagnement religieux : même protection contre Foi et Rite ;
- tuteur joueur informé légèrement lorsqu'un pupille assimile culture, Foi ou Rite ;
- pas de notification en double si le tuteur est aussi le parent ;
- si plusieurs assimilations surviennent ensemble sous le même tuteur, message combiné lorsque possible ;
- tuteurs IA : pas de traitement RP inutile.

## 12. Cadence des nouvelles

**VALIDÉ**

- événements généraux : 25 % par anniversaire éligible ;
- cooldown commun : 2 ans ;
- les lettres de nouveaux traits restent indépendantes ;
- pas d'événement général le même anniversaire qu'une assimilation NU ou qu'une demande active liée au mal du pays.

## 13. Compatibilité et philosophie

**VALIDÉ**

- priorité à l'intégration invisible dans CK3 vanilla ;
- pas de système parallèle inutile quand vanilla fournit déjà une conséquence correcte ;
- support des aventuriers autant que le permettent les mécaniques vanilla ;
- ajout à une sauvegarde CK3 1.20 déjà commencée doit rester possible ;
- pas de reconstruction rétroactive des années d'exposition antérieures à l'installation de NU ;
- fichiers texte NU en UTF-8 avec BOM ;
- descriptor à passer à la version CK3 publiée au moment de la release, après tests.

## 14. Campagne de tests groupés

**À FAIRE APRÈS VALIDATION DE CE DOCUMENT**

Un gros test doit couvrir ensemble :
1. culture, Foi et Rite, y compris même Foi + Rite différent et Foi différente ;
2. accompagnement religieux et protection contractuelle ;
3. assimilation et réactions parentales ;
4. notifications du tuteur et absence de doublons ;
5. acquisition de traits et 36 lettres ;
6. les 8 événements généraux ;
7. les 10 événements de focus et leurs effets spéciaux ;
8. mal du pays persistant, demande unique et absence de nouvelle demande ;
9. fugue, progression, Story Cycle, succès, échec, retour et branches sévères ;
10. acceptation culturelle et Game Rule de portée ;
11. scopes IA/joueur et cas multijoueur pertinents ;
12. absence de régression sur la tutelle vanilla.

## 15. Derniers réglages validés

Les valeurs suivantes sont validées comme base de la 1.2 et pourront uniquement être rééquilibrées si les tests groupés montrent un problème manifeste :
- 10 % de Rivalité dans « L'étranger de la cour » branche Défi ;
- 10 % / 7 % de progression relationnelle dans les événements Diplomatie ;
- probabilités de +1 Prouesse dans les événements Martial ;
- probabilités de hooks faibles et Rivalités dans les événements Intrigue ;
- multiplicateurs de personnalité et plafond 12 % pour la fugue ;
- +20 / -25 d'opinion et stress moyen lors du choix du parent après un retour réussi.

L'ensemble de ce document est désormais validé pour l'implémentation de la 1.2.

## 16. Prévu pour la 1.2.1

- **Events RARES**
- **Story Cycle Complet**
