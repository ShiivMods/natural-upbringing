# Natural Upbringing - feuille de route interne 1.2

> Document de travail. Il sert à conserver les décisions validées pendant le développement et à préparer le changelog final.
> Ne pas considérer les points "à trancher" comme des fonctionnalités promises.

## Décisions validées

### Réactions aux assimilations culturelles et religieuses

- Le système actuel avec une option indépendante pour chacun des traits de personnalité vanilla doit être simplifié.
- Les traits doivent être regroupés en grandes familles de réactions RP plutôt que de forcer chaque trait à produire systématiquement un choix.
- Les six familles retenues à ce stade sont :
  - Rejet / Colère
  - Inquiétude / Méfiance
  - Acceptation / Empathie
  - Réflexion / Retenue
  - Pragmatisme / Opportunisme
  - Détachement / Adaptation
- Culture et religion ne doivent pas attribuer exactement la même importance aux mêmes traits.
- Certains traits peuvent avoir un rôle spécial ou contextuel, plutôt que d'appartenir rigidement à une seule famille.
- Exemple important : Zélé doit avoir un poids très fort pour une assimilation religieuse, mais beaucoup moins pour une assimilation culturelle.
- D'autres traits comme Sadique, Insensible, Généreux ou Courageux peuvent demander un traitement particulier selon le contexte.
- Les traits peu pertinents pour une question identitaire ne doivent pas être artificiellement utilisés uniquement pour couvrir les 36 traits vanilla.
- Une seule réaction dominante doit être retenue pour l'événement, à partir de l'ensemble des traits pertinents du parent.
- Le calcul reste simple et additif : chaque trait pertinent renforce une famille, sans coder de combinaisons de traits spécifiques.
- Les poids peuvent différer entre assimilation culturelle et religieuse.
- En cas d'égalité, le départage doit être contextuel plutôt qu'aléatoire pur.
- Certains traits secondaires modifient surtout l'expression ou les conséquences de la réaction sans nécessairement choisir la famille dominante :
  - Insensible : réduit la composante de stress et rend les réactions hostiles plus froides.
  - Sadique : peut durcir les conséquences envers l'enfant lors d'une réaction négative.
  - Courageux : peut atténuer la peur / le stress sans modifier à lui seul la position idéologique.
- Luxurieux, Chaste, Glouton et Diligent restent hors du calcul principal tant qu'aucun rôle RP convaincant n'est défini.

### Philosophie des événements d'éducation à l'étranger

- Les nouveaux événements d'éducation NU concernent en priorité les enfants élevés à l'étranger.
- Le parent joueur n'assiste généralement pas directement aux scènes d'éducation.
- L'information lui parvient surtout par lettre, messager, rapport du tuteur, témoignage indirect ou rumeur.
- Contrairement à un enfant élevé dans sa propre cour, le parent ne doit généralement pas pouvoir choisir comment la scène éducative se déroule.
- Les choix du parent doivent donc surtout représenter une réaction, une réponse à une lettre ou une décision logistique/politique lorsque cela est réellement crédible.
- Les événements doivent être résolus principalement par la personnalité, les compétences, le focus d'éducation et l'environnement de l'enfant et du tuteur.
- Des exceptions sont possibles lorsque le parent peut raisonnablement intervenir à distance, mais elles doivent rester rares et justifiées.
- Les propositions concrètes d'événements par domaine ne sont pas encore validées.

### Cohérence du contexte de la cour étrangère

- Les événements d'éducation à l'étranger doivent rester cohérents avec la cour dans laquelle vit réellement l'enfant.
- Toutes les scènes n'ont pas besoin de dépendre du gouvernement : les événements universels restent disponibles partout.
- Les événements dont le contenu suppose une organisation politique, économique ou sociale particulière doivent en revanche être filtrés ou disposer de variantes adaptées.
- Le type de gouvernement de la cour d'accueil constitue un des principaux critères de contexte.
- Les flags vanilla stables peuvent être utilisés, notamment :
  - `government_is_tribal`
  - `government_is_nomadic`
  - `government_is_feudal`
  - `government_is_clan`
  - `government_is_administrative`
  - `government_is_republic`
  - ainsi que les gouvernements particuliers lorsque cela devient pertinent.
