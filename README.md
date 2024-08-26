## Overview

This project involves developing an application for the ATmega16 microcontroller on the STK500 board, designed to efficiently solve SUDOKU puzzles.
The application takes a SUDOKU puzzle as input via a serial port based on a specified interface and provides a solution quickly and reliably.
It implements a backtracking algorithm to solve the puzzles and includes a feature that activates LEDs to indicate the progress of the solution, 
using a Timer/Counter that triggers an interrupt every 40 ms. The entire codebase is written in C and developed within the Atmel Studio environment for the ATmega16 microcontroller

## Interface

The microcontroller receives instructions from a serial port (UART). The instructions and the responses from the microcontroller are shown in the table:

![alt text](https://github.com/akourkoulos/ProjectSUDOKU/blob/main/projectSUDOKU/Figures/Protocol.png)

## Progress indication with LEDs
In the main function, PORTB is configured as an output, connecting it to the LEDs on the STK500 board. Consequently, the appropriate registers are set with the correct values, enabling compare interrupts for the Timer every 40 ms. During each timer interrupt, the necessary registers are pushed onto the stack. The global progress variable, which increments each time a new cell is solved by the Sudoku algorithm, controls the LEDs. For every ten units of progress, a corresponding LED is turned off, visually indicating the solving progress. After handling the interrupt, the registers are popped from the stack, and the program resumes from where it left off.

## Program flow 

The block diagram below visualizes the entire program's flow. After initializing the necessary registers, the program enters an infinite loop where it waits for interrupts from either the Timer (for updating LEDs) or UART. Upon receiving an interrupt, the program executes the corresponding action. When a complete Sudoku puzzle is received and the play flag is enabled, the program triggers the Sudoku-solving algorithm.

![alt text](https://github.com/akourkoulos/ProjectSUDOKU/blob/main/projectSUDOKU/Figures/program%20flow.png)

## Sudoku solving algorithm

The Sudoku solver uses a backtracking algorithm, implemented in C through the recursive SolveSudoku() function. It scans the grid to find unassigned positions (marked as 0) using FindUnassignedLocation() and tries placing numbers 1 through 9 in each spot. The isSafe() function checks if a number can be placed without violating Sudoku rules. If a valid number is found, it is assigned to the position, and the algorithm recurses to solve the next unassigned cell.
If no valid number is found, the function backtracks, marking the position as unassigned and trying alternative numbers. The algorithm continues until the grid is completely filled (solved) or deemed unsolvable. Each successful placement increases the progress, which updates the LED indicators.

![alt text](https://github.com/akourkoulos/ProjectSUDOKU/blob/main/projectSUDOKU/Figures/SudokuSolver.png)
