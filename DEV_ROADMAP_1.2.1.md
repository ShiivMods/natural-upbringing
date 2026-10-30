# Natural Upbringing 1.2.1 - Exposure Rework

## Version realignment

The previous roadmap is reorganized as follows.

### 1.2.1 - Exposure Rework

The former 1.3 exposure overhaul becomes 1.2.1, except for Hybrid Culture requirements/interactions.

Main scope:

- simultaneous exposure to multiple Cultures, Faiths and Rites;
- exposure decay;
- Adventurer/Camp support;
- County Culture as an environmental factor for both landed and landless characters;
- Court/Camp demographic influence;
- parents and guardian influence;
- cultural proximity and language modifiers;
- adult exposure without automatic adult culture conversion;
- foundations required by the later Foreign Education Story Cycle.

### 1.2.2 - Foreign Education & Advanced Integration

The former 1.2.1 and 1.2.2 scopes are merged here.

Main scope:

- full Foreign Education Story Cycle;
- deliberate incentives for sending children abroad;
- improved AI guardianship proposals;
- rare adulthood events linked to education and field of study;
- raised-abroad trait;
- Cultural Traditions integration;
- deeper religious logic, including monotheistic/polytheistic differences;
- Hybrid Culture requirements and interactions;
- further balancing and narrative integration of the 1.2.1 exposure system.

---

# 1. Core principle

Exposure and assimilation are separate systems.

A character may be strongly exposed to several cultures, faiths or rites at the same time without automatically changing identity.

Exposure represents familiarity, social environment and lived experience.

Assimilation is a rarer identity change and must require sustained conditions.

This distinction is mandatory to prevent rapid culture/faith switching.

---

# 2. Multiple simultaneous exposure

A character can maintain several active exposure tracks simultaneously.

Each track stores at minimum:

- target Culture / Faith / Rite;
- exposure score;
- total years exposed;
- current uninterrupted exposure streak;
- whether the target was actively reinforced during the current yearly update.

Exposure tracks are independent.

A character can therefore remain culturally Norse while simultaneously carrying meaningful Cisalpine, Greek and Lombard exposure.

The same principle applies to Faith and Rite.

---

# 3. Court / Camp dominance

A Culture, Faith or Rite is considered socially dominant when at least 33% of the relevant Court or Camp population shares it.

Several identities may therefore be dominant simultaneously.

Example:

- Cisalpine: 45% -> active social influence;
- Norse: 35% -> active social influence;
- Greek: 20% -> no passive Court/Camp influence.

The system must not treat "dominant" as synonymous with "absolute majority".

For Rites, the denominator should be the population belonging to the relevant parent Faith rather than the entire Court/Camp whenever technically possible.

Adventurer Camps use the same social principle as ordinary Courts.

---

# 4. Cultural exposure sources

The initial 1.2.1 implementation uses the following sources.

## Direct influence

- Guardian Culture.
- Parent Culture(s).

Parents are intentionally important.

A living parent who shares the child's current Culture helps preserve that identity and reduces the probability of assimilating into a foreign Culture, but never grants complete immunity.

A parent belonging to another Culture may instead reinforce exposure to that Culture.

## Social environment

- Every Culture meeting the 33% Court/Camp dominance threshold.

## Territorial environment

- Culture of the County in which the character currently lives.

County Culture applies to both ordinary Courts and Adventurer Camps.

For Adventurers, the current Camp/Domicile location must be used instead of assuming that the character's Court Owner represents the local cultural environment.

The County has two functions:

1. it creates a small amount of exposure by itself;
2. it strengthens other sources of exposure to the same Culture by a percentage modifier.

This makes a Culture more influential when the guardian/social environment and the surrounding population reinforce one another, without allowing County Culture alone to overwhelm a closed household within a few years.

---

# 5. Cultural proximity modifiers

Exposure to a target Culture is accelerated when cultural distance is lower.

Initial modifiers to support:

- shared Heritage;
- shared cultural language;
- target Culture's language already known by the character.

These bonuses may stack, but the final multiplier must be capped to avoid extremely rapid assimilation.

The language-known bonus represents active comprehension and is distinct from two cultures naturally sharing the same cultural language.

Cultural Traditions remain reserved for 1.2.2.

---

# 6. Age

Age affects the speed at which exposure is internalized.

Children are more impressionable than adults.

The implementation should preserve the general hierarchy:

