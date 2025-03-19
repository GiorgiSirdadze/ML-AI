# Minesweeper AI

## Functions Implemented

### 1. `add_knowledge(cell, count)`
In this function, I process information from the game whenever a new safe cell is revealed. The AI gets the number of mines around this cell, and here's what I did:
- I mark the given `cell` as safe and record it as a move that has been made.
- I check all neighboring cells to see if they are mines, and I calculate how many mines are around the cell.
- Based on this, I create a new sentence that represents the neighbors and how many of them are mines.
- Then I call `update_knowledge()` to go over the AI’s knowledge base and make new inferences like marking more cells as safe or mines.

### 2. `update_knowledge()`
This function is key to keeping the AI’s knowledge up to date. It continuously processes the knowledge base and tries to infer new safe cells and mines. Here's what I did:
- I loop through all the sentences in the knowledge base and identify which cells are known to be safe or mines.
- If the AI finds new mines, I mark those cells as mines. If it finds new safe cells, I mark them as safe.
- Then, I try to infer new sentences from the existing ones. For example, if one sentence is a subset of another, the AI will create a new sentence based on that.
- Any empty sentences (those with no remaining cells) are cleaned up to keep the knowledge base efficient.

### 3. `make_safe_move()`
This function makes sure the AI takes a safe move when available. Here’s how I did it:
- The AI checks through the list of safe cells and returns the first one that hasn’t been used yet. 
- If there's a safe move available, it will pick it. If not, the AI will need to make a random move.

### 4. `make_random_move()`
When there’s no obvious safe move left, the AI needs to take a random move. Here's how I implemented it:
- The AI generates a list of all cells that haven't been chosen and aren’t known to be mines.
- It picks a random cell from that list and returns it as the next move.
- If there are no available moves, it returns `None`.

---

### Conclusion
These are the main functions that drive the AI’s decision-making process in the game. It learns more about the board with each move, gradually making better decisions by leveraging propositional logic.
