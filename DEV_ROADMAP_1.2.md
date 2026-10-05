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
- Ajouter de nouveaux événements d'éducation liés aux différents domaines d'éducation, avec événements normaux et rares.

## Notes pour le futur changelog

Ne pas rédiger le changelog définitif avant validation en jeu. À la fin du développement, convertir uniquement les fonctionnalités réellement implémentées et testées en notes de version FR/EN.