- early childhood: strongest exposure gain;
- middle childhood: strong;
- pre-adolescence: moderate;
- adolescence: weaker;
- adulthood: exposure can still grow, but no automatic culture conversion occurs from exposure alone.

Exposure tracking begins at birth.

A newborn receives an initial Cultural exposure profile immediately, before the first yearly update. This prevents infancy from being culturally invisible to the simulation.

Automatic assimilation may remain unavailable during the earliest years even while exposure is already accumulating.

---

# 6A. Cultural exposure at birth

The character's current Culture is itself tracked as an exposure.

It is not merely an identity label outside the exposure system.

At birth, the child receives an initial Cultural exposure profile totaling 100 birth-share points.

The baseline model uses four equal anchors worth 25 points each:

1. the child's current Culture: 25;
2. parent A's Culture: 25;
3. parent B's Culture: 25;
4. the child's immediate social environment at birth: 25.

If several anchors point to the same Culture, their shares are combined.

Examples:

- Norse child + one Norse parent + one French parent + Norse environment -> Norse 75 / French 25.
- Norse child + two Norse parents + Norse environment -> Norse 100.
- Norse child + one Norse parent + one French parent + French environment -> Norse 50 / French 50.

These values are birth shares used to seed the persistent exposure tracks. They do not require all later exposure scores to remain normalized to a total of 100.

The current Culture receives this birth anchor only once. A later assimilation does not grant a fresh artificial +25 identity bonus.

After birth, every Culture follows the normal exposure rules:

- active sources reinforce it;
- absent sources allow it to decay;
- the current Culture can therefore weaken over time if nothing in the child's lived environment continues to support it.

This is intentional and allows a child culturally labelled Norse at birth, but genuinely raised without Norse social contact, to gradually become more strongly rooted in another Culture.

## Birth environment anchor

The 25-point environment anchor represents the child's immediate social household/Court/Camp environment at birth, not a duplicate County bonus.

If one Culture clearly represents that immediate environment, it receives the full 25 points.

If several Cultures simultaneously meet the Court/Camp dominance threshold, the 25 points should be distributed between those dominant Cultures according to their relative representation rather than granting 25 points to each.

County Culture remains a separate universal exposure source from birth onward through the normal environmental update.

If no valid Court/Camp social environment can be resolved at birth, the fallback for this anchor should be the character's current Culture rather than inventing an unrelated local identity.

## Missing parent edge cases

The normal case assumes two known parents.

If one parental Culture cannot be resolved, its 25-point anchor falls back to the child's current Culture.

This keeps the birth profile at 100 points and avoids an unknown parent weakening the child's starting cultural identity for purely technical reasons.


---

# 7. Exposure decay

Every exposure track is updated independently.

When a Culture/Faith/Rite is no longer reinforced by any current source:

- its exposure score decreases every yearly update;
- its uninterrupted exposure streak is broken;
- the track is eventually removed if its score reaches zero.

Old exposure must never remain permanently eligible for assimilation after the character has left the environment that created it.

A historical exposure may persist for years while fading, but cannot cause a delayed identity change without a current source.

The existing 1.2 permanent exposure floors are therefore not the target model for 1.2.1.

---

# 8. Anti-churn assimilation rules

The following safeguards are mandatory.

## 8.1 Active source requirement

A Culture can only be considered for assimilation if it was actively reinforced during the current yearly update.

Historical exposure alone can never trigger assimilation.

## 8.2 Strong exposure threshold

Very low exposure no longer receives even a small yearly assimilation roll.

The 1.2 behaviour where a score of 5 can already trigger a 1% roll is removed for the multi-exposure model.

Initial implementation target:

- minimum Cultural exposure score for assimilation eligibility: 60.

This value is a balancing baseline and can be changed after tests.

## 8.3 Sustained exposure

A target must have been continuously reinforced for several years before it becomes eligible.

Initial implementation target:

- at least 3 consecutive yearly updates with active exposure.

The exposure score may survive interruptions, but the assimilation streak does not.

## 8.4 One candidate only

A character never rolls independently for every exposed Culture during the same birthday.

Only the strongest eligible foreign Culture may become the assimilation candidate.

## 8.5 Clear lead requirement

Accumulated exposure and current environmental pressure are evaluated separately.

The leading foreign Culture must:

- have at least 60 accumulated exposure;
- have at least 25% more current annual Cultural pressure than the character's current Culture;
- remain at least 10 accumulated exposure points above the second strongest eligible foreign Culture.

This avoids a saturation problem where a current Culture already at 100 exposure could otherwise become mathematically impossible to replace, even when almost the entire present environment has changed.

