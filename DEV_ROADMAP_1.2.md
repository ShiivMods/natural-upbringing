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


### Réactions parentales validées pour les 8 événements généraux

Principe général :
- la réponse du parent commente ce qui est arrivé sans modifier rétroactivement l'événement de l'enfant ;
- la formulation dépend d'abord de la famille de personnalité du parent ;
- certains traits particulièrement pertinents peuvent prendre priorité sur la famille générale ;
- les effets mécaniques restent limités au stress du parent lorsque cela est narrativement justifié ;
- éviter les récompenses systématiques ou les effets sur or, prestige, piété ou statistiques.

#### 1. Des nouvelles de mon enfant

Très intégré :
- Rejet / Colère : inquiétude face à une intégration trop forte, petit stress ;
- Inquiétude / Méfiance : intégration jugée trop rapide, petit stress ;
- Acceptation / Empathie : rassuré de savoir l'enfant heureux, petite perte de stress ;
- Réflexion / Retenue : réaction neutre et mesurée ;
- Pragmatisme / Opportunisme : voit l'utilité future de cette adaptation ;
- Détachement / Adaptation : considère cette évolution comme naturelle.

Sociable :
- Rejet : accepte les amitiés tant que l'enfant n'oublie pas les siens ;
- Méfiance : s'interroge sur les fréquentations ;
- Acceptation : rassuré que l'enfant ne soit pas seul, petite perte de stress ;
- Réflexion : considère que la familiarité avec la cour passe par les relations ;
- Pragmatisme : voit la valeur future de bonnes relations ;
- Adaptation : constate que l'enfant sait se débrouiller seul.

Réservé :
- Rejet : se rassure du fait que l'enfant ne soit pas absorbé par la cour étrangère ;
- Méfiance : s'inquiète de l'isolement, petit stress ;
- Acceptation : espère que l'enfant trouvera quelqu'un à qui se confier, petit stress possible ;
- Réflexion : considère que certains enfants ont besoin de davantage de temps ;
- Pragmatisme : estime que l'enfant devra tout de même apprendre à vivre parmi eux ;
- Adaptation : fait confiance au rythme de l'enfant.

Difficile :
- Rejet : remet en cause la cour étrangère plutôt que l'enfant ;
- Méfiance : voit ses craintes confirmées, petit stress ;
- Acceptation : craint que l'enfant ne souffre davantage qu'on ne le dit, petit stress ;
- Réflexion : cherche la raison de cette résistance ;
- Pragmatisme : considère que l'enfant doit apprendre quand céder et quand tenir bon ;
- Adaptation : suppose que l'enfant finira par trouver sa place.

Fallback :
- réponse neutre commune possible.

#### 2. Une amitié inattendue

- Rejet / Colère : accepte la relation tant que l'enfant n'oublie pas les siens ;
- Inquiétude / Méfiance : s'interroge sur l'identité et l'influence de l'autre enfant, petit stress possible pour les personnalités très méfiantes ;
- Acceptation / Empathie : rassuré que l'enfant ait trouvé quelqu'un, petite perte de stress ;
- Réflexion / Retenue : voit l'amitié d'enfance comme potentiellement durable ;
- Pragmatisme / Opportunisme : pense à l'utilité future de cette relation ;
- Détachement / Adaptation : considère l'amitié comme normale.

Si l'amitié devient meilleure amitié :
- renforcer légèrement les réactions positives, prudentes ou opportunistes.

Si l'amitié devient béguin :
- utiliser la logique de réaction du Béguin.

#### 3. L'étranger de la cour

Repli :
- Rejet / Colère : colère contre ceux qui traitent l'enfant ainsi, petit stress ;
- Inquiétude / Méfiance : voit ses craintes confirmées, petit stress ;
- Acceptation / Empathie : regret de ne pas pouvoir soutenir directement l'enfant, petit stress ;
- Réflexion / Retenue : considère l'épreuve comme formatrice ;
- Pragmatisme / Opportunisme : estime que l'enfant doit apprendre à supporter ce regard ;
- Détachement / Adaptation : minimise l'incident comme une cruauté passagère.

