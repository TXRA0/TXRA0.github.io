---
title: "Skirmishers: How to Make Them and Why They Are Supreme"
date: 2026-10-30 12:00:00 +0000
categories:
  - bot-design
  - research
tags:
  - screeps
  - combat
  - skirmishers
  - combat-ai
excerpt: "Exploring the design, mechanics and tactical advantages of skirmisher creeps in Screeps."
---
## Why Are Skirmishers So Important?

Skirmishers are already an important part of Screeps combat, and are becoming an increasingly discussed topic with the introduction of the new Terminal Node update.#

They are utilised in 4 main categories:
- Harassment -> the attacking of enemy remote mining to kill miners/haulers/reservers, disrupting their economy and denying their access to sources
- Non formation room assaulting -> utilising creeps with normally built with RANGED_ATTACK or HEAL parts assaulting a room with a low tower count (or none at all)
- Resource / competition objective denial -> fighting over valuable resources (e.g. power/deposit mining and SK mineral harvesting) or disrupting someones ability to gain score in a competition setting (e.g. attacking peoples Thorium reactors in the most recent season to make it more difficult/unable to score)
- Terminal nodes (future update) -> destroying enemy terminal nodes to limit the energy flow into rooms with terminals (making room assaults easier)

## A Basic Skirmisher Design

Most "beginner" skirmishers utilise a very much simple design. Despite its simplicity, the design can be quite difficult to expand on, and not very effective in high stakes combat situations. This basic logic could be something like

if (health < 0.8) {
    fleeFrom(enemy);
} else {
    moveTo(enemy);
}
rangedAttack(enemy);
heal(skirmisher);

This is where i introduce a model that my skirmishers use: **ferocity**
Ferocity is a very general number that represents a fundamental question: "Should we pursue the enemy, or flee from them?". It is very easy to make a simple ferocity calculator. Using the example we had earlier, we could make a calculator that functions like this

if (health < 0.8) {
	ferocity = -1
} else {
	ferocity = 1
}

if (ferocity > 0) {
	moveTo(enemy)
} else {
	fleeFrom(enemy)
}
rangedAttack(enemy);
heal(skirmisher);

Although the example here is very basic, it is super simple to expand on, and introcues an important concept: seperating the *decision making process from the actions themselves*. Instead of directly telling the skirmisher when to move towards or away from an enemy, we calculate a value that determines the behaviour of it.

My current ferocity calculator is over 500 lines long, and takes into account
- the creep itself
- its friendly creeps inside the room
- the enemy creeps in the room
- the friendly/enemy towers in the room

## To Improve On It

There are many ways to improve on this simple calculator example. Here are some of the best ways to add onto it:
- 1: Taking into account our local strength vs the enemies local strength. My calculator will increase the ferocity by a scale based on our strength, thats capped at 4 addition, and the same goes for if our strength is lower than the enemies, reducing it up to 4
- 2: Different ranges for different ferocities. After calculating, my skirmisher will use a range to ferocity scale, that differs from range 0 if ferocity is very high to range fleeing up to 7 and pulling away
- 3: Forming up. If our strength is below 1.6 of the enemies strength total then my skirmishers will form up in a group to fight
- 4: A function to apply healing to all creeps in a room. I havea a applyRoomHeal function that will calculate what creeps should receive healing priority, when a creep will heal another vs itself, and when to ranged heal vs ranged attack an enemy

## The Future Of These Blogs
I had a great time writing this blog, and getting to share my combat knowledge with other players. I hope to write one of these a month (likely multiple this month as i've just started), and hope to have lots of people reading these!
Thanks for reading! 