## Building a secure communication layer for Multi-Party Comptuing - Project Description

## 1. Visions and Goals of the Project

Our communication layer will replace Message Passing Interface (MPI), the data transfer protocol currently being used by Secrecy to perform Multi-Party Computing (MPC). High-level goals for this project include:

  - Get rid of the MPI layer in Secrecy and establish standing TCP connections
  - Implement asynchronous communication
  - Run our Secrecy prototype on a Linux Unikernel (UKL)
  
## 2. Users and Personas of the Project

## 3. Scope and Features of the Project

## 4. Solution Concept

## 5. Acceptance Criteria

Minimum acceptance is defined as replacing MPI in Secrecy with functioning TCP connections and implementing functioning asynchronous communication so that the solution can be tested on the MOC. Stretch goals include:
  - Implementing a Secrecy prototype that performs data transfers and communications as quickly or quicker than MPI.
  - Run a communication-intensive application using our Secrecy prototype on the UKL
  - Testing and benchmarking our prototype to compare performance gains against MPI performance
  
## 6. Release Planning
