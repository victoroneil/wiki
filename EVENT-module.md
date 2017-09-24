# About this

In programming, multiple threads can communicate with each other by signaling events and handling events. An event, then, is like a message from one thread to another threads.

An event can be used for:

* Report from one thread to another that something important has happened.

  Example: In a home automation application, a thread may be monitoring the presence of fire. If fire is detected the thread generates an alarm event to 4 threads:

    * Thread 1: establish a communication with firefighters to give the warning.
    * Thread 2: turn on an acoustic alarm.
    * Thread 3: activate a series of actuators to try to extinguish the fire.

* Synchronize a thread with another.

  Example: 

