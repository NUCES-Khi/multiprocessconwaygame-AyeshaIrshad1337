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
|Serial No|Description|
|-|-|
|1|  Declare variables: board is a pointer to an integer array representing the game board. board_size is the total number of cells in the game board. shmid is the shared memory identifier used to access the shared memory segment. pipe_fd is a two-dimensional array of file descriptors for pipes used for inter-process communication. pid is an array of process IDs for child processes. rows_per_process is the number of rows each child process will be responsible for.|
|2|Create a shared memory segment using shmget() and attach it to board using shmat(). Initialize the game board using init_board().|
|3|    Create pipes for inter-process communication using pipe(). There will be NUM_PROCESSES pipes, one for each child process.|
|4|    Fork NUM_PROCESSES child processes using fork(). Each child process will be responsible for processing rows_per_process rows of the game board.|
|5|Fork NUM_PROCESSES child processes using fork(). Each child process will be responsible for processing rows_per_process rows of the game board.|
|6|    In each child process, simulate the board by calling simulate_board(), passing in the start and end row indices for the child process and the write end of the corresponding pipe. After the child process completes its task, it exits.|
|7|n the parent process, wait for each child process to complete one iteration of the game by reading from the read end of each pipe using read(). Then, send a message to all child processes to proceed to the next iteration by writing to the write end of each pipe using write().|
|8|    After NUM_GENERATIONS iterations, wait for all child processes to finish using waitpid(). Then, print the final state of the game board using print_board().|
|9|    Detach and remove the shared memory segment using shmdt() and shmctl().|

|10|Return 0 to indicate successful execution of the program.|

    
    






## Problems Faced
+ use this list to mention the major problems that you faced in completing this assignment.
+ Please use correct English
+ The print_board function takes an int as its argument instead of an int *. It should be changed to void print_board(int *board).

+The print_board function uses single quotes ('') instead of double quotes (" ") to represent a space character. This should be changed to printf("%c ", board[i * BOARD_SIZE + j] ? ' ' : '-');.

+The simulate_board function is called game_of_life when it is called in the main function. This should be changed to simulate_board(board, start_row, end_row, pipe_fd[i]);.

+The simulate_board function takes a single int as its last argument instead of an int *. It should be changed to void simulate_board(int *board, int start_row, int end_row, int *pipe_fd).

+The simulate_board function writes to the pipe using the wrong file descriptor. It should use write(pipe_fd[1], &msg, sizeof(msg)); instead of write(pipe_fd[1][1], &msg, sizeof(msg));.

+The simulate_board function reads from the pipe using the wrong file descriptor. It should use read(pipe_fd[0], &msg, sizeof(msg)); instead of read(pipe_fd[0][0], &msg, sizeof(msg));.

+The parent process does not synchronize with the child processes after each generation. This can be done by adding a loop that reads from each child process’s pipe and then writes to it after each generation.

## Online / Chat GPT Help
Mention where you got help for your assignment and if you used chat gpt (not encouraged) mention the questions you gave and the reply you got that you are using in the assignment.
Took help from classmates.... watched many repoistry which have done game of life.
## Screenshots
![image](https://github.com/NUCES-Khi/multiprocessconwaygame-AyeshaIrshad1337/assets/104616632/2b1752d1-e1d3-4869-8dd2-a6187a5a7c80)