- Éviter de dupliquer ces contrôles dans chaque événement : créer des scripted triggers NU réutilisables pour les grandes catégories de contexte.
- Exemple :
  - un événement de dispute, de lettre ou d'amitié peut être universel ;
  - un événement d'Intendance portant sur des registres, une administration fiscale ou une économie urbaine doit exiger un contexte compatible ;
  - une variante tribale peut parler de réserves, tributs, butin, troupeaux ou redistribution ;
  - une variante nomade peut parler de troupeaux, provisions, campement, routes saisonnières ou partage des ressources.
- Le contexte peut à terme inclure d'autres critères lorsque réellement utiles : rang de la cour, culture, rite, région, richesse, présence d'une cour royale ou d'institutions particulières.
- Ne pas multiplier les conditions pour le simple réalisme : les utiliser uniquement lorsqu'elles empêchent une incohérence visible ou améliorent réellement la narration.

### Notifications des traits acquis à l'étranger

- Lorsqu'un enfant réellement élevé à l'étranger acquiert un trait de personnalité pendant son éducation, son parent joueur doit en être informé.
- Cette notification fait partie du cœur des événements d'éducation NU : elle permet au parent de suivre concrètement l'évolution de l'enfant malgré son absence.
- La nouvelle est présentée comme une lettre, un rapport du tuteur ou un témoignage venu de la cour étrangère.
- Le parent ne rejoue pas la scène et ne choisit pas à la place de l'enfant comment le trait se forme.
- L'implémentation doit s'appuyer autant que possible sur `on_trait_gained` afin d'éviter d'override les nombreux événements de personnalité vanilla et de rester compatible avec les futurs événements Paradox.
- `on_trait_gained` indique le personnage et le trait obtenu, mais pas nécessairement l'événement précis qui l'a causé. NU utilisera donc un événement de nouvelles associé au trait obtenu plutôt qu'une copie de la scène vanilla.
- La notification doit être légèrement différée et vérifier que le trait est toujours présent, car le système vanilla permet parfois au tuteur de remplacer le trait immédiatement après son acquisition.
- À terme, les textes doivent pouvoir varier selon le trait et, lorsque le contexte disponible le permet, selon le tuteur, la culture, le rite ou l'environnement de la cour étrangère.

### État d'implémentation des notifications de personnalité

- [À tester en jeu] `on_trait_gained` est maintenant écouté par NU sans override des événements vanilla.
- [À tester en jeu] Seuls les traits appartenant à la catégorie `personality` sont concernés.
- [À tester en jeu] La notification ne concerne que les enfants réellement élevés à l'étranger auprès de leur tuteur et ayant au moins un parent joueur vivant.
- [À tester en jeu] Le trait obtenu est conservé dans le contexte d'un événement différé de trois jours.
- [À tester en jeu] Après ces trois jours, NU vérifie que l'enfant possède toujours ce trait afin de laisser les systèmes vanilla de remplacement de trait se résoudre avant la notification.
- [À tester en jeu] Si le trait est toujours présent, chaque parent joueur reçoit une lettre du tuteur indiquant le trait final acquis.
- La notification est purement informative et n'ajoute aucun effet mécanique supplémentaire.
- Un scripted trigger réutilisable, `nu_is_genuinely_educated_abroad_trigger`, centralise désormais la définition d'un enfant réellement élevé à l'étranger.
- [À tester en jeu] Les 36 traits de personnalité vanilla disposent désormais chacun d'une variante de lettre dédiée en français et en anglais.
- Un fallback générique reste prévu pour les traits de personnalité ajoutés par un autre mod ou une future version du jeu.
- [À enrichir ultérieurement si utile] Certaines variantes pourront encore tenir compte du contexte précis de la cour sans modifier le moteur du système.

### Philosophie des événements rares

- Les événements rares ne sont pas de simples événements normaux avec une probabilité plus faible.
- Ils doivent avoir un potentiel d'impact important sur la suite de la partie : succession, alliances, rivalités, guerre, loyauté, identité culturelle/religieuse, relation avec le tuteur ou le seigneur étranger, etc.
- Leur rareté repose à la fois sur :
  - une faible probabilité ;
  - plusieurs prérequis précis et cohérents ;
  - un contexte narratif déjà construit par l'éducation de l'enfant.
- Exemple de structure validée :
  - enfant non premier-né ;
  - éducation martiale ;
  - bonne Diplomatie ;
  - Ambitieux ;
  - possibilité rare de commencer à lever des soutiens pour revendiquer le titre de son parent.
- Variante possible :
  - enfant non premier-né ;
  - éducation martiale ;
  - assimilation culturelle et/ou religieuse étrangère ;
  - soutien potentiel du seigneur ou de la cour où l'enfant a été élevé pour revendiquer le titre familial.
