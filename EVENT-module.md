# About this

In programming, multiple threads can communicate with each other by signaling events and handling events. An event, then, is like a message from one thread to another threads.

  **Example 1:**
 
  In a MP3 player one thread scans a set of keys while the main thread is playing a song. When a key is pressed an event is send to the main thread, for example to stop the playing.


  **Example 2:**

  In a home automation application, a thread may be monitoring the presence of fire. If fire is detected the thread generates an alarm event to 2 threads: one to establish a communication with the firemen, and another to activate a series of actuators to extinguish the fire.

To use this module you must take into consideration the following:

  1. Create an event using the event.create function. The create function returns an event instance. You must store this instance into a variable for further operation with it.

  ```lua
  keyPressed = event.create()
  ```

  1. Use the event instance in 
