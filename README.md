## Building a Secure Communication Layer for Multi-Party Computing - Project Description

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

- Remove dependencies from MPI
    - Spawn one process per party without MPI
    - Standing TCP connections between parties
    - Asynchronous Communication
       - Implement communication threads
       - Implement input/output buffers
       - Establish ability for threads to push/pull data from buffers
    - Maintain proper function of all other aspects of current Secrecy framework

- TCP
    - A server used for standard socket programming that will be implemented in C
    - It rearranges data packets in the order specified with guarantee that they will be received in the same order sent
    - Does flow control
    - To set up standard socket connection, three data network packets to set up the socket connection
    
    ![image](https://github.com/msisk23/MPC_Project/blob/main/TCP%20Flow%20Diagram.png)
    _**Figure 1: Flow Diagram of how a TCP Server operates.**_ 

- Unikernel deployment
    - Benchmarking of MPI alternative
    - Ability to run communication-intensive applications using our MPI alternative on a Linux Unikernel (UKL)
    - Report performance improvements when using UKL (if any)

- Unikernel
    - Our understanding is that we aren't going to worry about the UKL until after we have a functioning MPI solution, and then PhD students from Professor Krieger's group will help us run Secrecy on UKL.

## 4. Solution Concept
**Global Architectural Structure of the Project**

Crucial project components and definitions:
  - MPI: Message Passing Interface - commonly used in cloud computing, has many unnecessary capabilities (unwanted software dependencies) for Secrecy. Is also unable to run on   Unikernel
  - Party: One of three web services used during the data transfer process. The "hub" where messages are sent or received.
  - Web: Cloud providers that provide machines were secure computations on supplied data are taking place.
  - Multi Party Communication (MPC): Communication between three cloud services to ensure secure data transmission and evaluation
  - Main Thread: Current line of communication used between parties. Blocking. 
  - Communication (Comm) Thread: Non-blocking line of communication to be implemented between parties. Using buffers, will allow for asynchronous party communication.
![image](https://user-images.githubusercontent.com/61120367/134678604-cf5f5657-4c49-4310-be77-839b6323eb1e.png)
_**Figure 2: Architecture of the MPC. Black components currently in use, blue components to be implemented.**_

Figure 2 demonstrates the current structure of the MPC, and the structure to be implemented. Currently, MPI is used to enable communication between parties. During certain points of program execution, parties have to verify information with each other. In the current MPC implementation, parties can only communicate along the Main Thread one message at a time. In order to establish a non-blocking method of asynchronous verification, a Communication Thread (seen in blue) will replace MPI. Using TCP communication, input and output buffers will allow for the non-blocking transfer of data. Later, the data will be processed asynchronously to provide verification for each party. 

**Design Implications and Discussion**

Key Design Decisions and Implementations:
  - MPI Elimination: MPI was first deployed as a temporary solution. In an effort to allow for asynchronous communication between parties, all MPI dependencies will be removed.
  - Addition of a Communication Thread: When two parties want to exchange messages through the main thread, it blocks all the main thread operations or computations. By dedicating parties communication tasks to additional threads, the parties will be able to pull from a communication thread buffer, instead of the main thread, which eliminates the block. In order to implement multithreading, we will be using pthreads allowing our group to maintain high speed communication without the MPI.
  - Implementation of Buffers: When two parties want to exchange messages, they cannot do so asynchronously. As such, only one message can be processed at a time. With the addition of input and output buffers, parties will be able to send and pull messages without being in sync.
  - Unikernel Implementation: After verifying functionality of the MPI-free system, MPC will run on top of a Unikernel. The stripped down implementation will further speed up MPC implementation. 


## 5. Acceptance Criteria

Minimum acceptance is defined as replacing MPI in Secrecy with functioning TCP connections and implementing functioning asynchronous communication so that the solution can be tested on the MOC. Stretch goals include:
  - Implementing a Secrecy prototype that performs data transfers and communications as quickly or quicker than MPI.
  - Run a communication-intensive application using our Secrecy prototype on the UKL
  - Testing and benchmarking our prototype to compare performance gains against MPI performance
  
## 6. Release Planning
Release #1 (due by Week 5):
  - Remove dependencies from MPI
  - Span three Communcation Threads

Release #2 (due by Week 7):
  - Implement Communication Thread input/output buffers

Release #3 (due by Week 9):
  - Establish TCP connections between parties

Release #4 (due by Week 11):
  - Implementation of features based on performance analysis against MPI-based implementation
  - Base Unikernel implementation
Release #5 (due by Week 13):
  - Final Unikernel implementation
  - Implementation of features based on further performance analysis