- Ces événements peuvent devenir des arcs en plusieurs étapes et laisser des conséquences longtemps après la fin de l'éducation.
- Leur conception est repoussée après les événements normaux afin de ne pas diluer le développement du système de base.

### Premier lot d'événements généraux validé

Les événements généraux racontent ce qui arrive à un enfant élevé à l'étranger. Le parent apprend généralement les faits après coup par lettre, messager, rapport ou rumeur. Il ne choisit pas à la place de l'enfant ce qui s'est produit.

Premier lot retenu pour la 1.2 :
- **Des nouvelles de mon enfant** : rapport général du tuteur sur l'adaptation après un certain temps à l'étranger. Variantes possibles : heureux, réservé, turbulent, nostalgique, très intégré.
- **Une amitié inattendue** : l'enfant se rapproche d'un autre enfant de la cour étrangère. Amitié sincère, fréquentation douteuse ou ancienne rivalité devenue complicité.
- **L'étranger de la cour** : l'enfant est confronté à des moqueries ou remarques sur son accent, ses coutumes ou ses habitudes. Sa personnalité détermine s'il se défend, ignore, tente de s'intégrer ou s'isole.
- **Une coutume étrange** : première participation notable à une tradition locale. Enthousiasme, curiosité, incompréhension ou rejet peuvent légèrement influencer l'exposition culturelle.
- **Quelques mots familiers** : une lettre de l'enfant laisse apparaître des expressions, références ou tournures propres à sa nouvelle cour. Sert notamment à rendre l'assimilation progressive visible avant un changement complet.
- **Deux mondes** : l'enfant mélange les habitudes de sa famille d'origine et celles de son environnement actuel. L'événement doit pouvoir représenter enrichissement, confusion ou véritable identité hybride sans forcer une assimilation.

Principes mécaniques :
- plusieurs de ces événements peuvent être entièrement narratifs ;
- éviter les récompenses automatiques de compétence ;
- effets éventuels légers : stress, opinion, exposition, relation ou points d'éducation ;
- les traits, l'âge, le tuteur et l'environnement de l'enfant déterminent principalement ce qui s'est produit ;
- un événement peut être rapporté par le tuteur, directement par l'enfant ou par un tiers pour varier le point de vue.


### Cadrage validé du pack initial d'événements généraux

Le pack initial doit comporter 8 événements généraux. Les effets d'exposition utilisent les systèmes NU existants afin de respecter les seuils, cibles et règles de suivi déjà en place. Pour la religion, les gains/pertes concernent l'exposition au rite.

#### 1. Des nouvelles de mon enfant

- Très intégré :
  - +5 exposition culturelle ;
  - +20 opinion mutuelle enfant / tuteur pendant 5 ans.
- Sociable :
  - +2 exposition culturelle ;
  - +10 opinion mutuelle enfant / tuteur pendant 5 ans.
- Réservé :
  - -2 exposition culturelle.
- Difficile :
  - -3 exposition culturelle ;
  - -5 opinion mutuelle enfant / tuteur pendant 5 ans ;
  - 1 % de chance de déclencher l'arc de fugue si tous ses prérequis sont remplis ;
  - si la fugue ne se déclenche pas, 10 % de chance de déclencher le mal du pays.
- Fallback :
  - aucun effet supplémentaire.

Ordre validé pour la variante Difficile : tester d'abord la fugue si elle est possible, puis seulement le mal du pays si aucune fugue n'a été déclenchée.

#### 2. Une amitié inattendue

- La relation d'amitié est créée comme actuellement.
- Réservé : +1 exposition culturelle.
- Sociable : +3 exposition culturelle.
- Fallback : +2 exposition culturelle.
- Après création de l'amitié :
  - 10 % de chance que l'amitié devienne une relation de meilleur ami si la relation est valide ;
  - 5 % de chance qu'un béguin naisse si les prérequis d'attirance sont remplis.
- Meilleur ami et béguin peuvent coexister si les règles CK3 le permettent.
- Un béguin reste une relation unilatérale, conformément au fonctionnement vanilla.

#### 3. L'étranger de la cour

- Repli :
  - -6 exposition culturelle ;
  - conserver le stress mineur déjà prévu.
- Défi :
  - -3 exposition culturelle ;
  - chance de créer une rivalité avec un enfant de la cour impliqué dans les moqueries.
- Adaptation :
  - +2 exposition culturelle.
- Fallback :
  - -1 exposition culturelle.

