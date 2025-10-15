1) Game must know the board that the race will take place on
	a) For now, we'll focus on building out just the Mild Mile (i.e. the Game will choose 1 board from a total of 1 possible boards)
	b) In the future, I'll work on building out the Wild Wilds
		- This board is more complex, because events happen when a racer lands on specific spaces

2) Game must know the racers in play
	a) There can only be one of each type of racer in a given race (36 total racers)

3) Game must know the turn order
	a) Game will establish turn order before the first round starts (i.e. assign order randomly)
	b) Game must be able to update turn order to exclude 1st place racer

4) Game must know the round number
	a) Game will count rounds starting from 1
	b) A round will end when every racer in play has finished a turn since the the start of the round
		- Note the Skipper

5) Game must know player positions
	a) Player positions will always start at 0
	b) Game will be responsible for updating player positions as a response to various events, modifiers, etc.
	c) Game must track past and current positions (at least the previous position is needed, but maybe more is required too?)

6) Game must know whenever specific events and/or conditions take place:
	a) Roll Die: when a racer rolls 1d6 at the start of their turn
		- Some racers can opt to do something instead of rolling the die on their turn
		- If you have some reason to re-roll a die (e.g. the Dice Monger, the Magician), only the final value affects the board state (i.e. it cannot trigger powers)
		- If you have some reason to re-roll a die, you can only re-roll the most recent die you've rolled (e.g. you cannot save a die value and choose it)

	b) Main Move: the primary action that racers take at the start of their respective turns
		- Normally, a racer moves the number of spaces shown on the die after the Roll Die event
		- Sometimes a racer's Main Move is modified by the effects of other racers
		- Sometimes a racer's Main Move is replaced by a special event

	c) Ahead: racer A is ahead of racer B if (racer_A.position > racer_B.position)

	d) Behind: racer A is behind racer B if (racer_A.position < racer_B.position)

	e) Alone: a racer is Alone if its position value is not shared with any other racer

	f) Last Place: a racer is in Last Place if it has the lowest position value in the game
		- can be tied for last place with any number of racers

	g) Lead: a racer is in the Lead if it has the highest position value in the game
		- can be for the lead with any number of racers

	h) Move: generally, when a racer's position changes, this counts as moving
		- If a power causes your racer to move, it must explicitly say "Move" in the description!
		- If you move 0, you did not move
			- See "Warp"

	i) Passing: racer A passes racer B if before moving, (racer_A.position < racer_B.position) and after moving (racer_A.position > racer_B.position)

	j) Sharing a Space: racer A shares a space with racer B if (racer_A.position == racer_B.position) while both are stopped (i.e. racers do not share a space if one of them is in the middle of moving, warping, etc.)
		- racers can share a space with any number of racers
			- Game must be able to determine the number of racers on a given space.
		- See "Stopping on a Space"

	k) Stopping on a Space: a racer is considered stopped on a space after it has finished moving onto that space (i.e. a racer is not considered to have stopped on a space if it is in the middle of moving, warping, etc.)
		- powers that trigger when two racers stop on the same space will activate if both racers move at the same time

	l) Trip: when a racer trips, it loses its next main move
		- while Tripped, at the start of your turn, you will un-trip yourself instead of rolling your die and/or performing your Main Move
		- while Tripped, your powers may still activate

	m) Warp: when a racer warps, its position value is instantly updated without emitting signals for things like Passing, Stopping, etc.
	
	n) Activate power: racers each have their own unique powers that activate conditionally
		- Most powers activate automatically
		- Some powers activate at the player's discretion!
			- Must have an algorithm handy to appropriately determine when to activate a power
		- Racer powers that happen at a specific time only happen once
		- A racer's power deactivates after it wins (unless stated otherwise)
		- If you run into a true infinite loop, resolve the interaction one time and move on
			- Probably have to make exceptions for this (e.g. Skoocher + Huge Baby)
		- If you run into a wacky, extended loop, let it happen! (e.g. Skoocher + Suckerfish)

7) Game must know when a race has ended
	a) The race is over when one of the following takes place:
		- two racers have crossed the finish line (position >= 30)
		- there are no racers left on the track (i.e. in the unlikely scenario that M.O.U.T.H. eats all other racers, the game would end with just a first place racer)


