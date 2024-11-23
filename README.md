Thread Execution

Each thread prints its PID (process ID) and TID (thread ID) using getpid() and pthread_self(). 
The threads then sleep for 1 second in a loop, counting down from their respective start times (10 for thread-1 and 15 for thread-2).
After finishing the countdown, each thread prints a message indicating it's exiting, then terminates with pthread_exit(NULL);.

Explanation of Threading and Synchronization 

Concurrency: 
Both threads run concurrently, meaning they execute at the same time (depending on the OS scheduling). They share the same process ID (PID) but have different thread IDs (TIDs).

Thread Creation: 
Threads are created using pthread_create(), which takes the following parameters:

     The address of the pthread_t variable to store the thread ID.

     The thread attributes (here it’s the stack size).

     The function to be executed by the thread.

     The argument to pass to the function (in this case NULL since no argument is needed).

Thread Synchronization: The pthread_join() calls ensure that the main thread waits for both thread-1 and thread-2 to finish before it prints "all threads done!" and terminates.
Without pthread_join(), the main function might exit before the threads finish executing, leading to incomplete output or undefined behavior.

Expected Output

The program will output something like this (with the exact thread IDs varying):

 The address of the pthread_t variable to store the thread ID.

    main: creating thread-1
    main: creating thread-2
        thread-1: PID[1234] and TID[1398751]
        thread-2: PID[1234] and TID[1398752]
        thread-1[10]
        thread-2[15]
        thread-1[9]
        thread-2[14]
        thread-1[8]
        thread-2[13]
        ...
        thread-1: exiting
        thread-2[3]
        thread-2[2]
        thread-2[1]
        thread-2: exiting
    main: all threads done!
    
Thread-1 prints a countdown from 10 to 1 and then exits.

Thread-2 prints a countdown from 15 to 1 and then exits.

The main thread waits for both threads to complete before printing the final message.