#### 4. Une coutume étrange

- Résistance :
  - -2 exposition culturelle ;
  - -2 exposition religieuse au rite.
- Curiosité :
  - si l'enfant est Curieux : +2 exposition culturelle et +2 exposition religieuse ;
  - si la variante provient uniquement du trait Cynique : aucun gain d'exposition supplémentaire.
- Enthousiasme :
  - +3 exposition culturelle ;
  - +3 exposition religieuse.
- Fallback :
  - neutre.

#### 5. Quelques mots familiers

- Fonctionnement actuel validé.

#### 6. Entre deux mondes

- Fonctionnement actuel validé.

#### 7. Le béguin

- Événement général dédié aux béguins formés dans la cour étrangère.
- Peut aussi être atteint depuis d'autres événements, notamment Une amitié inattendue et Le Rival.
- Prérequis :
  - orientation sexuelle déjà définie par vanilla ;
  - cible d'âge compatible ;
  - cible non proche parente ;
  - cible présente dans l'environnement étranger ;
  - sexe de la cible compatible avec l'orientation de l'enfant.
- Pour une attirance entre enfants du même sexe :
  - vérifier la position religieuse des deux rites vis-à-vis de l'homosexualité ;
  - si les deux rites l'acceptent, le béguin peut être rapporté normalement ;
  - si au moins un rite la réprouve ou la criminalise, la relation de béguin existe mais reste secrète pour le parent.
- Un béguin secret pourra être exploité plus tard par un événement distinct de découverte.
- Le texte doit pouvoir varier selon l'origine du béguin : nouvelle attirance, ami devenu béguin, rival devenu béguin.

#### 8. Le Rival

- Ne peut se déclencher que si l'enfant possède déjà un rival pertinent dans sa cour étrangère.
- L'événement raconte une nouvelle confrontation et peut faire évoluer la relation.
- Issues possibles :
  - rivalité inchangée ;
  - réconciliation et transformation en amitié ;
  - escalade et transformation en némésis ;
  - transformation en béguin si les règles d'attirance sont remplies.
- Les chances doivent être pondérées par la personnalité de l'enfant :
  - Indulgent, Compatissant, Sociable, Confiant, traits similaires : favorisent la réconciliation ;
  - Vengeur, Colérique, Sadique, Obstiné, traits similaires : favorisent la némésis ;
  - le béguin dépend principalement de l'attirance et de la compatibilité sexuelle.
- Les pourcentages exacts restent à cadrer avant implémentation.


### Pondération validée de l'événement « Le Rival »

Base de tirage :
- rivalité inchangée : poids 60 ;
- transformation en amitié : poids 20 ;
- transformation en némésis : poids 15 ;
- transformation en béguin : poids 5, uniquement si les conditions d'attirance sont remplies.

Modificateurs de personnalité :
- Amitié :
  - Indulgent ×3 ;
  - Compatissant, Sociable, Confiant ×2 ;
  - Calme, Patient ×1,5 ;
  - Vengeur ou Sadique ×0,25 ;
  - Colérique ou Obstiné ×0,5.
- Némésis :
  - Vengeur ×3 ;
  - Colérique ou Sadique ×2 ;
  - Obstiné ou Paranoïaque ×1,5 ;
  - Indulgent ou Compatissant ×0,25 ;
  - Calme ×0,5.
- Béguin :
  - uniquement si les règles d'attirance sont remplies ;
  - Luxurieux ×2 ;
  - Inconstant ×1,5 ;
  - l'orientation sexuelle reste le facteur déterminant principal.
- Rivalité inchangée reste le résultat dominant lorsqu'aucun trait ne pousse fortement vers une évolution.

### Réaction du parent aux traits acquis par l'enfant

Ordre de résolution validé :
1. si le parent possède le même trait que celui acquis par l'enfant, utiliser une réaction de reconnaissance généralement favorable ;
2. si le parent possède un trait opposé vanilla au nouveau trait de l'enfant, utiliser une réaction plus forte de désaccord, inquiétude ou incompréhension ;
3. sinon, utiliser les six familles de personnalité déjà définies pour déterminer la tonalité de la réponse.

Principes :
- ne pas écrire une matrice exhaustive de 36 × 36 réactions ;
- exploiter les oppositions vanilla et les familles existantes pour conserver un système maintenable ;
- les réponses restent centrées sur le parent et ne modifient pas rétroactivement ce qui est arrivé à l'enfant ;
- la majorité des réponses peuvent rester purement RP ;
- seuls les cas émotionnellement cohérents produisent un effet mécanique.

