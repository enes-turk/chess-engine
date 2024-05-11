# Chess Engine and AI

This personal project merges my passion for chess with my eagerness to delve into object-oriented programming.

# Tools Utilized

Python was the sole language utilized in this project, with Pygame serving as the primary library for constructing game states to interact with the game board.

# The Engine

### **Board**

- This chess engine facilitates player versus player (PvP) matches or challenges against an AI opponent. Additionally, it provides the option to spectate matches between AI opponents.
- Smooth animations have been implemented to enhance immersion.
- Illuminated squares have been introduced to offer visual cues regarding valid piece movements.
- On the side of the board, a game log screen using professional chess notations allows players to track the progression of the match.

<img src="/readme_assets/presentation_1.gif" alt="present_1" width="70%">

### **Functionalities**

Every essential functionality of the centuries-old game of chess is embedded within this engine.

#### Undo Moves

Mistakes happen, but fear not! You can undo moves to rectify any rookie errors. The log also updates to reflect the current state.

<img src="/readme_assets/presentation_2.gif" alt="present_2" width="70%">

#### Castling

Seize the opportunity to fortify your king's position through castling maneuvers, available on both flanks of the board.

<img src="/readme_assets/presentation_3.gif" alt="present_3" width="70%">

#### En Passant

Embracing the complexity of chess, the en passant rule has been integrated into the game mechanics.

<img src="/readme_assets/presentation_4.gif" alt="present_4" width="70%">

#### Checkmate, Stalemate

And in the finale, you can be the one to deliver the final blow with a checkmate.

<img src="/readme_assets/presentation_5.gif" alt="present_5" width="70%">



# The AI

To enhance the AI's capabilities, numerous algorithms were implemented to simulate the decision-making process of a real player. Drawing inspiration from the famous chess engine like Stockfish, complex structures were devised to generate improved moves and optimize performance. Among the algorithms implemented (such as min-max, nega-max, recursive best, recursive min-max, and recursive nega-max), the recursive model for nega-max exhibited the best performance. By incorporating alpha-beta pruning, the algorithm dynamically evaluates the maximum and minimum available positions, further enhancing its efficiency and allowing for deeper search depths.

The nega-max algorithm efficiently evaluates positions by calculating the maximum possible gain and minimum possible loss, enabling the engine to reach the optimal move swiftly. Depth was incorporated into the model to enhance move accuracy. Additionally, a hardcoded method was implemented to evaluate positions for specific pieces and squares, while not the optimal approach for a robust engine. However, it proved to be an effective approach in lower depths.

```python
def findMoveNegaMaxAlphaBeta(gs, validMoves, depth, alpha, beta, turnMultiplier):
    global nextMove, counter
    counter += 1
    if depth == 0:
        return turnMultiplier * scoreBoard(gs)
    
    # move ordering implement later
    maxScore = -CHECKMATE
    for move in validMoves:
        gs.makeMove(move)
        nextMoves = gs.getValidMoves()
        score = -findMoveNegaMaxAlphaBeta(gs, nextMoves, depth-1,-beta, -alpha, -turnMultiplier)
        # score = max(score, maxScore) # Python has built-in max function. Rather than doing below it's somewhat useful.
        if score > maxScore:
            maxScore = score
            if depth == DEPTH:
                nextMove = move
        gs.undoMove()
        if maxScore > alpha: # pruning happens
            alpha = maxScore
        if alpha >= beta:
            break 
    return maxScore
```



### Conclusion

This chess engine and AI project represents not just a technical accomplishment but a testament to the enduring fascination and challenge of the game of chess. Through its features and functionalities, it opens up new avenues for players to explore and enjoy the game in both traditional and innovative ways.