Défi :
- Rejet : satisfaction que l'enfant ne se soit pas laissé humilier, petite perte de stress possible ;
- Méfiance : craint une escalade ;
- Acceptation : accepte la défense de soi mais souhaite éviter une guerre personnelle ;
- Réflexion : voit l'enfant apprendre à défendre son identité ;
- Pragmatisme : voit une leçon utile de fermeté ;
- Adaptation : considère que l'enfant a trouvé sa propre manière de répondre.

Si une rivalité apparaît :
- ajouter une réaction spécifique de préoccupation ou, pour un parent Vengeur, de soutien à la mémoire de l'affront.

Adaptation :
- Rejet : craint que l'enfant banalise ce qui le distingue ;
- Méfiance : estime que l'enfant s'adapte peut-être trop bien ;
- Acceptation : rassuré de voir l'enfant capable d'en rire, petite perte de stress ;
- Réflexion : valorise la capacité à désamorcer sans s'effacer ;
- Pragmatisme : voit une compétence sociale utile ;
- Adaptation : constate simplement que l'enfant apprend vite.

#### 4. Une coutume étrange

Résistance :
- Rejet / Colère : satisfait que l'enfant conserve les usages familiaux, petite perte de stress possible ;
- Inquiétude / Méfiance : craint qu'on cherche à lui imposer davantage ;
- Acceptation / Empathie : souhaiterait davantage de compréhension avant rejet ;
- Réflexion / Retenue : considère la comparaison des usages comme un apprentissage ;
- Pragmatisme / Opportunisme : estime qu'un rejet pur nuit à la compréhension de la cour ;
- Détachement / Adaptation : suppose que l'enfant s'habituera peut-être avec le temps.

Curiosité :
- Rejet : trouve que l'enfant s'intéresse peut-être trop aux usages locaux ;
- Méfiance : considère certaines curiosités potentiellement dangereuses ;
- Acceptation : encourage à comprendre avant de juger, petite perte de stress possible ;
- Réflexion : valorise fortement la démarche, petite perte de stress ;
- Pragmatisme : voit l'intérêt de comprendre les usages pour comprendre les gens ;
- Adaptation : considère cela comme une exploration naturelle.

Enthousiasme :
- Rejet : regrette que l'enfant ne montre pas la même ferveur pour ses propres traditions, petit stress ;
- Méfiance : s'inquiète de l'influence de la cour, petit stress possible ;
- Acceptation : rassuré de voir l'enfant découvrir avec joie, petite perte de stress ;
- Réflexion : voit une occasion de comprendre d'autres manières de vivre ;
- Pragmatisme : voit un avantage à maîtriser les usages de la cour étrangère ;
- Adaptation : constate que l'enfant semble déjà à l'aise.

Override Zélé :
- si la coutume touche à un rite différent, la réaction religieuse peut prendre priorité sur la famille générale ;
- une exposition religieuse étrangère peut provoquer petit ou moyen stress selon l'écart religieux.

#### 5. Quelques mots familiers

Événement volontairement léger :
- Rejet / Colère : remarque avec gêne que même la manière de parler change ;
- Inquiétude / Méfiance : reconnaît de moins en moins certaines expressions ;
- Acceptation / Empathie : reste surtout heureux de reconnaître l'enfant derrière les nouvelles habitudes ;
- Réflexion / Retenue : considère l'influence linguistique comme naturelle ;
- Pragmatisme / Opportunisme : voit l'avantage de mieux comprendre la manière de penser locale ;
- Détachement / Adaptation : banalise quelques expressions étrangères.

Par défaut, aucun effet mécanique. Petit stress possible uniquement pour des cas très marqués.

#### 6. Entre deux mondes

- Rejet / Colère : craint une perte d'identité, petit stress ;
- Inquiétude / Méfiance : craint que l'enfant n'appartienne pleinement à aucun monde, petit stress ;
- Acceptation / Empathie : accepte que l'enfant n'ait pas à choisir, petite perte de stress ;
- Réflexion / Retenue : voit une identité nouvelle façonnée par deux environnements ;
- Pragmatisme / Opportunisme : voit un avantage à comprendre deux mondes ;
- Détachement / Adaptation : considère cette double appartenance comme parfaitement vivable.