Niveaux mécaniques retenus :
- forte satisfaction / reconnaissance : petite perte de stress ;
- réaction neutre ou analytique : aucun effet ;
- inquiétude / désapprobation : petit gain de stress ;
- opposition forte : gain de stress moyen.

Aucun gain d'or, prestige, piété ou statistique ne doit être attaché à ces réactions.

Les oppositions directes s'appuient sur les oppositions vanilla, notamment :
- Luxurieux / Chaste ;
- Glouton / Tempérant ;
- Cupide / Généreux ;
- Paresseux / Diligent ;
- Colérique / Calme ;
- Patient / Impatient ;
- Arrogant / Humble ;
- Fourbe / Honnête ;
- Lâche / Brave ;
- Timide / Sociable ;
- Ambitieux / Satisfait ;
- Arbitraire / Juste ;
- Cynique / Zélé ;
- Paranoïaque / Confiant ;
- Compatissant / Insensible / Sadique ;
- Obstiné / Inconstant / Excentrique ;
- Vengeur / Indulgent.

Les noms FR des traits sont toujours récupérés depuis la localisation vanilla CK3.


### Réponses du parent aux nouvelles d'éducation

- Les réponses du parent ne doivent pas modifier rétroactivement ce qui est arrivé à l'enfant.
- Elles reflètent le caractère du parent et peuvent avoir des effets sur le parent lui-même.
- Réutiliser les six grandes familles déjà définies pour les réactions d'assimilation :
  - Rejet / Colère ;
  - Inquiétude / Méfiance ;
  - Acceptation / Empathie ;
  - Réflexion / Retenue ;
  - Pragmatisme / Opportunisme ;
  - Détachement / Adaptation.
- La famille doit au minimum adapter la formulation de la réponse.
- Les effets mécaniques, notamment gain ou perte de stress, ne sont ajoutés que lorsqu'ils sont narrativement justifiés.
- Éviter de transformer chaque petite nouvelle en source automatique de stress ou de récompense.

### Lettres lors de l'acquisition d'un trait de personnalité

- Le système de notification différée reste validé.
- Le texte actuel du trait Chaste doit être réécrit afin de supprimer la formulation « au contraire », qui suppose à tort une continuité avec une lettre précédente.
- Nouvelle philosophie validée pour les 36 traits :
  - ne plus se contenter d'un constat psychologique générique ;
  - raconter un petit incident concret survenu à la cour étrangère ;
  - montrer comment l'enfant a réagi ;
  - conclure par le trait acquis.
- Structure cible :
  1. incident concret ;
  2. comportement de l'enfant ;
  3. constat du tuteur ;
  4. trait acquis.
- Les réponses du parent doivent également pouvoir varier selon sa propre personnalité.
- Pour les lettres de traits, aller au-delà des seules six familles lorsque pertinent : tenir compte de la compatibilité ou opposition spécifique entre les traits du parent et le nouveau trait de l'enfant.
- Les 36 scènes narratives ont été revues et validées comme base de travail avant implémentation.
- Chaque lettre doit raconter un incident concret révélant progressivement le trait, puis conclure par le trait acquis.
- Les noms de traits affichés en français doivent reprendre strictement la localisation vanilla CK3, sans traduction manuelle. Exemple vérifié : `brave` = « Brave » en français.
- Le texte du trait Chaste est validé dans sa nouvelle version sans la formulation « au contraire ».
- Les textes pourront encore recevoir de petites corrections de style ou d'accord lors de l'intégration FR/EN, sans changer leur scène ni leur intention.


### Menu debug des événements éducatifs

- [À tester en jeu] Une interaction debug sur un enfant élevé à l'étranger ouvre un menu de test des événements éducatifs.
- Le menu permet soit de lancer aléatoirement l'un des événements généraux, soit de choisir directement parmi les six événements.
- Les scopes nécessaires sont reconstruits automatiquement : enfant, tuteur, cour étrangère, culture locale et camarade de cour lorsque disponible.
- L'événement « Une amitié inattendue » n'est proposé que si un enfant compatible existe dans la cour et crée réellement la relation d'amitié afin de reproduire le comportement naturel.
- Ce menu est réservé au mode debug et ne modifie pas le fonctionnement normal du mod.

### État d'implémentation des nouvelles d'éducation à l'étranger

