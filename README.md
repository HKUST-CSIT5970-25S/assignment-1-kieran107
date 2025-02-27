[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/IAASVEAZ)

# CSIT5970 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Friday

---

### Name: ZHANG, Zhenghao
### Student Id: 21093189
### Email: zzhangjq@connect.ust.hk

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

    > The measurement tool used for evaluating CPU and memory performance is the **Phoronix Test Suite**, an open-source benchmarking software. For CPU performance, the `pts/compress-7zip` test was run to measure compression and decompression ratings in MIPS (Millions of Instructions Per Second), with the results averaged over three rounds to minimize variability. This configuration ensures consistency and reliability in assessing the computational performance of the system. For memory performance, the `pts/ramspeed` test was executed using the `copy int` operation, which benchmarks memory bandwidth in MB/s, also averaged over three rounds. These configurations were chosen to ensure a balance between statistical accuracy and test efficiency. The results represent quantitative performance metrics, such as execution speed (MIPS) for CPU and memory bandwidth (MB/s), allowing for comparisons against other systems or configurations.

2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?

    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

    | Size        | CPU performance | Memory performance |
    | ----------- | --------------- | ------------------ |
    | `t2.micro` | Compression: 3678 MIPS<br />Decompression: 3093 MIPS | 10856.60 MB/s (Copy Int) |
    | `t2.medium`  | Compression: 9644 MIPS<br />Decompression: 5743 MIPS | 19119.59 MB/s (Copy Int) |
    | `c5d.large` | Compression: 7623 MIPS<br />Decompression: 5081 MIPS | 13908.73 MB/s (Copy Int) |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.

## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

    | Type                      | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | `t3.medium` - `t3.medium` | 3720           | 0.282    |
    | `m5.large` - `m5.large`   | 4930           | 0.293    |
    | `c5n.large` - `c5n.large` | 4980           | 0.171    |
    | `t3.medium` - `c5n.large` | 2370           | 0.647    |
    | `m5.large` - `c5n.large`  | 2590           | 0.622    |
    | `m5.large` - `t3.medium`  | 4470           | 0.253    |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.

2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

    | Connection                | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | N. Virginia - Oregon      | 31.8           | 62.881   |
    | N. Virginia - N. Virginia | 4450           | 0.269    |
    | Oregon - Oregon           | 4740           | 0.133    |

    > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.
