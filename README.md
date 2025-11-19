# 🚚 Delivery Route Optimization for E-commerce (DAA Capstone)

This project explores a complex logistics challenge faced by e-commerce companies: optimizing a delivery route to minimize travel distance/time while adhering to critical real-world constraints, specifically **vehicle capacity** and **customer time windows**.

The solution integrates multiple algorithmic paradigms—including **Recurrence, Greedy, Dynamic Programming (DP), Graph Algorithms (Dijkstra/Prim),** and the **Traveling Salesman Problem (TSP)**—to model and solve the multi-constrained optimization problem.

## 🌟 Project Highlights

  * **Multi-Constraint Optimization:** Solves for the optimal route considering distance (TSP), vehicle capacity (Greedy Knapsack), and delivery time constraints (DP check).
  * **Algorithmic Integration:** Demonstrates the application and interaction of five different algorithmic strategies within a single real-world problem context.
  * **Intractability Analysis:** Profiles and visualizes the exponential time complexity growth of the TSP Brute-Force approach for small instances.

-----

## 💡 Algorithmic Strategy Overview

The overall strategy involves a multi-stage filtering process:

1.  **Greedy Selection (Feasibility):** Determine the maximum value of parcels that can fit the `vehicle_capacity` (30 kg) using a value/weight ratio heuristic. This establishes the **feasible subset of customer nodes** to visit.
2.  **TSP Optimization:** Use Brute-Force to find the shortest closed-loop route (Warehouse → Feasible Customers → Warehouse) for the reduced graph.
3.  **DP Validation (Feasibility Check):** Use a dynamic cost function to check if the TSP-optimal route is also **time-feasible** by ensuring all arrivals fall within the specified delivery windows.

| Problem | Strategy | Time Complexity | Domain | Notes |
| :--- | :--- | :--- | :--- | :--- |
| Route Cost Estimation | **Recurrence Relation** | $O(N)$ for fixed route | Logistics | Models the additive cost (distance/time) of a sequential path. |
| Parcel Selection | **Greedy Algorithm** (Value/Weight Ratio) | $O(N \log N)$ | Knapsack Problem | Maximizes load value subject to the $30 \text{kg}$ weight constraint (Initial constraint filter). |
| Time Window Compliance | **Dynamic Programming** (Conceptual Check) | $O(N^2)$ (Sequence Optimization) | Time-Constrained Path | Evaluates the feasibility of a path's sequence against time window constraints, penalizing lateness/wait time. |
| Shortest Path | **Dijkstra's Algorithm** | $O(E + V \log V)$ | Graph Theory | Finds the minimal travel time/distance from the Warehouse to all other nodes. |
| Optimal Delivery Sequence | **TSP Brute-Force** | $O(N! \cdot N)$ | Combinatorial Optimization | Finds the shortest closed-loop route (Warehouse → All → Warehouse). **Intractable** for large $N$. |

-----

## 🔎 Key Findings and Analysis

The problem was solved with multiple constraints, leading to a complex conclusion:

1.  **Capacity Constraint:** The vehicle could only carry parcels **C1 (10kg)** and **C2 (20kg)**, resulting in a total value of **110** and total weight of **30 kg**. Customer C3 was excluded.
2.  **Distance Optimality (TSP):** The shortest route covering the feasible set (W, C1, C2) had a total distance of **17 units**.
3.  **Time Window Failure:** Critically, the subsequent DP check showed that the TSP-optimal routes (both permutations: W → C1 → C2 → W and W → C2 → C1 → W) **violated the strict time windows** for C1 or C2, resulting in an "Infeasible" status.

### Trade-offs: Optimality vs. Computation Time

  * The **Brute-Force TSP** guarantees the absolute shortest distance (optimality) but is computationally **intractable** for large numbers of customers, as demonstrated by the **exponential ($O(N!)$) time complexity growth** visualized in the profiling section.
  * The final solution for this specific input is **"NO FEASIBLE ROUTE EXISTS"** that satisfies both the capacity constraint and the time window constraints simultaneously. This highlights that in real-world VRP, finding a **feasible** route often takes precedence over finding the single **distance-optimal** route.

-----

## ⚙️ Setup and Execution

### Prerequisites

You need Python (3.6+) installed.

### Dependencies

Install the required libraries:

```bash
pip install -r requirements.txt
```

### Files

  * `delivery_route_optimization.ipynb`: The main Jupyter Notebook containing all code, plots, and markdown explanations.
  * `README.md`: This file.
  * `requirements.txt`: Lists necessary Python libraries.

### How to Run

1.  Clone the repository:
    ```bash
    git clone https://github.com/jedapaw/delivery_route_optimization
    ```
2.  Navigate to the directory:
    ```bash
    cd delivery_route_optimization
    ```
3.  Install dependencies (if not already done):
    ```bash
    pip install -r requirements.txt
    ```
4.  Open and run the notebook:
    ```bash
    jupyter notebook delivery_route_optimization.ipynb
    ```