Si des serviteurs culturels ont été envoyés :
- Rejet : se rassure de voir une part du foyer préservée ;
- Acceptation : se réjouit d'avoir laissé quelque chose de chez eux à l'enfant ;
- Pragmatisme : considère que les précautions prises avant le départ ont été utiles.

#### 7. Le béguin

Si le béguin est secret :
- aucune réaction parentale, car le parent n'en a pas connaissance.

Si le béguin est connu :
- Rejet / Colère : considère que l'enfant n'a pas été envoyé là-bas pour cela ;
- Inquiétude / Méfiance : veut en savoir davantage sur l'autre enfant ;
- Acceptation / Empathie : réaction attendrie, petite perte de stress ;
- Réflexion / Retenue : considère les premiers attachements avec recul ;
- Pragmatisme / Opportunisme : s'intéresse immédiatement à la famille et au statut de l'autre enfant ;
- Détachement / Adaptation : banalise le béguin d'enfance.

Overrides possibles :
- parent Chaste : gêne ou désapprobation légère ;
- parent Luxurieux : amusement ou encouragement, neutre ou petite perte de stress ;
- parent Paranoïaque : craint que l'attachement soit exploité, petit stress ;
- parent Ambitieux : peut voir l'intérêt politique d'un béguin vers une famille importante.

Pour un béguin homosexuel connu :
- si le rite du parent l'accepte, réaction normale ;
- si le rite le réprouve, la réaction religieuse peut prendre priorité ;
- parent Zélé : désapprobation forte, stress moyen possible ;
- parent Compatissant dans un rite hostile : réaction protectrice possible malgré le conflit religieux.

#### 8. Le Rival

Rivalité inchangée :
- Rejet / Colère : encourage l'enfant à ne pas se laisser marcher dessus ;
- Inquiétude / Méfiance : juge la querelle trop longue, petit stress possible ;
- Acceptation / Empathie : souhaite une réconciliation ;
- Réflexion / Retenue : considère que certaines inimitiés s'éteignent avec le temps ;
- Pragmatisme / Opportunisme : voit un rival comme une source d'apprentissage ;
- Détachement / Adaptation : suppose qu'ils finiront peut-être par se lasser.

Rival → Ami :
- Rejet : surpris par le retournement ;
- Méfiance : prudence face à une réconciliation soudaine ;
- Acceptation : soulagé, petite perte de stress ;
- Réflexion : valorise le pardon ;
- Pragmatisme : voit la valeur d'un ancien rival devenu allié ;
- Adaptation : considère que les querelles d'enfants changent vite.
- Parent Vengeur : désapprouve le pardon trop rapide, petit stress ;
- Parent Indulgent : satisfait de la réconciliation, petite perte de stress.

Rival → Némésis :
- Rejet / Colère : constate que la querelle est devenue sérieuse ;
- Inquiétude / Méfiance : craint la création d'un véritable ennemi, petit stress ;
- Acceptation / Empathie : regrette l'absence de pardon, petit ou moyen stress ;
- Réflexion / Retenue : souligne qu'une rancune si jeune peut durer longtemps ;
- Pragmatisme / Opportunisme : insiste sur la nécessité de connaître la valeur de l'adversaire ;
- Détachement / Adaptation : espère qu'ils grandiront avant leur haine.
- Parent Vengeur : peut comprendre ou approuver la rancune, neutre ou petite perte de stress ;
- Parent Compatissant : forte inquiétude, stress moyen.

Rival → Béguin :
- reprendre la logique du Béguin ;
- variantes possibles :
  - Réflexion : le cœur prend parfois des chemins étranges ;
  - Adaptation : manière inattendue de mettre fin à une rivalité ;
  - Méfiance : passage rapide de la haine à l'affection jugé inquiétant ;
  - Pragmatisme : considère au moins la rivalité comme désamorcée.