Parents who retain the current Culture therefore continue to resist assimilation through both active Cultural pressure and the separate parental probability modifier, but never grant complete immunity.

If two strong foreign environments are competing closely, the character remains culturally stable rather than randomly alternating identities.

## 8.6 Assimilation cooldown

After an actual Cultural change, automatic Cultural assimilation is disabled for a period.

Initial implementation target:

- 5 years.

Exposure continues to accumulate and decay during the cooldown.

The cooldown blocks only another automatic Culture change.

This preserves the character's lived history while preventing rapid A -> B -> C -> A switching.

## 8.7 Parent resistance

Living parents who still represent the character's current Culture reduce the final assimilation probability.

Initial balancing target:

- one matching living parent: noticeable reduction;
- two matching living parents: stronger cumulative reduction;
- never a complete block.

## 8.8 Adults

Adult cultural exposure is tracked.

Exposure alone does not automatically change an adult's Culture.

Adult exposure can later support events, decisions, hybridization logic and Story Cycle information without turning travel into automatic culture switching.

---

# 9. Religious exposure

Faith and Rite retain the hierarchy established in 1.2:

- if the Faith differs, Faith exposure is relevant;
- if the Faith is the same but the Rite differs, Rite exposure is relevant;
- a foreign Faith conversion necessarily adopts a Rite belonging to that Faith;
- Rite exposure must never independently accelerate conversion to a different Faith.

The multi-track system extends this logic so that several Faiths or several valid Rites can be remembered simultaneously.

Religious exposure also receives decay and anti-churn protection.

Exact conversion thresholds may remain distinct from Cultural thresholds because changing Rite, changing Faith and changing Culture do not have the same narrative weight.

---

# 10. Adventurer-specific location resolution

The 1.2 logic often assumes:

court_owner -> capital_province

This is insufficient for a playable landless Adventurer who can effectively be their own Court Owner.

For a Landless Adventurer:

- resolve the active Domicile/Camp location;
- use the County containing that location as the territorial environment;
- use Camp/Court members for the 33% social-demographic calculation.

For ordinary characters:

- use the Court's actual local environment as before, with County Culture applying universally.

The implementation should use a shared resolver so downstream exposure logic does not need separate duplicated Adventurer and landed systems.

---

# 11. Story Cycle foundation

The later 1.2.2 Foreign Education Story Cycle will expose this information for:

- the player character;
- the player's non-adult descendants.

The UI/narrative layer should be able to distinguish:

- current identity;
- active exposure;
- fading exposure;
- relative exposure strength;
- currently reinforcing sources.

1.2.1 therefore needs persistent data that can be read later without redesigning the exposure backend.

---

# 12. Legacy 1.2 migration

1.2 currently stores one target per domain:

- nu_culture_exposure_target;
- nu_rite_exposure_target;
- nu_belief_exposure_target;

with one score/year/floor set per domain.

1.2.1 replaces this single-target architecture with multiple tracks.

Migration must be save-safe:

- if a legacy target exists on first 1.2.1 update, import it into a new exposure slot;
- preserve its current score and years where possible;
- remove the legacy variables only after successful migration;
- never duplicate the same target into more than one slot.

---

# 13. Implementation strategy

Because CK3 variable lists can store target scopes but do not conveniently associate a separate numeric score with every list entry, the first implementation should use a bounded set of parameterized exposure slots.

Target baseline:

- up to 8 simultaneous tracks per domain.

Eight tracks are deliberately above the number normally produced by the approved source model while remaining deterministic, debuggable and save-friendly.

If all slots are occupied, new negligible influences should not evict a mature exposure track.

Slot helpers should be parameterized so the implementation remains maintainable rather than duplicating full logic eight times.

---

# 14. Initial balancing targets

These numbers are implementation baselines, not final release guarantees.

Suggested relative Cultural source strengths:

- Guardian: strong;
- Parent: medium/strong;
- dominant Court/Camp Culture: strong;
- County Culture: weak direct gain + percentage synergy with matching sources.

Suggested Cultural proximity bonuses:

- shared Heritage: moderate;
- shared cultural language: moderate;
- target language known: moderate/strong;
- combined multiplier capped.

Suggested decay:

- clearly faster than a weak County-only gain;
- slow enough for several years abroad to leave a meaningful fading memory;
- no permanent exposure floor.

All exact values must be tested in long-form campaigns rather than validated only through forced debug exposure.

---

# 15. Required test cases