- [À tester en jeu] Premier lot de six événements généraux implémenté.
- [À tester en jeu] Déclenchement uniquement pour un enfant de 6 à 15 ans ayant un focus d'éducation, vivant réellement dans une cour différente de sa cour d'origine et auprès de son tuteur.
- [À tester en jeu] Les événements sont envoyés uniquement aux parents joueurs sous forme de lettres ou nouvelles ; les actions de l'enfant sont résolues avant réception.
- [À tester en jeu] Un événement général n'est pas ajouté le même anniversaire qu'une assimilation NU ou qu'une demande active liée au mal du pays.
- [À tester en jeu] Cooldown commun provisoire de 2 ans.
- [À ajuster après test] Chance provisoire de 25 % par anniversaire éligible.
- [À tester en jeu] « Une amitié inattendue » crée une véritable relation d'amitié avec un enfant de la cour étrangère lorsque c'est possible.
- [À tester en jeu] « L'étranger de la cour » et « Une coutume étrange » peuvent produire de très légers effets de stress ou d'exposition selon la personnalité.
- [À tester en jeu] « Quelques mots familiers » exige une exposition culturelle déjà sensible ; « Deux mondes » exige une exposition plus profonde et ne peut apparaître qu'une fois par enfance.

### Arc spécial : Fugue de l'enfant

- Prévoir un arc rare lié au mal du pays, accessible quel que soit le focus d'éducation.
- L'enfant élevé à l'étranger peut tenter de fuguer afin de rentrer chez lui par ses propres moyens.
- L'arc se déroule en trois étapes :
  1. Lettre annonçant la disparition / fugue de l'enfant.
  2. Période de rumeurs, recherches et informations fragmentaires.
  3. Finalité : l'enfant parvient à revenir de lui-même, est retrouvé avant d'y parvenir, échoue à rentrer, ou autre issue cohérente selon les circonstances.
- Le parent ne contrôle pas directement les décisions prises par l'enfant pendant sa fuite.
- Les compétences, traits, âge, durée du mal du pays, distance et contexte de voyage doivent pouvoir influencer les chances et les issues.
- Le focus d'éducation ne conditionne pas l'accès à la fugue, mais modifie fortement la manière dont l'enfant tente de rentrer et les événements intermédiaires :
  - Diplomatie : convaincre des voyageurs, paysans ou notables de l'aider, avec risque de trop révéler son identité ;
  - Martial : supporter les dangers physiques, intimidation, fuite ou défense ;
  - Intendance : financer et organiser le voyage, avec risques d'arnaque ou de mauvaise gestion ;
  - Intrigue : dissimuler son identité, éviter les recherches, mentir ou emprunter des chemins discrets ;
  - Érudition : s'orienter, lire cartes et indications, comprendre les coutumes locales ou trouver des solutions raisonnées.
- Cet arc doit rester suffisamment rare pour être mémorable.

### Stratégie de test

- Par défaut, regrouper plusieurs chantiers cohérents avant de lancer CK3.
- Éviter les micro-tests après chaque fichier ou sous-étape.
- Faire un test intermédiaire isolé uniquement si une modification présente un risque élevé : chargement du mod, interaction vanilla centrale, état de tutelle, migration de sauvegarde ou autre risque de régression majeure.
- Le système de réactions d'assimilation 1.2 est prévu pour être validé dans un test groupé avec les prochains chantiers.

### Philosophie des Game Rules

- La frontière entre le cœur du mod et les systèmes optionnels ne dépend pas de la version dans laquelle une fonctionnalité a été ajoutée.
- Le cœur de Natural Upbringing correspond à tout ce qui concerne directement l'éducation, la tutelle, l'environnement éducatif et le développement naturel des enfants.
- Tant qu'une fonctionnalité reste centrée sur l'éducation des enfants, elle fait partie du projet de base et ne doit pas être désactivable individuellement.
- Font donc partie du socle du projet :
  - exposition culturelle et religieuse naturelle des enfants ;
  - assimilation culturelle et religieuse pendant l'enfance ;
  - réactions RP liées à ces assimilations ;
  - événements d'éducation Natural Upbringing ;
  - mesures d'accompagnement de la tutelle ;
  - mal du pays / homesickness ;
  - notifications et conséquences directement liées à ces systèmes.
- La règle existante de portée de simulation reste un réglage de performance du cœur de NU et ne désactive pas le système lui-même.
- Les Game Rules optionnelles seront réservées aux extensions qui restent cohérentes avec le mantra du mod mais sortent du scope direct de l'éducation des enfants.
- Exemple prévu à terme : rendre les changements culturels plus organiques au-delà de l'éducation, pour d'autres personnages ou contextes. Ce type d'extension appartient à l'univers de Natural Upbringing, mais sort du projet de base et pourra être désactivable.