- si le béguin doit rester secret, aucune notification au parent.


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



### Pack validé d'événements normaux liés aux 5 domaines d'éducation

Philosophie générale :
- premier pack : 10 événements, soit 2 par focus d'éducation ;
- uniquement disponibles si l'enfant possède le focus correspondant ;
- les événements racontent ce que l'enfant vit réellement à l'étranger ;
- le parent reçoit la nouvelle après résolution des actions de l'enfant ;
- le parent ne contrôle pas rétroactivement les décisions de l'enfant ;
- les résultats sont influencés par les traits de personnalité, traits d'enfance, aptitude correspondante et relation avec le tuteur ;
- effets d'éducation sobres :
  - +2 points = réussite particulièrement formatrice ;
  - +1 point = expérience utile ;
  - 0 = échec ou expérience sans bénéfice scolaire direct ;
  - aucun point négatif pour ces événements normaux ;
- les points sont ajoutés à la variable vanilla correspondant au focus courant ;
- les variantes structurelles doivent respecter le contexte de la cour : gouvernement, mode de vie, institutions et ressources disponibles.

#### Diplomatie 1 : Entre deux querelles

Un conflit éclate entre deux jeunes de la cour et l'enfant tente spontanément de s'interposer.

Résultats :
- Médiateur efficace :
  - favorisé par Sociable, Patient, Compatissant, Juste et bonne Diplomatie ;
  - +2 points Diplomatie ;
  - petite opinion positive du tuteur envers l'enfant ;
  - possibilité légère de progression relationnelle positive avec un protagoniste.
- Compromis imparfait :
  - résultat normal ;
  - +1 point Diplomatie.
- Jette de l'huile sur le feu :
  - favorisé par Colérique, Arrogant, Arbitraire, Impatient ;
  - aucun point ;
  - petite perte d'opinion tuteur → enfant ;
  - stress mineur possible selon personnalité.

#### Diplomatie 2 : Un visage venu d'ailleurs

L'enfant échange avec un visiteur ou jeune personnage extérieur à sa cour habituelle.

Résultats :
- À l'aise avec l'étranger :
  - favorisé par Sociable, Confiant, Curieux ;
  - +1 point Diplomatie ;
  - +1 exposition culturelle ;
  - petite chance de relation positive avec le visiteur si un personnage persistant pertinent existe.
- Maladroit mais instructif :
  - +1 point Diplomatie.
- Fermeture :
  - favorisée par Timide, Paranoïaque, éventuellement Zélé selon contexte ;
  - aucun bonus.

#### Martial 1 : Le terrain plutôt que les livres

L'enfant comprend mieux l'enseignement martial par la pratique que par la théorie.

Résultats :
- Très à l'aise :
  - favorisé par Brave, Diligent, Obstiné et traits d'enfance martiaux pertinents ;
  - +2 points Martial ;
  - petite opinion positive du tuteur ;
  - faible chance de +1 Prouesse si la scène justifie réellement un progrès physique notable.
- Progression normale :
  - +1 point Martial ;
  - très faible chance de +1 Prouesse uniquement si le résultat et le contexte le justifient.
- Mauvaise discipline :
  - favorisée par Paresseux, Impatient, Arrogant ;
  - aucun point supplémentaire ;
  - pas de gain de Prouesse.

Les gains de Prouesse ne doivent jamais devenir systématiques : ils représentent un progrès physique concret et exceptionnel, pas une récompense attachée automatiquement à l'événement.

#### Martial 2 : Un coup de trop

Un entraînement ou jeu martial devient plus sérieux que prévu.

Résultats :
- Retient son coup :
  - favorisé par Calme, Patient, Compatissant ;
  - +1 point Martial ;
  - opinion positive avec l'autre enfant ;
  - progression vers amitié possible.
- Va jusqu'au bout :
  - favorisé par Brave, Colérique, Obstiné ;
  - +1 point Martial ;
  - opinion négative avec l'autre enfant ;
  - faible chance de rivalité ;
  - faible chance de +1 Prouesse si la performance martiale le justifie.
