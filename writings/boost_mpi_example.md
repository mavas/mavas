# Boost MPI example

This page describes a message passing interface (MPI) example I've concocted.

## How this demonstration works

Docker Compose is used to create several 'computers', with an example Boost MPI C++ program running on each one, and these computers work together to perform a computation/calculation, properly demonstrating the use of message passing interface.

The computation performed is that of sorting numbers.  At the beginning of each run, a list of 1,000 random numbers is generated, and the computers are used to sort them, via MPI.

This demonstration works because it makes use of only a minimal Boost MPI C++ program deployed on a number of discrete and isolated computers, and it successfully computes something that MPI is designed for.
