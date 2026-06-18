# Artificial Intelligence Foundations Report

## Overview

This project explores two foundational areas of Artificial Intelligence:

1. **Numerical optimisation**, implemented through a square-root approximation agent.
2. **Graph search**, implemented through route-finding algorithms for London Underground station data.

The work demonstrates how objective functions, update rules, search strategies, heuristics, and cost functions can be used to solve practical problems.

---

# 1. Square Root Agent

## Objective

The square-root agent estimates the square root of a positive number `x`.

The agent begins with an initial guess `y₀` and repeatedly updates the estimate until the objective function falls below a small threshold `ε`.

The general goal is:

```text
Find yₙ such that yₙ² ≈ x
```

## Absolute Error Objective

The first objective function uses absolute error:

```text
J = |yₙ² - x|
```

This measures the direct difference between the current squared estimate and the target value.

Using a Newton-style update gives:

```text
yₙ₊₁ = yₙ - (yₙ² - x) / (2yₙ)
```

This update adjusts the current estimate using both the current error and the slope of the function.

## Squared Error Objective

The second objective function uses squared error:

```text
J = (yₙ² - x)²
```

The derivative is obtained using the chain rule:

```text
dJ/dyₙ = 4yₙ(yₙ² - x)
```

Substituting this into the update rule gives:

```text
yₙ₊₁ = yₙ - (yₙ² - x) / (4yₙ)
```

## Why the Update Rules Work

Both update rules gradually move the estimate towards a value where the objective function is close to zero.

The Newton-style update uses the relationship between the current error and the local slope. This allows the estimate to move in a direction that reduces the error over repeated iterations.

The squared-error update is less direct than the absolute-error update, but still produces convergence because the update direction continues to reduce the distance between `yₙ²` and `x`.

## Implementation Summary

The square-root implementation includes:

- Input validation for positive numeric values
- Random initialisation of the starting estimate
- Iterative update loops
- Convergence checks using a small tolerance
- Test cases comparing results against `math.sqrt`

---

# 2. Route-Finding Search Algorithms

## Objective

The route-finding task models London Underground stations as a graph.

Each station is represented as a node. Each connection between stations is represented as an edge with an associated travel cost and line name.

The objective is to compare different search strategies across several routes using:

- The path returned by the algorithm
- The number of visited nodes
- The total travel cost

## Algorithms Implemented

## Breadth-First Search

Breadth-First Search explores stations level by level.

It is useful for finding paths with fewer station-to-station transitions, but it does not directly optimise for travel time.

## Depth-First Search

Depth-First Search explores one route as deeply as possible before backtracking.

It can be memory-efficient, but it does not guarantee the lowest travel time or the fewest stations.

## Uniform Cost Search

Uniform Cost Search expands the route with the lowest cumulative travel cost first.

This makes it suitable for finding low-cost routes when all travel costs are non-negative.

## Uniform Cost Search with Line-Change Penalty

This version extends Uniform Cost Search by adding an extra cost when the route changes Tube lines.

This models the practical inconvenience of line changes and can produce routes that prioritise fewer changes over raw travel time.

## Heuristic BFS

The heuristic BFS variant uses zone information to guide the search.

The heuristic compares station zones and prioritises routes that appear closer to the destination zone. This can reduce exploration in some cases, but it may also produce longer travel times if the heuristic does not align well with the true route cost.

---

# 3. Route Comparison Results

## Canada Water to Stratford

| Method | Visited Nodes | Total Travel Cost |
|---|---:|---:|
| BFS | 52 | 15 |
| DFS | 52 | 54 |
| UCS | 55 | 14 |
| UCS with line-change cost | 21 | 15 |
| Heuristic BFS | 12 | 21 |

## New Cross Gate to Stepney Green

| Method | Visited Nodes | Total Travel Cost |
|---|---:|---:|
| BFS | 53 | 14 |
| DFS | 33 | 50 |
| UCS | 19 | 14 |
| UCS with line-change cost | 16 | 24 |
| Heuristic BFS | 42 | 50 |

## Ealing Broadway to South Kensington

| Method | Visited Nodes | Total Travel Cost |
|---|---:|---:|
| BFS | 53 | 19 |
| DFS | 22 | 47 |
| UCS | 50 | 19 |
| UCS with line-change cost | 45 | 24 |
| Heuristic BFS | 18 | 46 |

## Baker Street to Wembley Park

| Method | Visited Nodes | Total Travel Cost |
|---|---:|---:|
| BFS | 26 | 13 |
| DFS | 100 | 68 |
| UCS | 85 | 13 |
| UCS with line-change cost | 28 | 13 |
| Heuristic BFS | 73 | 68 |

## Results Summary

No single algorithm is consistently best across every route and metric.

- **BFS** can find short station-count paths, but does not optimise travel cost.
- **DFS** can explore long routes and may produce inefficient paths.
- **UCS** is generally strong when the goal is to minimise travel cost.
- **UCS with line-change cost** is useful when route convenience matters.
- **Heuristic BFS** depends heavily on the quality of the heuristic.

The results show that the best algorithm depends on the optimisation goal.

---

# 4. Implementation Challenges

Several implementation challenges were considered during development.

## Avoiding Infinite Loops

Visited-node tracking was required to prevent the algorithms from repeatedly revisiting the same stations.

## Queue Sorting

Uniform Cost Search and heuristic search required queue sorting so that the next expanded route matched the algorithm’s priority rule.

## Zone Handling

Station zones could appear in different orders because they were stored in sets. Sorting was used to make zone-based comparisons more consistent.

## Start Station Equals Destination

A direct check was needed for cases where the starting station and destination station were the same.

## Longest-Path Search

The longest-path experiment was more computationally expensive than the route-finding tasks. A recursive DFS approach with memoisation was used to reduce repeated calculations.

---

# 5. Longest-Path Experiment

## Method

The longest-path function uses a recursive depth-first strategy.

Instead of searching from one fixed start station to one fixed destination, it explores possible paths from each station and tracks the longest route found.

Memoisation is used to store intermediate results and avoid recomputing paths that have already been explored.

## Result

The longest route found contained:

```text
104 stations
```

The route started at:

```text
Harrow & Wealdstone
```

and ended at:

```text
Wanstead
```

## Discussion

The longest-path task is more complex than standard route finding because the search space is much larger and the destination is not fixed.

DFS is suitable for this type of exploration because it naturally follows paths deeply before backtracking. Memoisation improves performance by avoiding repeated work.

---

# Conclusion

This project demonstrates how different AI techniques can be applied to numerical and graph-based problems.

The square-root agent shows how objective functions and update rules can be used for iterative optimisation. The route-finding system shows how search algorithms behave differently depending on whether the objective is shortest path length, lowest travel cost, fewer line changes, or heuristic-guided exploration.

The main conclusion is that algorithm choice should depend on the problem objective rather than assuming one method is universally best.