- Prend plaisir à dominer :
  - Sadique fortement favorisé ;
  - +1 point Martial possible ;
  - probabilité de rivalité renforcée ;
  - +1 Prouesse possible uniquement si la scène correspond réellement à une amélioration physique démontrée.

Aucun gain automatique de Prouesse et aucun bonus supérieur à +1 dans ces événements normaux.

#### Intendance 1 : Quelque chose ne compte pas

L'enfant remarque une incohérence dans les ressources ou la gestion de la cour.

Le contenu varie selon le contexte :
- féodal / administratif / république : comptes, dépenses, taxes, stocks ;
- tribal : tribut, réserves, butin, redistribution ;
- nomade : troupeaux, provisions, routes saisonnières, réserves.

Résultats :
- Trouve réellement l'erreur :
  - favorisé par Diligent, Cupide, Juste, Patient ;
  - +2 points Intendance ;
  - opinion positive du tuteur.
- Bonne intuition, mauvaise conclusion :
  - +1 point Intendance.
- Accusation trop rapide :
  - favorisée par Paranoïaque, Arbitraire, Impatient ;
  - aucun bonus ;
  - stress léger ou opinion négative possible.

#### Intendance 2 : Faire durer les réserves

L'enfant assiste à une décision de répartition de ressources limitées.

Résultats :
- Bonne solution :
  - favorisée par Tempérant, Diligent, Patient, Généreux selon le contexte ;
  - +2 points Intendance ;
  - +1 exposition culturelle.
- Apprentissage :
  - +1 point Intendance ;
  - +1 exposition culturelle.
- Mauvaise priorité :
  - favorisée par Glouton, Cupide, Arbitraire selon contexte ;
  - aucun point.

#### Intrigue 1 : Ce n'était pas destiné à ses oreilles

L'enfant surprend une conversation ou une information qui ne lui était pas destinée.

Résultats :
- Garde l'information :
  - favorisé par Fourbe, Paranoïaque, Calme ;
  - +2 points Intrigue ;
  - possibilité de gagner un hook faible contre la personne concernée si l'information fournit réellement un levier crédible ;
  - la cible peut être un membre de la cour étrangère ou le tuteur lui-même.
- Révèle l'information au tuteur :
  - favorisé par Honnête, Confiant, Compatissant ;
  - +1 point Intrigue ;
  - opinion positive du tuteur possible ;
  - si l'information est exploitable, le tuteur peut lui aussi obtenir un hook faible contre la personne concernée ;
  - l'enfant peut conserver son propre hook lorsque cela reste cohérent : révéler une information n'efface pas nécessairement le fait qu'il la connaît.
- Se fait remarquer :
  - aucun bonus ;
  - gêne ou stress léger possible ;
  - aucun hook si l'information n'a pas pu être réellement comprise ou conservée.

Les hooks ne sont pas nécessairement annoncés au parent joueur dans la lettre. Ils peuvent exister comme conséquence cachée et devenir pertinents plus tard.

Aucun hook fort n'est accordé par ces événements normaux.

#### Intrigue 2 : Je sais quelque chose que tu ignores

L'enfant utilise volontairement une information pour influencer quelqu'un.

Résultats :
- Manipulation réussie :
  - favorisée par Fourbe, Patient, Ambitieux ;
  - +2 points Intrigue ;
  - légère opinion négative de la cible ;
  - possibilité d'obtenir un hook faible approprié sur la cible si l'information constitue un levier crédible ;
  - faible chance de rivalité selon cible et personnalités.
- Négociation subtile :
  - +1 point Intrigue ;
  - hook faible possible mais plus rare que dans la réussite complète.
- Retour de bâton :
  - favorisé par Arrogant, Impatient ou Honnête selon la manière ;
  - aucun point ;
  - opinion négative avec la cible ;
  - petite chance de rivalité ;
  - pas de hook gagné.

Le système doit utiliser un type de hook faible cohérent avec la scène et vérifier que le hook peut légalement être ajouté avant de le créer.

