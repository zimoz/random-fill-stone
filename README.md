Objectives:
1.	Randomly fill a NxN 2D array with 0s and 1s. 
2.	Print the array.
3.	Count the number of stones around the selected cell.
4.	Calculated the distribution.
5.	Import the distribution into a new 2D array.
6.	Repeat

Steps:
1.	Define the global constants.
2.	Prompt for the number of bins along each edge of the board/numbers of stones/seeds/repeat time.
3.	Dynamically allocate two 2D arrays to hold the grid (the bins).
4.	Use try and catch to check the validation of the input.
5.	MyFactorial calculates the factorial of certain number
6.	Permutation calculates the total permutation.
7.	ArrayP1Fill fills the 2D array with 1s and 0s.
8.	ArrayRandFill randomly fills the 2D array with 1s and 0s.
9.	PrintSqArray prints a square dynamically allocated 2D array.
10.	PrintArray prints a 2D array with MAX_TYPES_NEIGH rows by (MAX_INTERIOR_NEIGH+1) columns.
11.	CalcDistribution calculates the theoretical distribution of probabilities.
12.	CountDistribution counts the number of neighbours which contain 1 of 3 types of the cells: edge, corner, or inner.

Restrictions:
1.	0 < bins along each edge <= MAX_SIZEGRID 
2.	0 < # of stones <= MAX(bins along each edge)^2 
3.	1 < seed <= RAND_MAX
4.	0 < number of repeats <= MAX_REPEATS

