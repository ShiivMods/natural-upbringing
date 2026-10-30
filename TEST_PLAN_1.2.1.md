# Natural Upbringing 1.2.1 - Exposure Rework Test Plan

This document is the first in-game validation checklist for the 1.2.1 exposure overhaul.

The goal is not only to prove that assimilation can occur. The main goal is to verify that exposure behaves plausibly without creating rapid Culture/Faith/Rite switching.

Use the debug exposure inspector and the generalized annual-exposure tick whenever a natural multi-year test would be unnecessarily slow.

---

# A. Smoke test

Before testing balance:

1. Launch a save with the 1.2.1 branch.
2. Confirm guardianship interactions still work.
3. Open the NU debug inspector on a child already present in the save.
4. Force one annual exposure update.
5. Confirm Culture/Faith/Rite tracks appear without script-visible errors.
6. Advance at least one natural birthday and confirm the same character updates normally.

Expected result:

- no broken event chain;
- no duplicate assimilation notification;
- no immediate Culture/Faith/Rite change merely from loading the save;
- existing 1.2 exposure is migrated rather than discarded.

---

# B. Birth profile

Create or observe newborns in controlled cultural households.

## B1. Norse / Norse / Norse environment

Setup:

- child Culture: Norse;
- both parents: Norse;
- social Court/Camp environment: Norse.

Expected birth profile:

- Norse: 100.

## B2. Norse / French parents / Norse environment

Setup:

- child Culture: Norse;
- parent A: Norse;
- parent B: French;
- social environment: Norse.

Expected birth profile:

- Norse: 75;
- French: 25.

## B3. Norse / French parents / French environment

Setup:

- child Culture: Norse;
- parent A: Norse;
- parent B: French;
- social environment: French.

Expected birth profile:

- Norse: 50;
- French: 50.

## B4. Mixed dominant birth environment

Use a Court/Camp where two Cultures both meet the 33% threshold.

Expected:

- the social 25 points are split proportionally between the dominant Cultures;
- the child themself does not count toward Court/Camp demographics;
- total birth-share remains 100.

---

# C. Adventurer case - primary 1.2.1 scenario

Reproduce the motivating case as closely as practical:

- playable or close-family child;
- Culture Norse;
- Faith Asatru;
- very young;
- living in an Adventurer Camp located in a Cisalpine/Christian County such as Venice;
- Camp populated primarily by Cisalpine/Christian characters.

Check after repeated annual ticks:

- County Culture is Cisalpine through the Camp/Domicile location.
- The child does not count as a Norse member of their own Camp demographic.
- Cisalpine Culture gains exposure from Camp and County.
- Christian Faith exposure grows when the Faith differs.
- Rite is not simultaneously exposed while the Faith itself differs.
- Existing Norse exposure can remain but does not receive social support unless an actual Norse source exists.

Repeat with:

1. no living Norse parent;
2. one living Norse parent;
3. two living Norse parents.

Expected:

- parents noticeably slow assimilation;
- they do not make assimilation mathematically impossible;
- foreign Cultural pressure can eventually dominate when the rest of the lived environment is sufficiently strong.

---

# D. Court/Camp 33% threshold

## D1. Two dominant Cultures

Example:

- Culture A: 45%;
- Culture B: 35%;
- Culture C: 20%.

Expected:

- A and B reinforce exposure;
- C does not receive passive Court/Camp exposure.

## D2. Three-way edge case

Build a population close to one-third each.

Expected:

- every Culture actually reaching the threshold can reinforce exposure;
- no Culture below the threshold does;
- the inspected character is excluded from the denominator.

## D3. Competing strong foreign Cultures

Keep two foreign exposures close in accumulated score.

Expected:

- neither should trigger Cultural assimilation while the leading foreign Culture lacks the required 10-point lead.

---

# E. County influence

## E1. County only

Place a character in a foreign County while keeping parents/guardian/Court aligned with the current Culture.

Expected:

- foreign County exposure grows slowly;
- County alone should not overwhelm a strongly coherent household quickly.

## E2. Matching County + guardian/Court

Make the County Culture match a foreign guardian or dominant Court/Camp Culture.

