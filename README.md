1. Project Overview
   

The Multi-Level Smart Security Alarm System (ML-SAS) is an advanced embedded system designed using the DMC8 8-bit microprocessor architecture and programmed in Assembly language.
The system monitors environmental inputs in real time and triggers different alert levels based on system state. It supports multiple operational modes, including Safe, Emergency, and Security/Travel modes.



2. System Architecture & Innovative Features

The ML-SAS follows a Defense-in-Depth security approach and includes the following features:

Integrated Digital Lock
The system requires a verified 4-bit passcode (14h) to disarm the alarm. Validation is performed using bitwise isolation and logical comparison inside the CPU.

Dual-Channel Alerting

Local alerts via multi-colored LEDs and an audible buzzer

Remote monitoring through serial communication



3. Advanced Implementation Techniques

The project implements three core embedded-system techniques:

A. Real-Time Polling

A continuous polling mechanism inside the MAIN_LOOP allows the CPU to read Port IA (00h) repeatedly, ensuring immediate detection of environmental changes without relying on interrupts.

B. Bidirectional Handshaking

To guarantee reliable communication with the ASTX serial transmitter, a handshaking protocol is used:

The CPU monitors the RDY signal on ID0 (Port 03h)

Data is transmitted only when RDY = 1, preventing data collisions and ensuring integrity

C. Asynchronous Serial Communication

The system transmits ASCII status codes to represent internal states:

'G' (47h) – System is Good / Safe

'E' (45h) – Emergency detected

'S' (53h) – Security / Travel mode active



4. Programming Logic & Security Protocol

Efficient and secure operation is achieved using low-level bitwise logic:

Input Isolation (Masking)
An AND 3Ch mask is applied to read the passcode from IA2–IA5, filtering irrelevant input bits.

Logical Comparison
The instruction CP 14h compares the input against the predefined secret key.

State Trapping
When an alarm is triggered, the system enters a WAIT_FOR_CODE loop, locking the system until the correct passcode is entered, preventing unauthorized resets.



5. Conclusion

The ML-SAS project demonstrates strong integration between hardware components and Assembly-level control logic.
By implementing Polling, Handshaking, and Asynchronous Serial Communication, the system meets the requirements of a high-level embedded security application and provides a scalable foundation for reliable, real-time security monitoring.
