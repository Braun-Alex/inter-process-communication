# 🚀 IPC performance testing tool 🚀

![License](https://img.shields.io/badge/license-MIT-blue.svg) ![C](https://img.shields.io/badge/language-C-blue.svg)

## 🌟 Project overview

Welcome to the IPC performance testing tool 🎉! This project consists of a C application designed to measure and compare the performance of various inter-process communication (IPC) mechanisms in Linux. 🧑‍💻👩‍💻

### 🎯 Key objectives

- **Measure** the performance of different IPC methods.
- **Compare** latency, throughput, CPU utilization and context switches across IPC mechanisms.
- **Provide** insights into the efficiency of each IPC method under different workloads.

## 🛠️ Features

- **Multiple IPC mechanisms**:
  - mmap
  - shared memory
  - file I/O
  - FIFO
  - message queue
  - UNIX socket
- **Customizable workloads**: tests with different data sizes.
- **Comprehensive reporting**: detailed performance metrics.
- **User-friendly**: easy setup and configuration using CMake.

## ⚙️ Installation and running

### 🔧 Prerequisites

Ensure you have the following installed on your system:

- GCC compiler (`sudo apt install gcc`)
- CMake (`sudo apt install cmake`)
- Git (`sudo apt install git`)

### Step 1: clone the repository
Clone the project from GitHub:
```bash
git clone https://github.com/Braun-Alex/inter-process-communication.git
cd inter-process-communication
```

### Step 2: build the project
```bash
mkdir build
cd build
cmake ..
make
```

### Step 3: run the IPC performance test

**Usage**:
```bash
./ipc <ipc_method> [workload]
```

**Paramaters**:
- `<ipc_method>`: the IPC method to test.
- `[workload]`: (optional) size of the data to transfer. Default is 1048576 bytes (1 MB).

**IPC methods**:
- `mmap`
- `shared_memory`
- `file_io`
- `fifo`
- `message_queue`
- `unix_socket`

## 💡 Examples

Below are example commands to run the IPC performance tests for different IPC mechanisms and workloads.

### 1. mmap with 1 MB workload 📄🔄

```bash
./ipc mmap
```

### 2. Shared memory with 50 MB workload 🐧🔄

```bash
./ipc shared_memory 52428800
```

### 3. File I/O with 1 GB workload 📁🔄

```bash
./ipc file_io 1073741824
```

### 4. FIFO with 1 MB workload 🕰️🔄

```bash
./ipc fifo
```

### 5. Message queue with 50 MB workload 📬🔄

```bash
./ipc message_queue 52428800
```

### 6. UNIX socket with 1 GB workload 🌐🔄

```bash
./ipc unix_socket 1073741824
```

## 📝 Performance analysis

Below is a comparison of different IPC mechanisms across various workloads.
Each mechanism was tested under similar conditions, and the results are presented in terms of latency, throughput, CPU utilization,
and voluntary context switches.

### 1. Workload: 1 MB

| Mode     | IPC mechanism   | Latency (ms)         | Throughput (MB/sec) | CPU utilization (ms) | Voluntary context switches
|----------|-----------------|----------------------|---------------------|----------------------|----------------------------|
| Reader   | mmap            | 2.565                | 389.864             | 1.318                | 0                          |
| Writer   | mmap            | 2.124                | 470.81              | 2.788                | 1                          |
| Reader   | shared memory   | 1.621 + 2.66 (sync)  | 616.903             | 0.486                | 1                          |
| Writer   | shared memory   | 2.611 + 0.011 (sync) | 382.995             | 3.524                | 0                          |
| Reader   | file I/O        | 1.674                | 597.372             | 1.071                | 1                          |
| Writer   | file I/O        | 17.105               | 58.462              | 6.334                | 18                         |
| Reader   | FIFO            | 4.131                | 242.072             | 1.585                | 2                          |
| Writer   | FIFO            | 2.582                | 387.297             | 5.053                | 2                          |
| Receiver | message queue   | 2.76                 | 362.319             | 1.7                  | 1                          |
| Sender   | message queue   | 1001.728             | 0.998               | 4.261                | 66                         |
| Server   | UNIX socket     | 0.577                | 1733.102            | 2.468                | 0                          |
| Client   | UNIX socket     | 0.953                | 1049.318            | 2.598                | 4                          |

### 2. Workload: 50 MB

| Mode     | IPC mechanism   | Latency (ms)           | Throughput (MB/sec) | CPU utilization (ms) | Voluntary context switches
|----------|-----------------|------------------------|---------------------|----------------------|----------------------------|
| Reader   | mmap            | 55.82                  | 895.736             | 63.458               | 82                         |
| Writer   | mmap            | 56.004                 | 892.793             | 59.491               | 2                          |
| Reader   | shared memory   | 64.124 + 52.239 (sync) | 779.739             | 71.319               | 1                          |
| Writer   | shared memory   | 52.022 + 0.011 (sync)  | 961.132             | 56.551               | 0                          |
| Reader   | file I/O        | 64.018                 | 781.03              | 80.456               | 1                          |
| Writer   | file I/O        | 161.753                | 309.113             | 123.031              | 181                        |
| Reader   | FIFO            | 137.904                | 362.571             | 78.787               | 132                        |
| Writer   | FIFO            | 77.520                 | 644.995             | 137.077              | 136                        |
| Receiver | message queue   | 76.078                 | 657.22              | 79.936               | 60                         |
| Sender   | message queue   | 1034.766               | 48.32               | 109.739              | 1812                       |
| Server   | UNIX socket     | 21.008                 | 2380.046            | 74.277               | 74                         |
| Client   | UNIX socket     | 21.252                 | 2352.72             | 84.687               | 25                         |

### 3. Workload: 1 GB

| Mode     | IPC mechanism   | Latency (ms)             | Throughput (MB/sec) | CPU utilization (ms) | Voluntary context switches
|----------|-----------------|--------------------------|---------------------|----------------------|----------------------------|
| Reader   | mmap            | 910.679                  | 1124.436            | 1058.208             | 559                        |
| Writer   | mmap            | 910.823                  | 1124.258            | 948.288              | 68                         |
| Reader   | shared memory   | 771.091 + 870.902 (sync) | 1327.989            | 918.762              | 0                          |
| Writer   | shared memory   | 870.794 + 0.011 (sync)   | 1175.938            | 937.326              | 0                          |
| Reader   | file I/O        | 851.232                  | 1202.962            | 877.437              | 3                          |
| Writer   | file I/O        | 1420.735                 | 720.754             | 2031.944             | 1484                       |
| Reader   | FIFO            | 1706.464                 | 600.071             | 1152.683             | 2146                       |
| Writer   | FIFO            | 1097.144                 | 933.332             | 1718.647             | 2158                       |
| Receiver | message queue   | 892.231                  | 1147.685            | 994.228              | 123                        |
| Sender   | message queue   | 1309.524                 | 781.964             | 1389.045             | 65980                      |
| Server   | UNIX socket     | 356.189                  | 2874.878            | 1037.282             | 10619                      |
| Client   | UNIX socket     | 356.267                  | 2874.249            | 1035.884             | 97                         |

## 🔍 Key findings

The performance analysis of the IPC performance testing tool provides valuable insights into the efficiency of various inter-process communication
mechanisms under different workloads. Below are the key observations derived from the test results.

### 📌 Comparison of IPC mechanisms

#### 1. **Latency and throughput**

- **UNIX sockets** consistently exhibit **low latency** and **high throughput** across all workloads, especially in larger data transfers.
- **Memory-based IPC mechanisms** (`mmap`, `shared_memory`):

  - **shared memory** combined with synchronization mechanisms shows **high throughput**, especially in large workloads (1 GB), surpassing other mechanisms.
  - **mmap** offers competitive performance with relatively low latency and high throughput.

- **File I/O** demonstrates good read performance but suffers from higher write latency and lower throughput, particularly in larger workloads due to disk I/O overhead.
- **FIFO** (named pipes) shows moderate performance but is less efficient compared to other mechanisms, especially in terms of latency and context switches.
- **Message queues** have high latency and low throughput in the sender process due to overhead in message handling and system limits.

#### 2. **CPU utilization and context switches**

- **CPU utilization** is generally higher in mechanisms that involve **disk I/O** or **kernel space communication** (`file_io`, `fifo`, `message_queue`).
- **Voluntary context switches** are significantly higher in mechanisms that require more synchronization and involve the kernel (`fifo`, `message_queue`), indicating more frequent process scheduling and potential overhead.

### 📌 Workload-specific observations

#### **1 MB workload**

- **UNIX sockets** achieved the **highest throughput** and **lowest latency**.
- **Shared memory** and **mmap** offer good performance with low latency and high throughput.
- **Message queues** have notably high latency on the sender side, resulting in extremely low throughput.

#### **50 MB workload**

- **UNIX sockets** remain the top performer in terms of throughput and latency.
- **mmap** and **shared memory** continue to provide high throughput, with **shared memory** showing improved performance due to efficient memory operations.
- **File I/O** shows increased write latency and reduced throughput, reflecting the impact of disk I/O overhead.
- **FIFO** and **message queues** lag behind in throughput and exhibit higher CPU utilization and context switches.

#### **1 GB workload**

- **UNIX sockets** outperform other mechanisms with the highest throughput and lowest latency.
- **Shared memory** shows excellent throughput, surpassing **mmap** and approaching the performance of **UNIX sockets** when synchronization is efficiently handled.
- **File I/O** write operations suffer significantly, with increased latency and CPU utilization due to disk I/O limitations.
- **FIFO** and **message queues** are less suitable for large workloads due to higher latency, lower throughput, and increased context switching.

### 📌 Overall insights

- **Memory-based IPC mechanisms** are highly efficient for large data transfers within the same system, offering high throughput and low latency.
- **UNIX sockets** provide the best overall performance, combining low latency, high throughput, and moderate CPU utilization, making them suitable for a wide range of IPC scenarios.
- **Disk-based IPC mechanisms** (`file_io`) are limited by disk I/O performance, leading to higher latency and CPU usage, especially in write operations.
- Efficient synchronization in **shared memory** operations is crucial to achieve high throughput and low latency.
- **Message queues** are less efficient for large data transfers due to system limitations and overhead in message handling, but may be suitable for small messages and control signals.

## ⚠️ Important notes

- **Synchronization**. For mechanisms like **shared memory** and **mmap**, proper synchronization between processes is essential to prevent race conditions and ensure data consistency. The performance can be significantly impacted by the synchronization method used.
- **System limits**. Mechanisms like **message queues** have system-imposed limits (e.g., maximum message size and queue length), which can affect performance and suitability for large data transfers.
- **Disk I/O bottlenecks**. **File I/O** performance is heavily dependent on the underlying disk subsystem. SSDs may improve performance but cannot match the speed of memory-based IPC mechanisms.
- **Context switches**. High numbers of voluntary context switches can indicate increased overhead due to process scheduling and synchronization, impacting overall performance.
- **Use case suitability**. The choice of IPC mechanism should consider the specific use case, data sizes, and performance requirements. No single mechanism is optimal for all scenarios.

## 📜 License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file 📝 for details.