### Compatibilité CK3 1.20.0.4

- Hotfix 1.20.0.4 vérifié le 09/10/2026.
- Le changelog officiel contient un correctif unique : un secondary recipient pouvait devenir indisponible après une interaction d'artefact, ce qui bloquait notamment certaines interactions d'éducation des enfants.
- Ce correctif concerne donc indirectement le domaine de NU et semble correspondre au bug vanilla d'interactions de tutelle devenant invalides observé sous Crozier.
- Aucun changement annoncé des systèmes d'éducation, traits, on_actions ou fichiers actuellement surchargés par Natural Upbringing.
- Aucun ajustement de code NU identifié comme nécessaire pour 1.20.0.4 à ce stade.
- Le descriptor reste volontairement sur `supported_version="1.20.0.3"` pendant le développement en cours.
- Passer le descriptor à 1.20.0.4 au moment du prochain déploiement de NU, afin d'éviter une publication intermédiaire uniquement pour supprimer l'avertissement du launcher.

### Compatibilité et philosophie générale

- Natural Upbringing doit continuer à fonctionner avec les aventuriers / personnages sans terres autant que le permet le système vanilla.
- L'ajout du mod à une sauvegarde déjà commencée sous CK3 1.20 doit rester possible.
- Les années d'exposition antérieures à l'activation du mod ne sont pas reconstruites rétroactivement.

## Grandes familles de réactions retenues

| Famille | Traits typiques | Logique RP |
| --- | --- | --- |
| Rejet / Colère | Colérique, Obstiné, Vengeur, Arrogant | Le changement est vécu comme une perte, une trahison ou une remise en cause de l'autorité. |
| Inquiétude / Méfiance | Paranoïaque, Lâche, Timide | Le personnage craint l'influence extérieure ou les conséquences du changement. |
| Acceptation / Empathie | Compatissant, Indulgent, Humble, Confiant | Le personnage accepte plus facilement que l'enfant puisse évoluer différemment. |
| Réflexion / Retenue | Calme, Patient, Tempérant, Juste, Honnête | Le personnage prend du recul et cherche à comprendre avant de juger. |
| Pragmatisme / Opportunisme | Ambitieux, Cupide, Fourbe, Cynique, Arbitraire | Le personnage évalue surtout l'utilité ou l'avantage potentiel du changement. |
| Détachement / Adaptation | Satisfait, Inconstant, Paresseux, Sociable, Excentrique | Le personnage dramatise peu le changement, s'y adapte ou le considère comme secondaire. |

## Pondération de départ validée

- Rejet / Colère :
  - Colérique ++
  - Obstiné +++
  - Vengeur ++
  - Arrogant ++ en culture, + en religion
- Inquiétude / Méfiance :
  - Paranoïaque +++
  - Lâche ++
  - Timide +
- Acceptation / Empathie :
  - Compatissant +++
  - Indulgent ++
  - Humble ++
  - Confiant ++ en culture, + en religion
  - Généreux +
- Réflexion / Retenue :
  - Calme ++
  - Patient ++
  - Tempérant +
  - Juste ++
  - Honnête +
- Pragmatisme / Opportunisme :
  - Ambitieux +++ en culture, ++ en religion
  - Cupide ++ en culture, + en religion
  - Fourbe ++
  - Cynique + en culture, ++++ en religion
  - Arbitraire + en culture, ++ en religion
- Détachement / Adaptation :
  - Satisfait ++
  - Inconstant +++
  - Paresseux +
  - Sociable +++ en culture, + en religion
  - Excentrique ++
- Zélé :
  - influence faible ou nulle pour la culture
  - Rejet +++++ pour la religion

## Logique de résolution validée

- Une réaction dominante unique est calculée séparément pour la culture et la religion.
- En cas d'égalité exacte entre familles pour un même domaine, un ordre déterministe départage les scores afin d'éviter un résultat aléatoire : Rejet / Colère, puis Inquiétude / Méfiance, Acceptation / Empathie, Réflexion / Retenue, Pragmatisme / Opportunisme, Détachement / Adaptation.
- Pour un changement simultané de culture et de religion :
  - si les deux domaines aboutissent à la même famille, cette réaction est retenue et légèrement renforcée ;
  - sinon, la réaction ayant obtenu le score le plus élevé est retenue ;
  - en cas d'égalité parfaite entre les deux domaines, la religion l'emporte pour un personnage Zélé ou Cynique ; sinon la culture sert de départage.
