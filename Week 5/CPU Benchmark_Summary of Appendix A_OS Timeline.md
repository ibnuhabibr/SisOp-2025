# Practices

## 1. CPU Benchmark Testing in IOPS and FLOPS Units

### 1. FLOPS & IOPS TESTING ON CPU

#### 1. Introduction
CPU benchmarking is a method used to measure the processor's performance in handling various instructions. FLOPS (Floating Point Operations Per Second) and IOPS (Integer Operations Per Second) are two metrics commonly used to measure CPU performance in numerical computations and integer operations. In this report, we will test the CPU's performance using the flops-iops tool available on GitHub in an Ubuntu operating system running on VirtualBox.

#### 2. Objectives
The goal of this report is to:
- Measure the CPU's performance in handling floating point operations (FLOPS) and integer operations (IOPS) in a virtual environment.
- Analyze the benchmark results on an Ubuntu system running on VirtualBox.

#### 3. Testing Methodology

##### 3.1 Hardware and Software
- **Hardware**: Laptop with Intel Core i5-11300H processor.
- **Host Operating System**: Windows.
- **Virtual Operating System**: Ubuntu.
- **Virtual Machine Software**: Oracle VM VirtualBox.
- **Testing Tool**: flops-iops from [GitHub](https://github.com/ferryastika/flops-iops).

##### 3.2 Virtual Machine Configuration
- **Number of CPU Cores**: 4 Cores.
- **RAM**: 8 GB.
- **Virtualization Support**: VT-x/AMD-V feature enabled.

##### 3.3 Testing Steps
1. **Environment Setup**
   - Install dependencies:
     ```sh
     sudo apt update
     sudo apt install -y build-essential
     ```
   - Clone the flops-iops repository:
     ```sh
     git clone https://github.com/ferryastika/flops-iops.git
     cd flops-iops
     ```
   - Build the program:
     ```sh
     make
     ```
2. **Running the Test**
   - Run the FLOPS and IOPS benchmarks:
     ```sh
     ./iops32
     ./iops64
     ./flops32
     ./flops64
     ```

#### 4. Results and Analysis
After running the tests, the system will display the benchmark results in terms of IOPS and FLOPS. Here is an example of the results obtained from testing in a virtual environment:

##### FLOPS 32-bit:
- Max CPU Throughput: **5.51 GIOPS**
- Max Single Core Throughput: **1.41 GIOPS**

![image](https://github.com/ibnuhabibr/SisOp-2025/blob/main/img/flops32.png)

##### FLOPS 64-bit:
- Max CPU Throughput: **10.98 GIOPS**
- Max Single Core Throughput: **2.75 GIOPS**

![image](https://github.com/ibnuhabibr/SisOp-2025/blob/main/img/flops64.png)

##### IOPS 32-bit:
- Max CPU Throughput: **6.59 GIOPS**
- Max Single Core Throughput: **1.66 GIOPS**

![image](https://github.com/ibnuhabibr/SisOp-2025/blob/main/img/iops32.png)

##### IOPS 64-bit:
- Max CPU Throughput: **7.02 GIOPS**
- Max Single Core Throughput: **1.78 GIOPS**

![image](https://github.com/ibnuhabibr/SisOp-2025/blob/main/img/iops64.png)

From the results, it can be observed that the performance in the virtual environment is lower than testing directly on physical hardware. This is due to the virtualization overhead and the limited resource allocation in the VM.

#### 5. Conclusion
- FLOPS and IOPS provide an insight into the CPU performance in handling floating-point operations and integer operations in a virtual environment.
- This testing can help in evaluating the impact of virtualization on processor performance.

---

## 2. Appendix-A Summary

### A.1 Introduction
To understand basic operating system concepts such as CPU scheduling, memory management, and file systems, we can examine how these concepts were implemented in some of the early influential operating systems.

Some of these operating systems were specifically designed for large computers (mainframes), while others were for smaller computers. Some of these systems were unique and not widely used but had a significant impact on the systems that followed.

**The main objectives of this section:**
- Explain how operating system features evolved and migrated from large computers to smaller systems.
- Describe the characteristics of some of the most influential historical operating systems.

### A.2 Feature Migration in Operating Systems
Features initially developed for mainframes (large computers) were then adopted for minicomputers and eventually applied to microcomputers and handheld devices. For example:
- **MULTICS** pioneered memory security and protection concepts, which are now used in modern operating systems such as Windows, Linux, and macOS.

### A.3 Influential Operating Systems

![timeline_os](https://github.com/ibnuhabibr/SisOp-2025/blob/main/img/Sejarah%20SisOp.png)

#### 1. MULTICS (Multiplexed Information and Computing Services)
- Developed by MIT, Bell Labs, and General Electric in the 1960s.
- Featured high-level security, virtual memory, and a hierarchical file system.
- Inspired Unix.

#### 2. UNIX
- Developed by Ken Thompson and Dennis Ritchie at Bell Labs.
- Simplified and modular design.
- Became the foundation for modern operating systems like Linux and macOS.

#### 3. OS/360
- Developed by IBM for mainframe computers.
- Supported batch processing and time-sharing.

#### 4. THE (Technische Hogeschool Eindhoven) Operating System
- Developed by Edsger Dijkstra.
- Introduced the concept of **layered structure**.

#### 5. XDS-940
- A time-sharing operating system.
- Influenced the design of subsequent multi-user operating systems.

#### 6. CTSS (Compatible Time-Sharing System)
- Allowed multiple users to access the computer simultaneously.

#### 7. CP/M (Control Program for Microcomputers)
- One of the first operating systems for microcomputers.
- Became the foundation for MS-DOS.

#### 8. MS-DOS and Windows
- MS-DOS evolved from CP/M and was widely used on IBM computers.
- Windows introduced a GUI for MS-DOS.

#### 9. MacOS
- The first operating system to widely adopt the GUI.
- Influenced the design of modern operating systems.

### A.4 Concepts and Innovations from Historical Operating Systems
Some key concepts that are still used in modern systems include:
1. **Time-Sharing and Multitasking**
   - Developed from CTSS and XDS-940.
2. **Hierarchical Operating System (Layered Structure)**
   - Introduced by THE Operating System.
3. **Virtual Memory**
   - Developed from MULTICS and OS/360.
4. **Hierarchical File System**
   - Developed in UNIX and MULTICS.
5. **Security and Protection**
   - MULTICS introduced strong security features.
6. **Graphical User Interface (GUI)**
   - First introduced in macOS and Windows.
