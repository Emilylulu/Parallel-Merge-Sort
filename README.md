# Parallel-Merge-Sort
## Merge Sort
You need to write a program, sort_mpi, that will take as input two files, the file of numbers to sort and the file it should write sorted numbers in. A baseline serial program, sort, is provided to you as C code. The input file is a text file with 𝑁𝑁 unsigned integers, one per line. After executing the program, the output file should contain the same numbers as in the input file, except in sorted order. Essentially, your program will operate like the Unix sort utility, but without any of the fancy command options and always saving the sorted result to a file.
For example, the list of 5 numbers below,
      2
      1948
      523
      43
      298754
would be sorted into the list below and written to a file.
      2
      43
      523
      1948
      298754
## Parallel Strategy
Design your programs so that they follow the following steps:
1. One process reads the file and distributes the data to the other processes.
2. All processes locally sort the data that they received in step 1.
3. All the processes work together to merge the results of step 2. (This means no serial operations of size O(N)).
4. One process is responsible for doing the output.
## Approach
I use one process to load all data, and then send to every node, every node locally sorted using quick sort, then merge all node together in one main process, use this main process write to file. For the send part, I use scatterv to avoid unequal data for each node. Then treat the node named with even rank as master node. And treat the node named with odd rank as slave node. Merge master node and slave node together. For the merge part, I use bottom up merge algorithm. Two for loop instead of recursive call.
As a final result, main process will hold the final sorted array and print them out in a file.
