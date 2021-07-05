# Time, Clocks, and the Ordering of Events in a Distributed System

## Definition of the **happened-before** (<img src="https://render.githubusercontent.com/render/math?math=\to">) relation

The **happened-before** relation satisfies these three conditions:

1. If *a* and *b* are events in the same process, and *a* comes before *b*, then (<img src="https://render.githubusercontent.com/render/math?math=a \to b">)
2. If *a* is the sending of a message by one process and *b* is the receipt of the same message by another process, then <img src="https://render.githubusercontent.com/render/math?math=a \to b">
3. If <img src="https://render.githubusercontent.com/render/math?math=a \to b"> and <img src="https://render.githubusercontent.com/render/math?math=b \to c"> then <img src="https://render.githubusercontent.com/render/math?math=a \to c">

## Definition of concurrent events
An event *a* is concurrent to an event *b* if <img src="https://render.githubusercontent.com/render/math?math=a \to b"> does not hold.

## Definition of a clock
A clock is just a way of assigning a number to an event. The number is thought of as the time at which the event has occurred.

## Clock condition
A clock to be considered correct must hold the following condition 
For any events *a*, *b*, if <img src="https://render.githubusercontent.com/render/math?math=a \to b">, then <img src="https://render.githubusercontent.com/render/math?math=C(a) < C(b)">. This is the condition that physical clocks don't hold.

Logical clocks lets you capture causality. If event *a* **happens-before** (<img src="https://render.githubusercontent.com/render/math?math=\to">) event *b*, then the timestamp of *a* should be less than the timestamp of *b*.

<img src="https://render.githubusercontent.com/render/math?math=a \to b \Rightarrow T(a) < T(b)">


## Satisfying the clock condition

1. If *a* and *b* are events in the process <img src="https://render.githubusercontent.com/render/math?math=P_i"> and *a* comes before *b*, then <img src="https://render.githubusercontent.com/render/math?math=C_i(a) < C_i(b)">
2. if *a* is the sending of a message by process <img src="https://render.githubusercontent.com/render/math?math=P_i"> and *b* is the receipt of that message by process <img src="https://render.githubusercontent.com/render/math?math=P_j">, then <img src="https://render.githubusercontent.com/render/math?math=C_i(a) < C_j(b)">

## Implementation rules

Leslie Lamport provides a clock implementation broken up into 2 parts called implementations rules (IR). Each part is responsible for addressing one of the above conditions.

IR1: Each process <img src="https://render.githubusercontent.com/render/math?math=P_i"> increments <img src="https://render.githubusercontent.com/render/math?math=C_i"> between any two successful events

IR2: each message *m* contains a timestamp <img src="https://render.githubusercontent.com/render/math?math=T_m"> which equals the time at which the message was sent. Upon receiving a message timestamped <img src="https://render.githubusercontent.com/render/math?math=T_m">, a process must advance its clock to be later than <img src="https://render.githubusercontent.com/render/math?math=T_m">. 

## Total ordering

You can define a total order of events. We simply order the events by the times at which they occur. To break ties, we use any arbitrary total ordering of the processes.

The total ordering depends upon the system of clocks and is not unique

## Mutal exclusion

Leslie Lamport uses this clock implementation and show the usefulness of total ordering by implementing an algorithm that solves a mutual exclusion problem.
