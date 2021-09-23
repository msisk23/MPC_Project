## Building a secure communication layer for Multi-Party Comptuing - Project Description

## 1. Visions and Goals of the Project

Our communication layer will replace Message Passing Interface (MPI), the data transfer protocol currently being used by Secrecy to perform Multi-Party Computing (MPC). High-level goals for this project include:

  - Get rid of the MPI layer in Secrecy and establish standing TCP connections
  - Implement asynchronous communication
  - Run our Secrecy prototype on a Linux Unikernel (UKL)
  
## 2. Users and Personas of the Project

Multi-party computation is built off of the relationship between data owners and data learners. These titles are designated to anyone who owns sensitive data that needs computation to be applied along with any party who the owner has allowed to learn about the findings of this computation.

Common occurrences of this relationship are:

  - Patients (data owner) releasing personal health data to a healthcare provider (data learner)
  - Educational institutions (data learner) analyzing student GPAs (data owner)
  - Government agencies (data learner) analyzing the wages of each gender to determine potential gaps in workers (data owner) pay

This project does not target those who do not need to compute sensitive data from multiple parties. 

## 3. Scope and Features of the Project

## 4. Solution Concept
Global Architectural Structure of the Project:
Crucial project components and definition:
API: Layer, written in C, to process data transfer between application and web server.
Party: One of three web services used during the data transfer process. The "hub" where messages are sent or received.
Main Thread: Current line of communication used between parties. Blocking. 
Communication (Comm) Thread: Non-blocking line of communication to be implemented between parties. Using buffers, will allow for asynchronous party communication.

Design Implications and Discussion:
![image](https://github.com/msisk23/MPC_Project/blob/ca9bb11c63c2797bce30a572713003b7bdbfc677/Diagram.jpg)

## 5. Acceptance Criteria

Minimum acceptance is defined as replacing MPI in Secrecy with functioning TCP connections and implementing functioning asynchronous communication so that the solution can be tested on the MOC. Stretch goals include:
  - Implementing a Secrecy prototype that performs data transfers and communications as quickly or quicker than MPI.
  - Run a communication-intensive application using our Secrecy prototype on the UKL
  - Testing and benchmarking our prototype to compare performance gains against MPI performance
  
## 6. Release Planning
