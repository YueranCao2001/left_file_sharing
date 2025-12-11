# LEFT: Large Efficient Flexible and Trusty File Sharing System

A lightweight **Python socket–based file sharing system** supporting:

- Automatic file & folder detection  
- Large file transmission (tested up to 500MB)  
- Breakpoint retransmission (resume after interruption)  
- File synchronization between two devices  

This project was originally developed as part of the **Introduction to Networking** course.

---

## Features

### 1. Automatic File Detection
The program scans the `share/` directory to detect:
- newly added files (any format, any size)
- newly added folders containing multiple files

### 2. File Transmission Protocol
A custom application-layer protocol over TCP ensures:
- reliable transmission
- correct MD5 integrity verification
- compatibility between Linux virtual instances

### 3. Breakpoint Retransmission
If the receiver is interrupted:
- the partially received file is saved as `.temp`
- after restart, the program continues transmission from where it stopped

### 4. File Synchronization
The system compares file modification time (or MD5) to determine whether synchronization is required, ensuring both devices stay consistent.

---

## Project Structure

```
main.py # entry point, argument parsing & coordination
server.py # sender-side logic (traverse, compute md5, send files)
client.py # receiver-side logic (create dirs, receive & restore files)
share/ # directory being monitored for syncing
```

## How to Run

1. Start two PCs / virtual machines  
2. Clone this repository on both devices  
3. In each device, run:

```
python3 main.py --ip <peer_ipv4_address>
```

Files in each ```share/``` folder will be automatically compared, transmitted, resumed, or synchronized.

## Testing Summary

The system was tested using:

- PyCharm 2021.1.2, Python 3.9

- VirtualBox Linux instances (two VMs)

Key tests included:

- Sending a single 10MB file ✔️

- Sending a 500MB file + folder of 50 files ✔️

- Breakpoint retransmission after forced interruption ✔️

- Synchronization after file update ✔️

All test cases passed successfully.
(Details documented in the original coursework report.)

## Implementation Techniques

- Python Socket programming (TCP)

- Threading & OOP design

- MD5 checksum for data integrity

- Directory traversal & file monitoring

- Error handling for port conflicts and incomplete transfers

## Future Improvements

Planned extensions include:

- File encryption (AES/DES)

- File compression before transmission

- More robust synchronization mechanisms
