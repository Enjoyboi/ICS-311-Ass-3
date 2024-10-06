# ICS-311-Ass-3
This week’s assignment asks for three (3) people to work on an assignment inspired by a game. An editable Google sheet for choosing your own group has been shared with you already (if you didn't receive the sharing notification, check your junk mail then contact the instructor). Turn in your assignment by posting here in Laulima a link to your Google Document. It should be shared as Editable with the instructor and TA (dbconner,lcdavis9, jans26, qianyang). We will not edit your documents, but this lets us confirm who made which edits.

You do not need to implement your assignment, but you do need to prove the effectiveness of your approach.

Each author of the trio can receive up to thirty five (35) points, distributed as follows:

10 points: Appropriate choices of algorithms and data structures. If you choose something with bad running time when something better is available, you will not score well on this part. 
20 points: The explanation and proof of why your choices are good ones. If you can’t prove that your choices are good ones, you will not score well. If you didn’t choose the best algorithm, but still explain clearly what it does do well, you can still score well here.
5 points: The professionalism of the writing and presentation. This includes appropriate citations (the textbook, Wikipedia pages, etc.)
The game is a war game, with two competing sides. Each player must choose an assortment of pieces, where each piece has different strengths and weaknesses. This forms their army. Each piece, or unit in the army, also has an associated point cost, and players must choose their units within an agreed point budget for a particular game.

Inspiration
The game in this assignment is a simplified version of army building in the game Warhammer 40,000 (see warhammer40000.com for much more, and games-workshop.com for miniature soldiers that can be bought, assembled, and painted to play on a tabletop). Warhammer 40k is a dark and satiric look at the galaxy of the 40th millennium, when even the “good guys” defending humanity are deeply evil and everyone else is worse. War spans the galaxy from one end to the other.

Each player chooses a codex, a collection of possible units to use in their army. Different codices support different play styles and different esthetics, from armored, genetically engineered superhumans to demonic incursions from beyond space-time to giant robots to world-devouring psychic monsters.

You don’t need to be familiar with this game to do this assignment, and it requires no specific knowledge of the rules, or familiarity with the setting. It is a grim future, and you can ignore that for this assignment if you want to. You can easily think of buying an assortment of chess pieces instead (it just doesn’t come with the extensive backstory that Warhammer 40k does).

Choosing an Army
Your team must describe an algorithm to choose an army that will perform well for a given points budget. If you can demonstrate that the army is optimal, so much the better.

You are given a list of codices. Each codex consists of a list of possible units to include in the army. Each unit has the following information:

Speed. How many spaces per turn the unit can move.
Wounds. How many wounds the unit has, i.e., the number of times the unit can be hit before being removed from play.
Armor. The probability that a wound caused by the enemy is ignored (i.e., because of armor).
Shooting accuracy. The probability that the unit can cause damage at a distance (i.e., ranged fire, like guns).
Shooting damage. If that distance attack hits, how many wounds it will cause.
Close combat accuracy. The probability that the unit can cause damage when adjacent to an enemy unit (i.e., melee combat).
Close combat damage. If the melee attack hits, how many wounds it will cause.
Each unit in the codex has a point cost. While in the game that inspires this exercise, points are generally higher for tougher, stronger, more powerful units, your algorithm should not assume this. Each unit may have a maximum quantity that can be included in the army - for example, a very powerful leader may only be able to be included once, while elite units might have a limit of 3, and general rank and file might unlimited (similar to a standard chess set, where there is one queen, two knights, and eight pawns).

For example, a codex might have a fast unit with many wounds, good armor, and accurate and damaging weapons, all for a very small amount of points. This would be an obvious unit to take. In practice most units don’t work like that (and if they did, the game wouldn’t be fun, like playing chess against an opponent who used nothing but queens).

Your algorithm, when given a specific codex and a particular point limit, should produce an army that will perform well against other possible armies, including ones chosen from other codices.

Context: A Battleplan
Units will be placed on a battlefield, and take turns moving and fighting. Units that can control special locations, called objectives, on the board score points towards winning the game. If one army is completely destroyed, points don’t matter and the destroyed army loses.

A battlefield may be very large, or very small. It may have very few objectives, or very many.

So a slow army will do poorly on a large battlefield. A fast army may not be able to make use of its speed on a small battlefield. Similarly, if there are many objectives, an army with a small number of powerful units may be able to control a small number of objectives, but still lose to an army with many units, able to control more objectives.

You are not required to provide an algorithm that produces a battle plan for your army, but your algorithm for choosing an algorithm should be considering various victory conditions. If there are criteria that drive army selection, you should describe that. For instance, while you typically do not know the battlefield when selecting an army, your algorithm should be able to incorporate that information if it is available.

To address this, you may want to consider first a very simple battlefield, with only a single objective to control. That may assist you in thinking about a more general problem of ensuring an army is effective in general, or how to modify an army for a specific situation.

Deciding Battles
In the game by which this assignment is inspired, dice provide the probability of success in many things. This assignment is not about statistics, though, so you may assume the use of the following two functions to determine which unit would win in a battle between two units, and to determine which army would win in a battle between two armies. 

Combat(Unit A, Unit B, Distance) returns the result of a combat fought between Unit A and Unit B, at a specific distance. Note that the results can be different for different distances. For example, a unit with high shooting damage and low close combat damage is likely better at a greater distance than one with the reverse. You may assume that transitivity holds (though it doesn’t in the actual game) for a given distance. I.e., If A beats B, and B beats C, then A will beat C. Combat runs in O(1) time.
Battle(Army A, Army B, Battlefield F) returns whether Army A wins or Army B on a given Battlefield. Note that, as described in the section on the battle plan, different armies will fare differently on different fields. A slow army may do poorly on a very large field, especially if it is focused on close combat. A fast army may find a small battlefield too small for its speed to be put to effective use. As with Combat, you may assume transitivity holds (though again it does not in the actual game). If Army A beats Army B, and Army B beats Army C, then Army A will beat Army C. Battle runs in O(n) time, where n is the total of units in Army A and Army B (i.e., bigger battles with bigger armies take longer to play).
Neither of these functions consider the points costs for either the unit or the army. You can use them in your army building algorithm as part of determining the optimal army choice for a given codex. Remember that your algorithm is given a list of codices and a point budget to build to, so consider that aspect when analyzing the efficiency of your algorithm.

Food for Thought
Implementing an army builder like this can be done in many different ways. Depending on how you choose to tackle this problem, you may make use of divide and conquer, dynamic programming, or greedy algorithms. Sorting and balanced trees may have a place as well. While in the real world of playing Warhammer 40K, codices have a relatively small (typically less than fifty) different units, and there are a relatively small (perhaps thirty) number of codices, armies may get very large, with potentially hundreds of units (such large games are played over the length of a weekend). Don’t assume for your algorithm that the numbers will always remain small - there are exponential combinations in army building, and part of the assignment is to avoid those situations where possible (and if not possible, explain why).
