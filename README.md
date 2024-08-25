## Overview

This project involves developing an application for the ATmega16 microcontroller on the STK500 board, designed to efficiently solve SUDOKU puzzles.
The application takes a SUDOKU puzzle as input via a serial port based on a specified interface and provides a solution quickly and reliably.
It implements a backtracking algorithm to solve the puzzles and includes a feature that activates LEDs to indicate the progress of the solution, 
using a Timer/Counter that triggers an interrupt every 40 ms. The entire codebase is written in C and developed within the Atmel Studio environment for the ATmega16 microcontro

