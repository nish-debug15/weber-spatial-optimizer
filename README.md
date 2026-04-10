# weber-spatial-optimizer

> **Locating the mathematical center of demand using first-order optimization.**

## Overview
This repository contains a spatial optimization engine built from scratch to solve the **Continuous Weber Problem**. Bypassing standard black-box machine learning libraries, this project implements a custom Gradient Descent algorithm to calculate the mathematically perfect location for an autonomous medical drone hub.

By processing the exact GPS coordinates and historical emergency demand weights of five major medical centers, the algorithm iteratively descends a highly non-linear cost surface to find the global minimum—optimizing for battery efficiency, flight time, and critical care delivery speed.

## The Mathematical Engine
The objective is to minimize the total weighted flight distance. Because the Euclidean distance cost surface is convex but highly nonlinear, setting the derivatives to zero does not yield an algebraic solution for more than three coordinates. 

**The Cost Function (J):**
J(X,Y) = Σ [ w_i * √((X - x_i)² + (Y - y_i)²) ]

By calculating the partial derivatives of the cost function with respect to X (Longitude) and Y (Latitude), the algorithm determines the gradient vector and steps in the direction of steepest descent.

**The Update Rules:**
X_new = X_old - α(∂J / ∂X)
Y_new = Y_old - α(∂J / ∂Y)

## Key Technical Implementations
* **Algorithmic Execution:** Built entirely in Python using `numpy` for vectorized matrix operations, ensuring lightweight and rapid computation.
* **Geospatial Hyperparameter Tuning:** Standard learning rates (e.g., α = 0.5) cause massive overshooting when applied to the micro-scale of decimal degree GPS coordinates. The learning rate was heavily tuned and dropped to `0.005` to force a monotonic convergence to the optimal coordinates without bouncing past the global minimum.
* **Visualization:** Integrated `matplotlib` to plot the coordinate grid, weighted demand nodes, and the iterative descent trajectory.

## Execution Stack
* **Python 3.x**
* **NumPy** (Linear algebra & vector operations)
* **Matplotlib** (Convergence visualization)

## Future Scope
While this iteration utilizes Euclidean geometry (a highly accurate flat-plane approximation at the city level), future updates to the engine will incorporate:
1. **The Haversine Formula:** To account for the curvature of the Earth over global deployment scales.
2. **3D Topographical Constraints:** Incorporating altitude (Z-axis) constraints to navigate high-rise infrastructure and restricted airspace.
3. **Dynamic Demand Weighting:** Replacing static historical weights with real-time API feeds (traffic, weather, emergency spikes) for live network recalibration.

---
*Engineered for rapid-response logistics and predictive infrastructure planning.*