#### Érudition 1 : Deux enseignements, deux vérités

L'enfant découvre une contradiction entre ce qu'on lui enseignait chez lui et ce qu'il apprend dans la cour étrangère.

Résultats :
- Cherche à comprendre les deux :
  - favorisé par Curieux, Patient, Cynique ;
  - +2 points Érudition ;
  - +1 exposition culturelle ;
  - +1 exposition au rite si la contradiction est religieuse.
- Accepte l'enseignement local :
  - favorisé par Confiant ou forte intégration ;
  - +1 point Érudition ;
  - +1 exposition correspondante.
- Rejette fermement :
  - favorisé par Zélé, Obstiné ;
  - +1 point Érudition ;
  - -1 exposition étrangère correspondante.

Même la résistance peut donc améliorer l'éducation sans favoriser l'assimilation.

#### Érudition 2 : Pourquoi ?

Une question de l'enfant transforme une leçon courte en longue discussion.

Résultats :
- Questionnement fécond :
  - favorisé par Curieux, Patient, Diligent ;
  - +2 points Érudition ;
  - opinion du tuteur modulée par sa propre personnalité.
- Bonne curiosité :
  - +1 point Érudition.
- Questionne pour contester :
  - favorisé par Arrogant, Obstiné, Cynique ;
  - +1 point Érudition ;
  - petite perte d'opinion du tuteur possible.

Le trait Cynique peut donc être très favorable à l'apprentissage tout en rendant l'enfant difficile à enseigner.

### Effets spéciaux du pack par focus

Prouesse :
- réservée aux événements Martial lorsque la scène représente réellement une progression physique ;
- gain maximal normal : +1 ;
- toujours rare et conditionnel ;
- jamais accordée automatiquement à chaque succès martial.

Hooks :
- réservés aux événements Intrigue lorsque l'enfant découvre ou exploite une information fournissant un véritable levier ;
- peuvent viser un membre de la cour étrangère ou le tuteur ;
- si l'enfant révèle l'information au tuteur, le tuteur peut lui aussi obtenir un hook faible sur la cible ;
- l'enfant peut conserver son hook lorsque cela reste cohérent ;
- les hooks peuvent rester cachés dans la présentation au parent joueur ;
- aucun hook fort dans ce pack d'événements normaux.


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

Principes validés :
- arc rare lié au mal du pays ;
- âge minimum : 12 ans ;
- mal du pays présent depuis au moins 1 an ;
- l'enfant doit toujours être réellement élevé à l'étranger ;
- une seule fugue réelle maximum par enfant dans cette version ;
- une prochaine version pourra ajouter un événement spécifique permettant exceptionnellement une seconde fugue ;
- le focus d'éducation ne conditionne pas l'accès à la fugue, mais détermine la compétence utilisée pour progresser pendant la fuite ;
- le parent ne contrôle pas les décisions prises par l'enfant pendant la fugue.

Chance de déclenchement :
- valeur validée : 5 % pour le déclenchement spontané ;
- un seul jet spontané lorsqu'un enfant devient éligible après au moins 1 an de mal du pays ;
- si ce jet échoue, il n'est pas répété automatiquement chaque mois ou chaque anniversaire ;
- les déclenchements contextuels déjà prévus, notamment la variante « Difficile » de « Des nouvelles de mon enfant », peuvent toujours proposer leur propre très faible chance tant que l'enfant n'a jamais réellement fugué ;
- dès qu'une fugue réelle commence, un flag permanent interdit toute nouvelle fugue dans cette version.

Structure visible :
1. La disparition.
2. Après un délai aléatoire de 2 à 4 mois : Recherches / rumeurs.
3. Après un nouveau délai aléatoire de 3 à 5 mois : Conclusion.
- durée normale de chaîne visible : environ 5 à 9 mois ;
- une résolution critique peut terminer la chaîne plus tôt.

