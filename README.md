# IS590PZ 2020 Spring Student Projects

## FINAL PROJECT: NINE MEN'S MORRIS AI PLAYER

### About the Game
* It is a two player strategy board game that dates back to the Roman Empire
* The board consists of a grid with 24 intersection points
* At the start of the game, each player is given 9 pieces 
* A mills is having 3 same pieces aligned horizontally or vertically
* Forming a mill, allows us to eliminate opponent’s piece from the board
* Aim of the game is to reduce opponents pieces to two so they can no longer form a mill
* An empty game board looks like [this](https://cdn.printablepaper.net/samples/Morris_Nine_Men.png)

### Game Rules
Game is divided into 2 phases:
* PHASE I: Placing pieces
Each player takes turns placing their 9 pieces on the empty slots of the board
If a player is able to form a mill, they can remove one of opponent's piece that is not part of a mill

* PHASE II: Moving pieces
Each player takes turns to move their piece to an adjacent slot (diagonal moves are not allowed) to form mills 

### Variation from existing game
* In the second phase, if a player forms a mill, in the next turn they are allowed to move to any empty slot on the board

* Players may remove pieces that even part of a mill

### Game Implementation

I implemented an interactive game in Python 3.2 using a list of lists (two-dimensional array). Each player is given nine beads at the start of the game. The game randomly selects one player i.e., either the computer or the human player to play first. The human player is allotted as player ‘1’ and the machine is allotted as player ‘2’. I chose alpahbets from A-X to denote the 24 empty slots.

In phase-I of the game, a player chooses to input his move by choosing one of the empty alphabets to place a bead on the board. The game works in phase I, till a player uses all the 9 beads. A player’s bead is indicated on the board by replacing the alphabet with ‘1’ for a human player and ‘2’ for the machine. While placing the beads, if a player forms a mill i.e., three of a player’s beads are placed either horizontally or vertically, the player may choose to remove one of the opponent’s beads. Being a variant of the original game, players may remove an opponent’s bead even if it is part of a mill. Every move played by each player is stored in a nested dictionary along with the phase in which the move was played, wins(mill formations), looses(opponent’s mill formations) that arose because of the move, and the player(1 or 2) of the move. 

After the 9 beads of either player are played, we enter into the second phase of the game. Here, a player may only move his bead to an adjacent slot either horizontally or vertically. A player chooses to input his move by entering two alphabets which denote the position from which a bead moves to another position. For example, ‘AB’ indicate the movement of a bead from position ‘A’ to position ‘B’. During this process, if a player successfully forms a mill i.e., three of a player’s beads are placed either horizontally or vertically, the player may choose to remove one of the opponent’s beads. As a variant of the original game and to make it fun, after a player removes one of the opponent’s beads, just for the next move he can place the bead anywhere and does not need to adhere to the adjacency move criteria. 

A game is won if:
1. The opponent is left with just 2 beads, making it impossible to form a mill
2. A player cannot move to an empty slot because of being surrounded by opponent’s beads

How does the AI work?
When the first game is played, the machine records all the moves that occurred during the game.

A typical move consists of:
1. the move played
2. player who played the move
3. wins (initialized to 0)
4. losses (initialized to 0)
5. phase (1, 2 or 3; Here, Phase-3 indicates when an opponents bead is removed)

Whenever a human player forms a mill, the key ‘losses’ of all the moves that lead to the formation of a mill is incremented by 1.  Likewise, when the machine forms a mill, the key ‘wins’ of all the moves that lead to the formation of a mill is incremented by 1. When the machine comes across a move that is already memorized, it plays the move that has a high ‘wins’ count. If the ‘wins’ count is 0, the machine chooses to randomly generate the next move.

I chose a list of lists (2D array) to implement the board because of the ease of retrieving the beads at any given combination of row and column. I chose a nested dictionary to implement the played moves because of it’s constant retrieval time.
