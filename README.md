# Biquadris

## Description

Biquadris is the two-player version of the video game Tetris.

A game of Biquadris consists of two boards, each 11 coloumns wide and 15 rows high. Blocks appear at the top of each board, and each player must drop their block onto their respective board so as not to leave any gaps. Once an entire row has been filled, it dissapears, and the blocks aboe move down by one unit. 

Biquadris differs from Tetris in one significant way: it is not real-time. Players have as much time as they want to decide
where to place a block. Players will take turns dropping blocks, one at a time. A player’s turn ends when he/she has dropped
a block onto the board (unless this triggers a special action; see below).

![](https://allenwu.ca/img/Biquadris%20(2).PNG.jpg)

## Development

The game of Biquadris was built with the intention of low coupling and high cohesion, as well as resilience to change and addition of new features.

### Factory Design Pattern

The factory design pattern was implemented in the Level classes because a single Level instance is needed per player at a time, thus the family of algorithms associated with levels can be interchanged as needed. This design allows for the addition of an arbitrary amount of levels, where each new level can be added without affecting existing code.

### Strategy Design Pattern

The Level classes support the possibility of various changes to the program specification because the strategy design pattern allows for adequate separation of methods to keep each LevelX class low in
coupling. Each level chooses a different means of producing a block with different properties(the difference in properties means this is partially also a use of the factory design pattern as properties such as heaviness and value depend on the level). Here, the addition/removal of levels does not affect the other level implementations.

### Observer Design Pattern

Each cell within the grid acted as a subject, that contains a list of it's adjacent cells. As a result, whenever a block is dropped or deleted every cell adjacent to it is notified.

# Game Setup

### Blocks
Similar to Tetris there are S, Z, L, J, I, T and O blocks

![](https://static.wikia.nocookie.net/tetrisconcept/images/c/ca/Tetromino_image.png/revision/latest/scale-to-width-down/360?cb=20090706171943)

### User Commands

All movement commands are to be input using the keyboard within the terminal. A short list of available commands are seen below

* **left** moves the current block one cell to the left. If this is not possible (left edge of the board, or block in the way), the command has no effect.
* **right** as above, but to the right
* **down** as above, but one cell downward.
* **clockwise** rotates the block 90 degrees clockwise, as described earlier
* **counterclockwise** as above, but counterclockwise.
* **drop** drops the current block as far down as possible. Even if a block is already as far down as it can go (as a result of executing the down command), it still needs to be dropped in order to get the next block
* **levelup** increases the difficulty level of the game by one. The block showing as next still comes next, but subsequent blocks are generated using the new level
* **leveldown** same as above by decreases the difficulty level of the game by one
* **restart** clears the board and starts a new game.

### Scoring

When a line (or multiple lines) is cleared, you score points equal to (your current level, plus number of lines) squared. (For example, clearing a line in level 2 is worth 9 points.) In addition, when a block is completely removed from the screen (i.e., when all of its cells have disappeared) you score points equal to the level you were in when the block was generated, plus one, squared. (For example if you got an O-block while on level 0, and cleared the O-block in level 3, you get 1 point.)

### Levels

There are 5 levels, each of which score different number of points, and provide different challenges.

* **Level 0** : This is the starting level, and is the only level in the game that doesn't have randomness. All of the blocks are predetermined based on a starting file called sequence1.txt and sequence2.txt
* **Level 1** : This is the first level to introduce randomness, but the probabilities are skewed such that S and Z blocks are selected with probability 1/12 each, and the other blocks are selected with probability 1/6 each
* **Level 2** : Each block is selected with the equal probabilty
* **Level 3** : This is the first level where certain challenges start to come forward for the players. In all previous levels, the block would only move down, or drop when the user wanted it to. In this level every block is "heavy" and every command to move or rotate the block will be followed immediately and automatically by a downward move of one row. In addition S and Z blocks are selected with probability 2/9 each, and all other blocks are selected with probability 1/9
* **Level 4** : This is the last level in the game, which incorporates ever rule as seen in Level 3, but ever time you place 5 (and also 10, 15, etc.) blocks without clearing at least one row, a 1x1 block is dropped onto your game board in the centre column. An example of the 1x1 block can be seen below as a maroon block


### Special Actions

If a player, upon dropping a block, clears two or more rows simultaneously, a special action is triggered. A special action is a negative influence on the opponent’s game. When a special action is triggered, the game will prompt the player for his/her chosen action. Available actions are as follows:

1. **Blind** : The player’s board, from columns 3-9, and from rows 3-12, is covered with question marks (?), until the player drops a block; then the display reverts to normal
2. **Heavy** : Every time a player moves a block left or right, the block automatically falls by two rows, after the horizontal move
3. **Force** : Change the opponent’s current block to be one of the player’s choosing. If the block cannot be placed in its initial position, the opponent loses.
