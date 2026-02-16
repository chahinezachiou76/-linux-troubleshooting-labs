# Linux Troubleshooting: Resolving Disk Space Exhaustion (Saint John Challenge)

##  About this Project
This repository contains a technical write-up for the **"Saint John"** scenario from [SadServers](https://sadservers.com/). 

**Troubleshooting** is the process of identifying, tracing, and fixing problems in a system. In this case, I diagnosed and fixed a server issue where a rogue process was filling up the disk space rapidly.

---

##  The Problem (Scenario)
The server disk was filling up due to a testing program continuously writing to a log file: `/var/log/bad.log`. 
* **The Goal:** Find the process (PID) writing to this file and stop it.
* **The Constraint:** Do not delete the log file itself.

---

##  Commands & Solution Steps

### 1. Monitor File Activity
To confirm the file was growing in real-time, I used:
`tail -f /var/log/bad.log`
*Result: Confirmed constant data stream appending to the log.*

### 2. Identify the Culprit (PID)
To find out which program was writing to the file:
`lsof /var/log/bad.log`
*Result: Identified the Process ID (PID) responsible for the file growth.*

### 3. Terminate the Process
To stop the process immediately and force it to close:
`sudo kill -9 <PID>`
*Result: The writing stopped instantly.*

### 4. Reclaim Disk Space
To empty the file and free up space without deleting the file itself:
`sudo truncate -s 0 /var/log/bad.log`
*Result: File size reduced to 0 bytes.*

---

##  Final Result
The challenge was solved successfully!

![Success Badge](1000005218.jpg)

###  Summary Table
| Command | Why I used it |
| :--- | :--- |
| tail -f | To monitor live growth of the file. |
| lsof | To get the PID of the rogue program. |
| kill -9 | To forcefully stop the program. |
| truncate | To clear file content without deleting it. |

---
**Platform:** [SadServers.com](https://sadservers.com/)