Progression cachée mensuelle :
- dès le début de la fugue, un test mécanique caché est effectué environ une fois par mois ;
- ces tests ne génèrent pas d'événement visible et servent uniquement à représenter la progression réelle de l'enfant entre les grandes nouvelles ;
- la compétence utilisée est celle correspondant au focus d'éducation actuel :
  - Diplomatie ;
  - Martial ;
  - Intendance ;
  - Intrigue ;
  - Érudition ;
- le palier est recalculé à partir de la valeur actuelle de la compétence de l'enfant.

Paliers de compétence validés :
- Exécrable : 3 ou moins ;
- Mauvais : 4 à 6 ;
- Moyen : 7 à 9 ;
- Bon : 10 à 13 ;
- Excellent : 14 ou plus.

Variable cachée de progression :
- départ à 0 ;
- réussite mensuelle : +1 ;
- échec mensuel : -1 ;
- neutre : 0 ;
- la progression cumulée doit influencer les nouvelles intermédiaires et la conclusion.

Résolutions critiques :
- une réussite critique signifie que l'enfant parvient à rentrer chez lui avant la prochaine étape prévue ;
- un échec critique signifie qu'il est retrouvé / intercepté et ramené chez son tuteur ;
- certains échecs critiques cohérents avec le contexte peuvent comporter un risque exceptionnel de blessure grave ou de mort ;
- la mort ne doit jamais être l'issue normale d'un échec critique.

Progression mensuelle validée :
- Exécrable, 3 ou moins : 50 % échec, 35 % neutre, 15 % réussite ;
- Mauvais, 4 à 6 : 35 % échec, 40 % neutre, 25 % réussite ;
- Moyen, 7 à 9 : 25 % échec, 35 % neutre, 40 % réussite ;
- Bon, 10 à 13 : 15 % échec, 30 % neutre, 55 % réussite ;
- Excellent, 14 ou plus : 8 % échec, 22 % neutre, 70 % réussite ;
- le palier est recalculé à partir de la compétence actuelle de l'enfant à chaque test mensuel.

Résolutions critiques validées :
- ne pas effectuer un jet critique indépendant chaque mois ;
- progression cumulée de +4 : réussite critique, l'enfant parvient à rentrer avant la prochaine grande étape ;
- progression cumulée de -4 : déclenche un sous-jet caché d'échec critique ;
- l'échec critique n'a donc pas un résultat ou un texte unique : le sous-jet détermine la gravité réelle de l'issue ;
- résultat neutre de l'échec critique : l'enfant est retrouvé / intercepté puis ramené chez son tuteur ;
- résultat aggravé : blessure, épuisement sévère, vol, capture temporaire ou autre conséquence cohérente avec le domaine utilisé ;
- résultat exceptionnel : blessure grave ou mort lorsque le contexte permet réellement une issue létale ;
- chaque résultat possède son propre texte visible, et les formulations doivent également varier selon le domaine d'éducation ;
- la mort doit rester un sous-résultat exceptionnel de l'échec critique, jamais son issue par défaut ;
- cela évite qu'une succession de nombreux jets mensuels rende les critiques artificiellement fréquentes.

Variation par domaine :
- Diplomatie : obtenir l'aide de voyageurs, paysans ou notables, convaincre, négocier, risque de révéler son identité ;
- Martial : supporter les dangers physiques, se défendre, intimider ou fuir ;
- Intendance : gérer argent, provisions, transport et itinéraire, avec risques d'arnaque ou de mauvaise gestion ;
- Intrigue : cacher son identité, mentir, éviter les recherches et emprunter des routes discrètes ;
- Érudition : s'orienter, exploiter cartes et indications, comprendre les coutumes locales et raisonner son trajet.

Retour réussi :
- si l'enfant rentre chez lui, le parent peut décider de le laisser rester ou de le renvoyer auprès de son tuteur ;
- laisser l'enfant rester met fin à la tutelle étrangère et au mal du pays ;
- accepter son retour augmente l'opinion de l'enfant envers le parent ;
- le renvoyer auprès de son tuteur diminue l'opinion de l'enfant envers le parent ;
- les réactions et effets secondaires du choix du parent sont adaptatifs selon sa personnalité, sur le même principe que les autres réactions parentales de NU ;
- le choix du parent ne modifie pas rétroactivement la réussite de la fugue elle-même ;
- aucune nouvelle fugue n'est possible dans cette version après une première fugue réelle.

