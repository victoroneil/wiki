# About this

In programming, multiple threads can communicate with each other by signaling events and handling events. An event, then, is like a message from one thread to another thread.

  **Example 1:**
 
  In a MP3 player one thread scans a set of keys while the main thread is playing a song. When a key is pressed an event is send to the main thread, for example to stop the playing.


  **Example 2:**

  In a home automation application, a thread may be monitoring the presence of fire. If fire is detected the thread generates an alarm event to 2 threads: one to establish a communication with the firemen, and another to activate a series of actuators to extinguish the fire.

To use this module you must take into consideration the following:

  1. Create an event using the event.create function. The create function returns an event instance. You must store this instance into a variable for further operation with it.

     ```lua
     keyPressed = event.create()
     ```

  2. Use the event instance and call to the wait function when a thread requires to wait for the event. When the event is processed call to the done function.

     ```lua
     while true do
        keyPressed:wait()
        print("a key is pressed")
        keyPressed:done()
     end
     ``` 

  3. Use the event instance an call to the broadcast function when you need to inform the waiting threads that the event has occurred.

     ```lua
     keyPressed:broadcast()
     ```

     The broadcast function accepts a boolean argument to indicate if the calling thread must wait for the process of the event by all the waiting threads.

# Functions

## instance = event.create()

Creates a new event instance.

Arguments: nothing.

Returns: an event instance, or an exception. You must store this instance into a variable for further operations with it.

## instance:disable() 

Disables an event instance, unblocking all the threads that are waiting for the event instance. When an event is disabled all calls to instance:broadcast or instance:wait are ignored.

Arguments: nothing.

Returns: nothing, or an exception

## instance:enable() 

Enables a disabled event instance.

Arguments: nothing.

Returns: nothing, or an exception

## instance:broadcast([wait for completion]) 

Broadcast an event instance to all the threads that are waiting for this event.

Arguments:

* wait for completion (optional): is a boolean that indicates whether the calling thread must wait for the event to be processed on all threads that are waiting for the event. If true the calling thread is blocked until all threads have processed the event. By default the value for this argument is false (don't wait).

Returns: true if the event has been broadcasted, false if the event is disabled, or an exception.

## instance:wait()

Wait for an event, blocking the calling thread until the event is broadcasted.

Arguments: nothing.

Returns: true if the event has been broadcasted, false if the event has been disabled while waiting, or an exception.

## instance:done()

Indicates that the thread has been processed the event.

Arguments: nothing.

Returns: nothing.

# Example

In the following example a set of sensors are attached in the main thread, and once attached the sensor values are monitored in a secondary thread.

```lua
-- Create an event
sensorsAttached = event.create()

thread.start(function()
   sensorsAttached:wait()
   sensorsAttached:done()

   while true do
        print("Monitor")

       distance_r = right:read("distance")
       distance_l = right:read("distance")
   
      tmr.delay(1)
   end
end)

-- Instantiate sensors
right = sensor.attach("2Y0A21", adc.ADC1, 0)
left  = sensor.attach("2Y0A21", adc.ADC1, 0)

-- Broadcast event
sensorsAttached:broadcast()
```