- Si aucun trait pertinent ne donne de score, une réaction neutre de secours est utilisée.

## Conséquences mécaniques validées

- Rejet / Colère :
  - opinion de l'enfant envers le parent : -10 par défaut ;
  - stress léger pour le parent ;
  - réaction combinée renforcée : opinion pouvant atteindre -15 et stress renforcé ;
  - Sadique durcit la perte d'opinion jusqu'à -20 ;
  - Zélé face à une assimilation religieuse peut atteindre -20 d'opinion et un stress moyen.
- Inquiétude / Méfiance :
  - stress léger par défaut ;
  - stress moyen si culture et religion produisent toutes deux cette réaction ;
  - Courageux réduit ce stress d'un niveau ;
  - Insensible supprime la composante de stress.
- Acceptation / Empathie :
  - opinion de l'enfant envers le parent : +10 ;
  - +15 si culture et religion produisent toutes deux cette réaction.
- Réflexion / Retenue :
  - réaction surtout narrative ;
  - opinion de l'enfant envers le parent : +5.
- Pragmatisme / Opportunisme :
  - pas d'effet mécanique direct pour éviter d'en faire une source d'optimisation.
- Détachement / Adaptation :
  - pas d'effet mécanique direct.
- Réaction neutre de secours :
  - pas d'effet mécanique direct.
- Insensible supprime les gains de stress des réactions concernées sans supprimer leurs conséquences relationnelles.
- Aucun gain de prestige, piété, or ou statistique ne doit être attaché à ces réactions.

## État d'implémentation

- [À tester en jeu] Nouveau système de réaction dominante aux assimilations culturelles et religieuses.
- [À tester en jeu] Six familles de personnalité + réaction neutre de secours.
- [À tester en jeu] Pondérations culture/religion distinctes, gestion des égalités et cas combiné culture + religion.
- [À tester en jeu] Conséquences relationnelles et de stress, avec modificateurs pour Insensible, Sadique, Courageux et Zélé.
- L'état de calcul est conservé dans des variables locales à chaque événement afin d'éviter les collisions entre plusieurs enfants ou plusieurs parents joueurs.

## Accompagnement des pupilles déjà sous tutelle

- L'interaction d'accompagnement existe déjà et permet d'ajouter des mesures après la création d'une tutelle.
- Bug identifié : l'interaction était trop permissive et pouvait apparaître sur des enfants sans lien réel avec le joueur, notamment des otages étrangers présents à sa cour.
- Cause : la visibilité acceptait les enfants simplement courtisans du joueur ou placés dans sa hiérarchie.
- Correction retenue : limiter l'accès à la famille proche du joueur. La simple présence à la cour, le statut d'otage ou le fait d'être lié à un vassal ne suffit plus.

### Notification du tuteur après assimilation

- [À tester en jeu] Lorsqu'un pupille change réellement de culture ou de rite par le système NU, son tuteur joueur reçoit désormais une notification légère.
- Le parent joueur conserve l'événement RP complet.
- Si le tuteur est également le parent, aucune notification supplémentaire n'est envoyée afin d'éviter un doublon.
- Si culture et religion changent au même moment sous le même tuteur, une seule notification combinée est envoyée.
- Si, dans un cas inhabituel, les contextes culturels et religieux pointent vers deux tuteurs différents, chacun reçoit uniquement la notification correspondant au changement auquel il est lié.
- Les tuteurs IA ne reçoivent pas d'événement ou de traitement inutile.

## Chantiers 1.2 déjà identifiés

- Refonte des réactions du parent aux assimilations culturelles et religieuses.
- Revoir l'accès aux options d'accompagnement pour les tutelles déjà existantes.
- Ajouter des notifications / réactions pertinentes lorsque le pupille change réellement de culture ou de rite.
- Revoir les Game Rules uniquement lorsque des extensions hors scope direct de l'éducation des enfants seront ajoutées.
- Ajouter de nouveaux événements d'éducation liés aux différents domaines d'éducation. Priorité actuelle : événements normaux. Les événements rares à fort impact seront conçus ensuite comme arcs conditionnels.

## Notes pour le futur changelog

Ne pas rédiger le changelog définitif avant validation en jeu. À la fin du développement, convertir uniquement les fonctionnalités réellement implémentées et testées en notes de version FR/EN.
