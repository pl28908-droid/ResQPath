# Emergency Ambulance Routing System

An algorithm-based ambulance route planning system that finds routes from an accident location to a hospital using **Breadth-First Search (BFS)**, **Uniform Cost Search (UCS)**, and **A* Search**.

The project models a small city as a weighted graph. Users can specify traffic conditions and blocked roads, choose a destination hospital or automatically select the nearest reachable hospital, and compare the routes produced by different search algorithms.

## Project Overview

In emergency situations, choosing a suitable route can make a significant difference. This project demonstrates how graph-search algorithms can be applied to ambulance routing by representing city locations as nodes and roads as weighted edges.

The system currently uses a predefined city map containing:

- **9 locations:** A, B, C, D, E, F, G, H, I
- **2 hospitals:** C and I
- **Weighted roads:** Each edge represents an estimated travel time in minutes

It is an educational simulation using a static graph, rather than a live navigation system.

## Features

- **Multiple pathfinding algorithms:** Run BFS, UCS, A*, or all three for the same route request.
- **Traffic simulation:** Apply a multiplier to road travel times:
  - Clear roads: `×1.0`
  - Moderate traffic: `×1.5`
  - Heavy traffic: `×2.0`
- **Road-block handling:** Remove specified roads from the graph before searching.
- **Nearest hospital selection:** Use UCS to compare travel costs to the available hospitals and select the closest reachable one.
- **Algorithm comparison:** Display route cost and number of explored nodes for each selected algorithm.
- **Route summary:** Display the selected route and its estimated travel time.
- **Input validation:** Check location and menu inputs before proceeding.

## Algorithms Used

### 1. Breadth-First Search (BFS)

BFS explores the graph level by level using a FIFO queue.

- Useful for finding a path with the fewest edges in an unweighted graph.
- In this project, it also accumulates the weights of the selected route.
- **Important:** Because roads have different travel times, BFS does not necessarily find the minimum-time route.

### 2. Uniform Cost Search (UCS)

UCS expands the node with the lowest cumulative path cost using a priority queue (min-heap).

- Considers road travel times when choosing a route.
- Finds a minimum-cost route when edge weights are non-negative.
- Also used by the nearest-hospital finder to compare the travel cost to each hospital.

### 3. A* Search

A* uses both the cost already travelled and a heuristic estimate of the remaining cost.

`f(n) = g(n) + h(n)`

Where:
- `g(n)` = actual cost from the start node to the current node
- `h(n)` = estimated cost from the current node to the goal
- `f(n)` = estimated total route cost through the current node

The project stores heuristic estimates for both hospital destinations.

**Note:** A*'s optimality depends on the heuristic and implementation conditions. The heuristic values are predefined for this sample map and should be validated if the graph or road costs are changed.

## City Map

The project uses the following predefined road network. Numbers represent travel times in minutes, and `*` marks a hospital.

```text
   A ──4── B ──3── C*
   │        │        │
   6        2        5
   │        │        │
   D ──1── E ──7── F
   │                 │
   8                 3
   │                 │
   G ──2── H ──4── I*

   Hospitals: C and I
```

## How It Works

1. The program displays the city map.
2. The user selects the traffic condition.
3. The user can enter roads to block, or press Enter to skip.
4. The user enters the accident location.
5. The user chooses automatic nearest-hospital selection or enters a hospital destination.
6. The user selects BFS, UCS, A*, or ALL.
7. The program displays the route, total travel cost, and explored-node count.
8. If all algorithms are run, a comparison is displayed.

## Getting Started

### Requirements

- Python 3.8 or later
- No external Python packages required (the project uses Python standard-library modules).

### Installation

Clone the repository:

```bash
git clone https://github.com/<your-username>/<your-repository-name>.git
cd <your-repository-name>
```

### Run the project

If your Python file is named `main.py`, run:

```bash
python main.py
```

If it has a different filename, replace `main.py` with that filename.

## Example Interaction

```text
Traffic conditions:
  1. Clear roads      (×1.0)
  2. Moderate traffic (×1.5)
  3. Heavy traffic    (×2.0)

Enter choice (1/2/3): 2

Enter roads to block: A-B, D-E

Enter accident location (start): A

Auto-select NEAREST hospital? (y/n): y

Choose algorithm:
  1. BFS
  2. UCS
  3. A*
  4. ALL
```

The program then prints the route details and, when `ALL` is selected, an algorithm comparison. Actual results depend on the selected start location, traffic multiplier, and blocked roads.

## Technologies Used

- **Language:** Python
- **Data structure:** Weighted graph represented using an adjacency list
- **Queue:** `collections.deque` for BFS
- **Priority queue:** `heapq` for UCS and A*
- **Core concepts:** Graph traversal, informed and uninformed search, path-cost calculation, heuristic search

## Project Structure

```text
project/
│
├── main.py       # Main program containing the graph and search algorithms
└── README.md     # Project documentation
```

Adjust the filename in this structure if your Python source file has a different name.

## Limitations and Future Scope

This project is a simplified academic simulation. It currently uses a fixed city graph, manually selected traffic multipliers, predefined blocked roads, and hardcoded heuristic values. It does not connect to real maps, GPS devices, live traffic feeds, or hospital systems.

Possible future improvements:

- Integrate real map data and road networks.
- Use live traffic information instead of manually selected traffic multipliers.
- Add dynamic road closures and incident updates.
- Build a graphical map-based interface.
- Validate or calculate heuristics automatically when the road network changes.
- Extend the model to include multiple ambulances and emergency requests.

## Learning Outcomes

Through this project, we explored:

- Representing a road network using a weighted graph.
- Implementing BFS, UCS, and A* search.
- Understanding the difference between path length and weighted path cost.
- Using queues and priority queues for graph search.
- Simulating traffic conditions and road blockages.
- Comparing algorithms using route cost and nodes explored.

## Disclaimer

This project is developed for academic and learning purposes. It is not intended for real-world emergency dispatch or navigation.

---

**If you find this project useful, feel free to star the repository!**
