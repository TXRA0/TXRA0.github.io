---
title: "Combat Spawning: Why Attack Creep Mixes Are Valuable"
date: 2026-10-30 12:00:00 +0000
categories:
  - bot-design
  - research
tags:
  - screeps
  - combat
  - skirmishers
  - combat-ai
  - spawning
excerpt: "Going in-depth into combat spawning, and why attack creeps are the best"
---

In my last blog, I talked about how you can make an amazing skirmisher architecture that is easy to expand onto. In this blog, i will talk about what creeps we should spawn against an enemy threat, and why creeps with ATTACK parts are super valuable

## My Journey Into Spawning

In the older versions of my bot (around June 2026 time), my bot had a super simple spawner for remote defense. It looked something like this:

```pseudocode
	enemyStrength += enemyAttackPower
	enemyStrength += enemyRangedPower
	enemyStrength += enemyHealPower

	friendlyStrength += friendlyAttackPower
	friendlyStrength += friendlyRangedPower
	friendlyStrength += friendlyHealPower

	while friendStrength < enemyStrength * 1.2:
		body = findBlinkyBody()
		addToQueue("blinky", body)
```
This was fine, up until i started fighting actually capable players (Shu in season 10). The main issue here was that the enemy could have hugely more ranged power than heal power, but because the enemy strength was built up to all of their power, it would still spawn the same biggest hardcoded blinky body and not take into account that we don't have enough heal. This is where i came up with a spawning system that utilises **heuristics**

## Heuristics, The Spawning Solver

I derived a system of generating what different parts (ATTACK, RANGED_ATTACK, HEAL) and the amount we need to spawn for a certain scenario (e.g. Invaders in my remote that have 5 HEAL parts, 5 ATTACK parts, and 3 RANGED_ATTACK parts). This system uses values that i've tweaked to work the best. The overview of it is like this:

```pseudocode
	healNeeded = calculateHealingRequirements(enemyComposition)
	rangedNeeded = calculateRangedRequirements(enemyComposition) <- this uses a heuristic
	attackNeeded = calculateAttackRequirements(enemyComposition) <- this uses a heuristic

	applyEnemyDurabilityAdjustments()

	if Invasion:
		adjustRequirementsForInvasion()

	if difficultOpponent:
		applyMatchupAdjustments()

	if tooMuchNeeded:
		dontSpawn()
```
The main advantage of this system is that it can adapt to the enemy having alot of HEAL/RANGED_ATTACK parts. In my simple system from earlier, this wasn't the case. This now allows spawning to be adaptive to the enemy, instead of chucking out the same composition every time. 

## Why ATTACK parts are so valuable

From testing in many different scenarios, i found that utilising a mix of creeps with RANGED_ATTACK/HEAL, just HEAL, and just ATTACK was much more effective than utilising ONLY creeps with RANGED_ATTACK/HEAL.
The reasons for this are here:
- 1, ATTACK breaks systems like my simple example. ATTACK parts have 30 ATTACK power per part, compared to just 10 for RANGED_ATTACK and 12 for HEAL. In my old system, players/Invaders attacking my remotes with ATTACK parts would cause it to freak out and spawn a huge amount of blinkies, which was incredibly excessive
- 2, Pushing the enemy away. If a enemy managed to get into range 1 of a creep thats part of a large group (common with skirmishers), then they could use rangedMassAttack(), which would cause devastating amounts of damage to our skirmishers. With a creep that has ATTACK parts near the front of the group, this will punish enemies trying to come range 1 of the front of our group (remember, each ATTACK part deals 30 damage). 
- 3, Cheaper costs for low extension count spawning rooms. Each RANGED_ATTACK part costs 150 energy, which can add up alot for rooms that have a low extension count. However, ATTACK parts cost only 80 energy, meaning you can fit more on creeps when you are low on energyCapacity.

## Next blog
Next blog, I will go deeper into combat, and likely start talking about simple mission workflows. Please tell me if you have any specific requests!
❤️