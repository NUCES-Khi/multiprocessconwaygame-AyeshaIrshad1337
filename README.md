[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-c66648af7eb3fe8bc4f294546bfd86ef473780cde1dea487d3c4ff354943c9ae.svg)](https://classroom.github.com/online_ide?assignment_repo_id=10686574&assignment_repo_type=AssignmentRepo)
# Assign 02 - Multiprocess Conway Game
|Name|Id|
|-|-|
|Ayesha Irshad|k21-4734|


## Intro
A Template for ConwayGame Multiprocess. This report is part of the assignment you are to complete this report. The headings must remain the same. Remove any other text and add your own. 

## Approach
Breifly explain how did you planned to approach the problem  
### Functions
|Function Name|Description|
|-|-|
|printGeneration|For printing the grid|
|updateRow|Function to update the generation for a single row|

### Main function  
1- Asked user the size of grid which is NxN  
2- Allocate the shared memory in grid and newGrid by using malloc
3- Asked user to input the state in grid for initial generation  
4- Asked user for generation  
5- Created pipes for communciation "**pipes"  
6- Fork for each row and update generations concurrently  
   |-i- In each child process close the read end of pipe and updated the generation for the row and write the updated row in the pipe|  
   |-ii- Created a loop for Waiting for all child process to be completed|  
   |-iii- Readed the updated grid from pipes|  
   |-iv- Copy new grid to original for next generation|    
7- Print the final generated grid
8- free allocated memory
## Problems Faced
+ use this list to mention the major problems that you faced in completing this assignment.
+ Please use correct English

## Online / Chat GPT Help
Mention where you got help for your assignment and if you used chat gpt (not encouraged) mention the questions you gave and the reply you got that you are using in the assignment.

## Screenshots
(![image](https://user-images.githubusercontent.com/104616632/235513975-6dffc168-54c5-45ae-aefb-5c92615de292.png)
) 
