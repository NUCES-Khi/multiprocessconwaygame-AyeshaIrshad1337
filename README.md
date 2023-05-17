[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-c66648af7eb3fe8bc4f294546bfd86ef473780cde1dea487d3c4ff354943c9ae.svg)](https://classroom.github.com/online_ide?assignment_repo_id=10686574&assignment_repo_type=AssignmentRepo)
# Assign 02 - Multiprocess Conway Game
|Name|Id|
|-|-|
|Ayesha Irshad|k21-4734|


## Intro  
This program is an implementation of John Conway's Game of Life using multiple processes to parallelize the computation of each generation. The program initializes a game board with random values, forks multiple child processes, and simulates a portion of the game board in each child process. Each child process communicates with the parent process using pipes to synchronize after each generation. The parent process waits for all child processes to finish before exiting
## Approach
Breifly explain how did you planned to approach the problem  
```
The main function first initializes the game board by creating a shared memory segment using shmget and attaching it to the address space of the current process using shmat. It then creates an array of pipes for inter-process communication using pipe.

It then forks NUM_PROCESSES child processes and assigns each process a portion of the game board to simulate. The child processes call the simulate_board function to simulate their portion of the game board using the rules of the Game of Life. The function applies the rules to each cell in the sub-grid and communicates with the parent process using pipes to synchronize after each generation.

The parent process waits for all child processes to complete each generation before sending a message to all child processes to proceed to the next generation. After all generations are complete, the parent process waits for all child processes to finish before exiting
```
### Functions
|Function Name|Description|
|-|-|
|print_board|For printing the grid|
|apply_rules	|Function to apply the rules of the game to a single cell|
|simulate_board	|Function to simulate a portion of the game board|
|init_board	|Function to initialize the game board with random values|
### Main function  
The approach for this problem is as follows:

    
    Allocate the shared memory in grid and newGrid using malloc.
    Ask the user to input the state in grid for initial generation.
    Ask the user for the number of generations.
    Create pipes for communication using pipe.
    Fork a new child process for each row of the grid to update the generations concurrently.
        In each child process, close the read end of the pipe and update the generation for the row. Write the updated row in the pipe.
        Create a loop to wait for all child processes to be completed.
        Read the updated grid from pipes.
        Copy the new grid to the original for the next generation.
    Print the final generated grid.
    Free the allocated memory.  
  
7- Print the final generated grid  
8- free allocated memory
## Problems Faced
+ use this list to mention the major problems that you faced in completing this assignment.
+ Please use correct English

## Online / Chat GPT Help
Mention where you got help for your assignment and if you used chat gpt (not encouraged) mention the questions you gave and the reply you got that you are using in the assignment.

## Screenshots