Prestige lié à l'issue :
- une fugue réussie et un retour effectif au foyer accordent du prestige à l'enfant, indépendamment du choix ultérieur du parent ;
- une fugue échouée retire une petite quantité de prestige à l'enfant ;
- le prestige représente la réputation acquise ou perdue par l'enfant à la suite de cette aventure ;
- les valeurs exactes restent à équilibrer, avec une préférence pour les échelles vanilla mineures ou moyennes plutôt que des nombres arbitraires.

### Affichage de la fugue dans l'onglet Situations

- direction technique validée : privilégier un Story Cycle visible plutôt qu'une grande Situation mondiale ;
- les Story Cycles sont désormais affichés dans l'onglet Situations du jeu et peuvent montrer un personnage ainsi qu'une chaîne d'informations personnalisées ;
- pendant une fugue active, le parent joueur pourrait voir une entrée dédiée contenant notamment :
  - l'enfant concerné ;
  - le temps écoulé depuis sa disparition ;
  - son domaine d'éducation ;
  - un état qualitatif de la recherche / progression ;
  - éventuellement la dernière information connue ;
- ne pas afficher directement la valeur brute de progression cachée : privilégier une description qualitative ;
- le Story Cycle se termine dès que la fugue est résolue.
- évolution future hors 1.2 : utiliser cet espace pour suivre plus largement tous les enfants élevés à l'étranger et leur situation / ressenti.

### Influence globale très légère sur l'acceptation culturelle

Principe validé :
- cette mécanique fait partie du cœur de Natural Upbringing et n'est pas désactivable ;
- tout enfant réellement élevé dans une cour d'une culture différente de la sienne contribue très légèrement à l'acceptation entre sa culture et celle de la cour d'accueil ;
- le système s'applique aussi aux enfants IA selon son propre scope de simulation ;
- cette contribution cesse immédiatement si l'enfant assimile la culture locale ;
- elle cesse également lorsqu'il quitte durablement la cour étrangère ou n'est plus dans une situation d'éducation étrangère valide ;
- objectif : représenter les liens humains créés par l'éducation interculturelle sans faire de la tutelle un outil d'optimisation.

Équilibrage :
- le gain doit être extrêmement faible, inférieur aux gains événementiels vanilla ordinaires ;
- ordre de grandeur retenu pour équilibrage : environ +0,01 à +0,02 d'acceptation par année complète et par enfant ;
- la valeur finale exacte sera choisie lors de l'implémentation / des tests ;
- prévoir un plafond annuel par paire de cultures afin d'empêcher l'exploitation via un grand nombre de pupilles.

Scope indépendant :
- ajouter une Game Rule dédiée à la portée de cette mécanique ;
- la mécanique reste toujours active, la règle ne modifie que son périmètre ;
- réglages prévus :
  - Suivre la portée générale de NU, réglage par défaut ;
  - Famille proche uniquement ;
  - Cour du joueur ;
  - Royaume du souverain ;
  - Royaume et royaumes voisins ;
  - Monde entier.
- ce scope indépendant permet de conserver une simulation éducative limitée tout en simulant, si désiré, les micro-effets culturels à plus grande échelle.

### Catégorie de Game Rules Natural Upbringing

- créer une catégorie personnalisée natural_upbringing dans l'interface vanilla des Game Rules ;
- localisation FR : « Natural Upbringing » ;
- les règles propres au mod doivent être regroupées dans cette catégorie plutôt que dispersées entre Culture, Foi et Ajustements ;
- y placer au minimum :
  - Portée de la simulation ;
  - Portée de l'acceptation culturelle ;
- conserver une interface native au jeu, sans créer de nouvel écran personnalisé ;
- les futures Game Rules réellement nécessaires à NU rejoindront cette catégorie ;
- ne pas transformer les fonctionnalités centrales d'éducation en options activables/désactivables individuellement.


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
