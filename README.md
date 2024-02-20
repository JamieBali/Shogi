# Shogi Computer

During my A-Levels, I created a simple AI system which was able to play Shogi (a japanese board game similar to chess). It was bad - it had predictable openings which made it easy to gain an early advantage, it put too much priority on re-placement of captured tiles which ultimately gives the player a development advantage, and it took upwards of 20 seconds to think of the next move. It was able to think 4 moves ahead (2 of its moved and 2 user moves), which meant that it only really proved a challenge to novice players. Being the first AI system I'd ever made, I don't think it was too bad, but now that I've done a lot more AI development I want to remake it and see how much better it will be.

## Issues With My Old System

Let's start by pinpointing the main issues with the old system and see how we can fix them - we'll focus only on the code here, not the ms paint graphics or any UX design.

### Incorrect Implementation of Minimax

The algorithm used in my old system isn't quite the minimax algorithm, but it effectively does the same thing. Correct minimax implementation should create a tree of all moves that could be made, finding the value of a state only at the leaf nodes, whereas the system I made was making dynamic calculations based on the move made. When taking a pawn, the value of the board would be dynamically updated by +1, and when losing a general the value of the board would be dynamically updated by -3. This means duplicated code, and way more calculations. It also means far too many large passed parameters.

In the new system, I will implement proper minimax, as this will make the program more space and time efficient, won't need a 12 times nested for loop to run, and allow me to implemetn Alpha-Beta Pruning.

### Decomposition 

The system I made had 2 different classes - "Game" which featured the board, the menu, the interaction code, and all the processing for the user (such as highlighting clicked tiles and showing possible moves); "AI" which featured the code for the AI move generation system. The use of functions was also extremely limited and ended up resulting in a lot of duplicated code - the functions were very broad and could all be reduced down to turn what was almost 1000 lines down to (what I predict could be) 250 lines at most.

### Absence of AB Pruning

One of the main issues with the old system is the amount of time it takes to generate the next move (or a hint for what the users next move should be). The only time reduction steps in place were to skip processing on moves that resulted in the loss of a king. In order to make this work better in the new system, I will implement Alpha-Beta pruning - a system I have since implemented a few times. I have more details about AB pruning and the minimax algorithm as a whole in this report I wrote at univesity. https://github.com/JamieBali/checkersMinimax/blob/main/Knowledge%20and%20Reasoning%20Report.pdf

### The Buttons

Rather than generating the buttons for my board at the start, I manually placed them on a windows form in Visual Studio and wrote a block of code into every button's detection algorithm to call the required functions. I don't need to explain why this is awful design.

## Goals of this Project

Recreate my shogi computer so it now works correctly, efficiently, and poses at least a moderate challenge. The system should be able to think at least 4 moves ahead, make moves in less than 1 second, and be able to beat a novice shogi player. Code should be written in C# (as was with the original).