At minimum:

1. Norse Asatru infant Adventurer raised for many years in a heavily Cisalpine Christian Camp in Venice.
2. Same case with two living Norse parents.
3. Same case with one Norse parent and one Cisalpine parent.
4. Foreign Guardian but home Court and home County.
5. Home Guardian but foreign dominant Court and foreign County.
6. Foreign County only.
7. Two foreign Cultures both above 33% in the same Court/Camp.
8. Three Cultures around the 33% threshold.
9. Move from Culture B environment to Culture C environment after several years.
10. Return to the original Culture after a recent assimilation and verify cooldown.
11. Adult moves repeatedly through foreign Counties and accumulates exposure without automatic Culture changes.
12. Shared Heritage vs unrelated Heritage.
13. Shared language vs unrelated language.
14. Learned target language.
15. Faith-different environment.
16. Same Faith but different Rite.
17. Multiple competing Faith/Rite exposures.
18. Existing 1.2 save containing legacy single-target exposure variables.

The primary acceptance criterion is not merely that assimilation can happen.

It is that sustained upbringing produces plausible identity changes while ordinary travel and mixed environments do not create a culture-switching carousel.


---

# 16. First implementation pass status

The first 1.2.1 coding pass is complete and is awaiting in-game validation.

## Implemented - requires in-game validation

- [Implemented] Cultural exposure begins at birth with the 100-point birth profile.
- [Implemented] Current Culture is stored as a real exposure track rather than existing outside the exposure system.
- [Implemented] Up to eight simultaneous Culture exposure tracks.
- [Implemented] Up to eight simultaneous Faith exposure tracks.
- [Implemented] Up to eight simultaneous Rite exposure tracks.
- [Implemented] Independent exposure scores, total years, uninterrupted streaks and decay.
- [Implemented] Current annual Cultural pressure, distinct from accumulated Cultural familiarity.
- [Implemented] Parents as direct influences.
- [Implemented] Guardian as a strong direct influence.
- [Implemented] Court/Camp demographic influences with the 33% dominance threshold.
- [Implemented] The subject is excluded from their own Court/Camp demographic calculation.
- [Implemented] County Culture/Faith/Rite using the character's actual County.
- [Implemented] Adventurer support through Domicile/Camp location.
- [Implemented] Liege Culture as a weak political influence.
- [Implemented] Councillor Cultures as weak secondary influences.
- [Implemented] Shared Heritage modifier.
- [Implemented] Shared cultural language modifier.
- [Implemented] Learned target-language modifier.
- [Implemented] County synergy with matching non-County Cultural sources.
- [Implemented] Cultural decay without permanent 1.2 exposure floors.
- [Implemented] Faith/Rite decay without permanent exposure floors.
- [Implemented] Adult exposure while blocking automatic adult assimilation.
- [Implemented] No automatic assimilation before age 4.
- [Implemented] Cultural anti-churn gate: score, streak, current pressure, competing exposure and cooldown.
- [Implemented] Separate Faith and Rite assimilation thresholds/cooldowns.
- [Implemented] Parental resistance to Culture/Faith/Rite assimilation without immunity.
- [Implemented] Migration from 1.2 single-target exposure variables.
- [Implemented] Compatibility view for 1.2 events, homesickness, notifications and assimilation context.
- [Implemented] Existing education-event exposure changes are routed into persistent multi-exposure tracks.
- [Implemented] Debug inspector for all Culture/Faith/Rite tracks.
- [Implemented] Generalized debug annual-exposure tick for infants, Adventurers and adults.

## Current balancing baselines

These values are explicitly provisional until normal and forced in-game tests are complete.

- Cultural automatic-assimilation minimum: 60 accumulated exposure.
- Cultural uninterrupted active streak: 3 years.
- Cultural current-pressure lead: target pressure >= 125% of current-Culture pressure.
- Cultural lead over second foreign Culture: 10 accumulated points.
- Cultural cooldown after an actual change: 5 years.
- Faith automatic-assimilation minimum: 60.
- Faith uninterrupted streak: 3 years.
- Faith cooldown: 5 years.
- Rite automatic-assimilation minimum: 45.
- Rite uninterrupted streak: 2 years.
- Rite cooldown: 3 years.
- Exposure decay when unsupported: 8 points per yearly update.

## Validation rule

Do not consider these systems release-validated from static inspection alone.

The branch must be tested in CK3 with the dedicated 1.2.1 test plan before balancing values or changelog wording are finalized.
