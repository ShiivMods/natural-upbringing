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
