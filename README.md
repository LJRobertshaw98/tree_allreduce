# tree_allreduce
Creating a highly efficient tree reduction algorithm in C using MPI

A reduction algorithm is an algorithm which, given an operator, applies that operator to all processes. These processes each have a matrix of values rather than just a single value. The most basic way to operate on these processes is a ring reduction. This is where each process visits every other process and operates on its own values with that of the process it is currently visiting. The outcome is that each process holds the same end result, for example if each process started with a 2D vector and the operator was to sum, every process would now store a 2D vector whose 1st component is the sum of all processes' first component, similarly for the 2nd component of the vector. On the other hand, a tree reduction algorithm works by operating pairwise between processes. For example if we have 2 processes, the data stored by processes 0 and 1 is operated on and the result is stored on the even process (0 in this case). With more processes this forms a tree where each process operates on its data with its neighbour and the even processes carry the end result down the tree. The algorithm is shown in more detail in the "diagram" file. The end result is that as the number of processes grows, the time taken for a tree reduction to complete all operations grows logarithmically. In comparison, the time taken for a ring reduction algorithm to complete the operation grows linearly. Thus the tree algorithm is more efficient by nature. In my implementation, MPI is used to assign the data to each process and to parallelise the code.
