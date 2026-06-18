# Artificial Intelligence Foundations

This repository contains a small collection of foundational Artificial Intelligence implementations in Python.

The project is split into two main parts:

1. **Square Root Agent**  
   An iterative numerical agent that estimates square roots using Newton-style update rules with absolute-error and squared-error objective functions.

2. **Route-Finding Search Algorithms**  
   A London Underground route-finding system that compares classic search strategies including Breadth-First Search, Depth-First Search, Uniform Cost Search, Uniform Cost Search with line-change penalties, and a heuristic zone-based search.

## Project Structure

```text
artificial-intelligence-foundations/
│
├── README.md
├── requirements.txt
├── .gitignore
│
├── sqrt_agent.py
├── search_algorithms.py
│
└── project_report.md
```

## Techniques Demonstrated

- Iterative optimisation
- Newton-style numerical updates
- Objective functions
- Breadth-First Search
- Depth-First Search
- Uniform Cost Search
- Heuristic search
- Graph traversal
- Route-cost comparison
- Basic performance evaluation using visited nodes and travel cost

## Requirements

Install the required Python package:

```bash
pip install -r requirements.txt
```

The project uses Python standard-library modules such as `math`, `random`, and `collections`, plus `pandas` for reading the route data.

Python 3.12 or later is recommended.

## Running the Square Root Agent

```bash
python sqrt_agent.py
```

This runs the built-in square-root tests using several input values and prints whether the estimates are close to the values returned by `math.sqrt`.

## Running the Route-Finding Algorithms

The route-finding script expects a London Underground dataset named:

```text
tubedata.csv
```

Place this file in the repository root, then run:

```bash
python search_algorithms.py
```

The code includes implementations for:

- Breadth-First Search
- Depth-First Search
- Uniform Cost Search
- Uniform Cost Search with added line-change cost
- Heuristic BFS using zone information
- Longest-path exploration using recursive DFS with memoisation

## Report

A written project report is available here:

```text
docs/project_report.md
```

It summarises the square-root agent, search algorithms, route comparison results, implementation challenges, and the longest-path experiment.

## Notes

The route-finding results depend on the contents and format of `tubedata.csv`. The expected CSV structure is:

```text
StartingStation, EndingStation, TubeLine, AverageTimeTaken, MainZone, SecondaryZone
```