Expected:

- the non-County source receives the County synergy bonus;
- the County direct source is not multiplied by its own synergy;
- integration is clearly faster than in E1.

---

# F. Cultural proximity and language

Compare otherwise identical exposure setups.

1. unrelated Heritage/language;
2. shared Heritage;
3. shared cultural language;
4. learned target language;
5. combinations of the above.

Expected:

- each approved similarity accelerates foreign Cultural exposure;
- combined proximity never exceeds the configured cap;
- current Culture exposure is not artificially accelerated by these foreign-integration modifiers.

---

# G. Decay

Build a meaningful exposure to Culture B, then completely remove all B sources.

Expected after yearly updates:

- B loses 8 accumulated points per unsupported year;
- B uninterrupted streak immediately resets to 0;
- B cannot trigger delayed assimilation while unsupported;
- the track disappears at zero.

Then reintroduce B.

Expected:

- surviving accumulated familiarity can resume from its remaining score;
- uninterrupted assimilation streak restarts from the new period of active exposure.

---

# H. Cultural anti-churn

## H1. Current Culture strongly supported

Maintain strong support for the character's current Culture while also exposing them to another Culture.

Expected:

- high foreign accumulated score alone is insufficient;
- foreign current annual pressure must exceed current-Culture pressure by the configured margin.

## H2. Actual assimilation

Create a valid foreign candidate:

- minor age >=4;
- score >=60;
- streak >=3;
- strongest current pressure;
- 10-point lead over second foreign Culture.

Expected:

- only one Culture can be rolled as the candidate on that birthday.

## H3. Post-assimilation cooldown

After a successful Culture change, move immediately into another strongly foreign environment.

Expected:

- exposure continues to update;
- no automatic second Culture change for 5 years.

---

# I. Adults

Inspect an adult repeatedly while moving through foreign Counties/Courts.

Expected:

- Culture/Faith/Rite exposure can accumulate and decay;
- no automatic Culture/Faith/Rite assimilation occurs from the exposure system alone.

---

# J. Faith and Rite

## J1. Different Faith

Place an Asatru character in a Christian environment.

Expected:

- Faith exposure progresses;
- Rite exposure from that same source does not progress separately.

## J2. Same Faith, different Rite

Use two characters sharing the same Faith but different Rites.

Expected:

- no foreign-Faith exposure from that source;
- Rite exposure progresses.

## J3. Several dominant Faiths

Use a Court/Camp where multiple Faiths meet the 33% threshold.

Expected:

- multiple Faith exposure tracks can coexist.

## J4. Several Rites of current Faith

Use a Court/Camp where multiple Rites within the character's current Faith meet the 33% threshold among members of that Faith.

Expected:

- valid Rites can coexist as exposure tracks;
- Rite denominator is the relevant Faith population, not the whole Court/Camp.

## J5. Conversion safeguards

Expected:

- Faith requires score >=60 and streak >=3;
- Rite requires score >=45 and streak >=2;
- parent resistance reduces probability without creating immunity;
- cooldowns prevent immediate repeated changes.

---

# K. 1.2 compatibility / save migration

Load a save created with NU 1.2 containing an existing Culture/Faith/Rite exposure.

Expected on first 1.2.1 update:

- old exposure is imported into a persistent slot;
- score and years are preserved where available;
- current Culture receives a stable baseline if necessary;
- old compatibility variables are rebuilt from the active multi-track state;
- homesickness, notifications and existing 1.2 education events continue to function.

---

# L. Pass criteria for the first campaign

The first implementation pass is considered technically validated only when:

- birth profiles are correct;
- Adventurer County/Camp detection works;
- several exposures coexist;
- unsupported exposure decays;
- Court/Camp 33% logic behaves correctly;
- root is excluded from its own demographics;
- language/Heritage modifiers work;
- adults never auto-assimilate;
- Faith-vs-Rite hierarchy remains correct;
- no rapid Culture/Faith/Rite carousel is observed;
- old 1.2 saves migrate without breaking dependent systems.

Balance values can then be adjusted from observed campaign behaviour rather than from debug-only intuition.
