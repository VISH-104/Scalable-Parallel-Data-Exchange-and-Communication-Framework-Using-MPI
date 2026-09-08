# ⚡ Scalable Parallel Data Exchange and Communication Framework Using MPI

> **MPI-based distributed-memory application for iterative data exchange, parallel computation, and scalability benchmarking.**

---

## 📌 Project Overview

This project implements a **distributed-memory MPI application in C** for iterative point-to-point data exchange between configurable process distances. Each valid sender exchanges large data arrays with receivers at distances \(D_1\) and \(D_2\), performs parallel numerical updates, and repeats the communication–computation cycle for multiple iterations.

The implementation is benchmarked across different **process counts and data sizes** to study execution time, communication overhead, and distributed-memory scalability.

---

## 🔬 Methods

- **MPI Communication:** Point-to-point data exchange between configurable rank distances \(D_1\) and \(D_2\).
- **Parallel Computation:** \(D_1\) receivers perform element-wise square operations, while \(D_2\) receivers apply logarithmic transformations.
- **Iterative Updates:** Returned data are combined at the sender and transformed into buffers for the next communication iteration.
- **Final Aggregation:** Valid sender ranks send their final data to rank 0 for maximum, average, and execution-time evaluation.
- **Benchmark Configuration:** \(P = 8,16,32\), \(M = 1024^2, 2048^2\) doubles, \(D_1=2\), \(D_2=4\), \(T=10\), seed \(=1000\).

### 🔄 Computational Workflow

```text
Data Initialization → MPI Point-to-Point Exchange → D1/D2 Computation → Return Data → Sender Update → Repeat T Iterations → Rank-0 Aggregation
```

---

## 🛠️ Key Contributions

- Developed a **distributed-memory MPI application in C** for configurable point-to-point data exchange.
- Implemented **iterative communication and parallel numerical computation** for large data arrays.
- Supported large messages up to **2048² doubles** across **8, 16, and 32 MPI processes**.
- Implemented rank-dependent data updates and final aggregation at **rank 0**.
- Benchmarked execution performance across **process counts and data sizes** using repeated runs.
- Quantified **communication overhead and parallel scalability** through execution-time analysis.

---

## 📊 Results & Validation

The application was evaluated using the prescribed benchmark configurations with **five executions per configuration**.

| Parameter | Configuration |
|---|---|
| MPI Processes | **8, 16, 32** |
| Data Size | **1024², 2048² doubles** |
| Communication Distances | **D1 = 2, D2 = 4** |
| Iterations | **T = 10** |
| Random Seed | **1000** |
| Repetitions | **5 per configuration** |
| Nodes | **16 processes per node** |

Execution time was analyzed across process counts and data sizes using **boxplots**, enabling comparison of runtime variation and parallel scalability.

> **Note:** Numerical performance values are intentionally not stated here because the provided assignment specification defines the required benchmark configurations but does not provide measured execution-time results.

---

## 🧩 Conclusion

The project demonstrates an MPI-based **distributed-memory communication and computation workflow** for large-message data exchange. Performance benchmarking across process counts and problem sizes provides insight into **communication overhead, execution-time behavior, and scalability** of parallel applications.

---

## 🛠️ Tools & Technologies

- **Language:** C
- **Parallel Programming:** MPI
- **Communication:** MPI Point-to-Point Communication
- **Memory Model:** Distributed Memory
- **Benchmarking:** Execution-Time Measurement, Repeated Runs
- **Performance Analysis:** Boxplot-Based Scalability Analysis
- **Execution:** `mpirun`, Hostfile-Based MPI Execution

---

## 📁 Repository Structure

```text
.
├── README.md
├── src/
│   └── main.c
├── scripts/
│   └── run_benchmark.sh
├── results/
│   └── execution_times.csv
└── plots/
    └── scalability_boxplot.png
```

> Add the actual source code, benchmark script, measured results, and final plot to the corresponding folders before publishing the repository.

---

## ▶️ Execution

```bash
mpirun -np <P> -f hostfile ./src/main <M> <D1> <D2> <T> <seed>
```

Example:

```bash
mpirun -np 16 -f hostfile ./src/main 1048576 2 4 10 1000
```

