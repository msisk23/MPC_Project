## Building a Secure Communication Layer for Multi-Party Computing - Project Description

## 1. Visions and Goals of the Project

Our communication layer will replace Message Passing Interface (MPI), the data transfer protocol currently being used by Secrecy to perform Multi-Party Computing (MPC). High-level goals for this project include:

  - Eliminate MPI dependency in Secrecy and establish standing TCP connections
  - Implement asynchronous communication
  - Run our Secrecy prototype on a Linux Unikernel (UKL)
  
## 2. Users and Personas of the Project

In order for outside parties to benefit from MPC, developers will implementing this improved software. They will benefit from a faster communication layer that enables MPC computation of a data owner's sensitive data at an improved rate.

Developers of the MPC software with this faster communication layer will be the main users of this project as implementation on a unikernel rather than reliance of MPI communication will allow for faster computation.

This project does not target those outside parties (data owner and data learner) that are inputting and visualizing this sensitive data. They will not be interacting with the communication layer as that will be the task of the developers. They will, however, also benefit from faster computation speeds regarding their sensitive data. 

## 3. Scope and Features of the Project

- Remove dependencies on MPI
    - Spawn one process per party without MPI
    - Standing TCP connections between the data analysts, data owner, and the secure computation parties
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
  - MPI: Message Passing Interface - commonly used in cloud computing, has many unnecessary capabilities (unwanted software dependencies) for Secrecy. Is also unable to run on Unikernel
  - Party: One of three web services used during the data transfer process. The "hub" where messages are sent or received.
  - Web: Cloud providers that provide machines were secure computations on supplied data are taking place.
  - Multi Party Communication (MPC): Communication between three cloud services to ensure secure data transmission and evaluation
  - Main Thread: Current line of communication used between parties. Blocking. 
  - Secrecy: Application used to securely analyze private data
  - Communication (Comm) Thread: Non-blocking line of communication to be implemented between parties. Using buffers, will allow for asynchronous party communication.
![image](https://user-images.githubusercontent.com/61120367/134678604-cf5f5657-4c49-4310-be77-839b6323eb1e.png)
_**Figure 2: Architecture of the MPC. Black components currently in use, blue components to be implemented.**_

Figure 2 demonstrates the current structure of the MPC, and the structure to be implemented. Currently, MPI is used to enable communication between parties. During certain points of program execution, parties have to verify information with each other. In the current MPC implementation, parties can only communicate along the Main Thread one message at a time. In order to establish a non-blocking method of asynchronous verification, a Communication Thread (seen in blue) will replace MPI. Using TCP communication, input and output buffers will allow for the non-blocking transfer of data. Later, the data will be processed asynchronously to provide verification for each party. 

**Design Implications and Discussion**

Key Design Decisions and Implementations:
  - MPI Elimination: MPI was first deployed as a temporary solution. In an effort to allow for asynchronous communication between parties, remove unnecessary softwared depenencies and run on UKL, MPI needs to be replaced.
      - This will be done by creating a standing TCP circuit between parties
  - Addition of a Communication Thread: When two parties want to exchange messages through the main thread, it blocks all the main thread operations or computations. By dedicating parties communication tasks to additional threads, the parties will be able to pull from a communication thread buffer, instead of the main thread, which eliminates the block. In order to implement multithreading, we will be using pthreads allowing our group to maintain high speed communication without the MPI.
  - Implementation of Buffers: When two parties want to exchange messages, they cannot do so asynchronously. As such, only one message can be processed at a time. With the addition of input and output buffers, parties will be able to send and pull messages without being in sync.
  - Unikernel Implementation: After verifying functionality of the MPI-free system, MPC will run on top of a Unikernel. The stripped down implementation will further speed up MPC implementation. 


## 5. Acceptance Criteria

Minimum acceptance is defined as replacing MPI in Secrecy with functioning TCP connections and implementing functioning asynchronous communication so that the solution can be tested on the MOC. Stretch goals include:
  - Implementing a Secrecy prototype that performs data transfers and communications as quickly or quicker than MPI.
  - Run a communication-intensive application using our Secrecy prototype on the UKL
  - Testing and benchmarking our prototype to compare performance gains against MPI performance
  
## 6. Release Planning
Release #1:

  - Remove dependencies on MPI from init function


Release #2:

  - Remove dependencies on MPI from init function
  - Establish standing TCP connection between 3 parties


Release #3:

  - Finish establishing standing TCP connections
  - Remove other MPI dependencies


Release #4:

  - Finish removing MPI dependencies
  - Test  to ensure implementation functions without MPI


Release #5:

  - Interface with Unikernel implementors
  - Complete testing
  - Streamline code

## Mentors
John Liagouris: liagos@bu.edu

Professor Orran Krieger: okrieg@bu.edu

Professor Peter Desnoyers: pjd-nu or pjd@ccs.neu.edu

Anqi Guo: anqianqi1
