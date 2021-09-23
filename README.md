## Building a secure communication layer for Multi-Party Comptuing - Project Description

## 1. Visions and Goals of the Project

Our communication layer will replace Message Passing Interface (MPI), the data transfer protocol currently being used by Secrecy to perform Multi-Party Computing (MPC). High-level goals for this project include:

  - Get rid of the MPI layer in Secrecy and establish standing TCP connections
  - Implement asynchronous communication
  - Run our Secrecy prototype on a Linux Unikernel (UKL)
  
## 2. Users and Personas of the Project

Multi-party computation is built off of the relationship between data owners and data learners. These titles are designated to anyone who owns sensitive data that needs computation to be applied along with any party who the owner has allowed to learn about the findings of this computation.

Common occurrences of this relationship are:

Patients (data owner) releasing personal health data to a healthcare provider (data learner)
Educational institutions (data learner) analyzing student GPAs (data owner)
Government agencies (data learner) analyzing the wages of each gender to determine potential gaps in workers (data owner) pay

This project does not target those who do not need to compute sensitive data from multiple parties. 

## 3. Scope and Features of the Project

## 4. Solution Concept

## 5. Acceptance Criteria

Minimum acceptance is defined as replacing MPI in Secrecy with functioning TCP connections and implementing functioning asynchronous communication so that the solution can be tested on the MOC. Stretch goals include:
  - Implementing a Secrecy prototype that performs data transfers and communications as quickly or quicker than MPI.
  - Run a communication-intensive application using our Secrecy prototype on the UKL
  - Testing and benchmarking our prototype to compare performance gains against MPI performance
  
## 6. Release Planning
