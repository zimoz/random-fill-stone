To compile this code you need you use g++ compiler 

This code basiclly randomly fill a N by N 2d array with either 0 or 1. 
And then print the arrary. And then count the number of stone around the selected cell.
Then calculated the distribution and import the distribution into a new 2d array with certain number of rows and number of columns.
Then repeat a certain amount of times


1. define the global constants
2. prompt for the number of bins along each edge of the borad/number of stones/seeds/repeat time
3. Dynamically allocate two 2-D arrays to hold the grid (the bins)
4. Use try and catch to check the vaildation of the input
5. function MyFactorial calculate the factorial of certain number
6. function Permutation calculate the total permutation 
7. function ArrayP1Fill fill the 2d array with 1 and 0
8. function ArrayRandFill randomly fill the 2d array with 1 and 0
9. function PrintSqArray print a square dynamically allocated 2-D integer array
10.function PrintArray Print a 2-D integer array with dimensions MAX_TYPES_NEIGH  rows by (MAX_INTERIOR_NEIGH + 1) columns. 
11.function CalcDistribution calculate the theoretical distribution of probabilities.
12.function CountDistribution count the number of neighbours which contain 1 with 3 kinds of center cell : edge corner and inner


0 <  bins along each edge  <= MAX_SIZEGRID
0 <  # of stones  <= MAX_(bins along each edge)2
1 <  seed  <=  RAND_MAX.
0 <  number of repeats  <=  MAX_REPEATS
