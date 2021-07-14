
---------------------------------------
ReadMe File for Sudoku Solver in Python
---------------------------------------

** The Purpose of The Document **
---------------------------------
This readme file is prepared to explain how I designed my agent to solve sudoku puzzles and give details on my approach
and the decisions I made during the design stage.

** General Explanation on the Approach and Algorithm Selected **
----------------------------------------------------------------
First of all, I would like to indicate that I am not a sudoku player, so I must indicate that I even didn’t know how to
solve a sudoku puzzle before I attempt to work on this assignment. So as a first step I studied on general sudoku rules 
and tried to solve some sudoku puzzles by myself. Using the experience that I have gained in a relatively short time
I tried to understand how I need to approach to the design of my agent in order to achieve the most efficient solution.

After this preparation period, I started checking the search algorithms that I have learnt during the first two weeks of 
our course unit. Finally, I decided that the backtracking deep-first search with constraint propagation algorithm is the 
best choice for my agent as it is fast and memory friendly. In this algorithm, I understand that empty squares of sudoku
puzzle will be my variables and the values that they can take will be my domains.

In principle my agent would recursively use deep-first search and find an empty square as a first variable and assign
a value from its domains and then search for the next available empty square which will be my second variable in one level
down and assign a value to it as before and in the best case this would go like this until my algorithm realised that there
was no empty square left so this would imply that the solution found. If in any step where there would be no domain found for
a variable would mean to my agent to go back one level up using backtracking and try another value if there is any for the 
variable on that level and continue as described above until a solution found. If there is no solution, then my agent returns
9x9 array with -1 in all its entry.

** Algorithm Testing and Development **
---------------------------------------
At the first attempt I realised that my algorithm worked well for the very-easy, easy and medium level sudoku puzzles but
did not show up any results for the hard sudokus as it was slow. So, certainly I needed to improve the performance of my
agent with a heuristic function to decrease its processing time and increase its speed. While I was searching I realised
that there is an intuitive idea called minimum-remaining-values (MRV) heuristic (Russell and Norvig, 2016).
Therefore, I decided to implement this heuristic into my algorithm. After the implementation, it greatly increased the
performance of my agent and eventually it was able to solve all hard sudoku puzzles quickly as well.

** Inner Function Structure **
------------------------------
If I need to get into more details of my sudoku solver agent, I can say that I created 5 inner functions within the sudoku
solver main function. I summarised their tasks one by one as below.

    * Inner Function 1: validity_check *
    ------------------------------------
    This function checks the validity of the given sudoku and returns True if so and False if not. Moreover, by this way before
    going into costly search processing we can immediately catch if the sudoku is not a valid one so that we can instantly return
    back with no solution (9x9 array with -1 in all its entry)

    * Inner Function 2: search_empty_square *
    -----------------------------------------
    This function is there to find all empty squares and return a list which contains all of them. If there is no square left,
    then it returns False.

    * Inner Function 3: heuristic *
    -------------------------------
    This function searches and finds the empty square with the most constrained space in other words minimum remaining values (MRV)
    (Russell and Norvig, 2016) and returns it. By this way it greatly decreases our processing time so increases the speed of the
    search algorithm.

    * Inner Function 4: constraint_space *
    --------------------------------------
    This function is used to create the constrained space of the selected square for propagation. By this way it greatly decreases 
    the space of the variable so that our agent only searches through these and saves a lot of time.

    * Inner Function 5: search *
    ----------------------------
    This function is the backbone of our agent. It implements the backtracking deep-first search algorithm with constrained
    propagation recursively by using the returned outputs from the previous three functions above.

** References **
----------------
Russell, S. and Norvig, P., 2016. Artificial Intelligence: A Modern Approach. 3rd Ed. Harlow: Pearson Education Limited.
