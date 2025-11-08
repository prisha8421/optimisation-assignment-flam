**R&D/AI Assignment - Flam**


This repository contains my solution for the Research and Development / AI Assignment.
The goal of this task was to estimate unknown parameters in a given parametric equation by minimizing the L1 distance between the predicted and actual data points.

#Objective:-

To determine the unknown parameters in the following equations:

x=\left(t*\cos(\theta)-e^{M\left|t\right|}\cdot\sin(0.3t)\sin(\theta)\ +X \right )

y = \left (42 + t*\sin(\theta)+e^{M\left|t\right|}\cdot\sin(0.3t)\cos(\theta)\right)

The optimisation is performed such that the mean L1 distance (Manhattan distance) between the predicted and observed coordinates is minimized.

#Explanation & Steps :

Step 1 – Data Loading and Understanding

The dataset xy_data.csv containing observed x and 𝑦 coordinates was loaded using Pandas.
The loaded values were stored as arrays actual_x and actual_y, and combined into coordinate pairs (P_actual) for direct comparison with predicted curve points.

Step 2 – Defining Parameter Range (t-values)

Explanation:

A set of t values was uniformly sampled between 6 and 60. 
The number of points sampled (1500) matches the number of points in the dataset. 
This array of t values is used to generate the predicted curve's point cloud. Since the original data is an unordered, there is no 1-to-1 correspondence between this t array and the xy_data.

Step 3 – Formulating the Objective (Cost) Function

Explanation:

The optimization objective was to minimize the mean L1 distance between predicted and actual curve points.
The L1 metric was chosen intentionally, since it is robust to outliers and directly measures absolute deviation.
For every predicted point, its L1 distance to all actual points was calculated, and only the minimum (closest) one was considered.
The formula used:

Loss_L1 = (1/N) * sum_{i=1 to N} ( min_{1 <= j <= N} ( |x_pred,i - x_actual,j| + |y_pred,i - y_actual,j| ) )

Step 4 – Defining the Model Equation

Explanation:

The given parametric equation was implemented in terms of 

x = t*\cos(\theta) - e^{M\left|t\right|}\cdot\sin(0.3t)\sin(\theta) + X

y = 42 + t*\sin(\theta) + e^{M\left|t\right|}\cdot\sin(0.3t)\cos(\theta)

These equations were used inside the cost function to generate predicted x andy points for comparison with the dataset.

Step 5 – Optimization Technique

Explanation:

The Differential Evolution algorithm (from scipy.optimize) was chosen because it performs global optimization efficiently for nonlinear equations.
It evolves multiple candidate solutions using mutation, recombination, and selection to minimize the cost function.

The parameter search bounds were:

θ: 0° to 50° (converted to radians during optimisation)

M: -0.05 to 0.05

X: 0 to 100

This ensured realistic and bounded search behavior.

Step 6 – Running the Optimizer

Explanation:

The optimizer iteratively minimized the mean L1 distance.

A population size of 10 and tolerance of 10^-4 were used for balanced accuracy and runtime.
The algorithm displayed progress and returned the best-fit parameters once convergence was achieved.

Step 7 – Obtaining and Presenting Results

Explanation:

Upon successful optimization, the optimal values of unknowns θ,M,X were printed in both radians and degrees
The final minimized Mean L1 Distance and optimized equation was reported as the performance metric.

Step 8 – Visualization and Verification

Explanation:

To verify correctness, the predicted curve (in red) and original data (in blue) were plotted using Matplotlib.
A close visual overlap confirmed that the optimizer successfully minimized the L1 distance and captured the data pattern effectively.

#Results:-

Final optimized result (submission-ready format):

\left(t*\cos(0.523594)-e^{0.030001\left|t\right|}\cdot\sin(0.3t)\sin(0.523594)\ +54.998555,42+\ t*\sin(0.523594)+e^{0.030001\left|t\right|}\cdot\sin(0.3t)\cos(0.523594)\right)

θ = 0.523594

M = 0.030001

X = 54.998555

Desmos representation of the final result :

https://www.desmos.com/calculator/3y9swdeuff

#Tools:-

This solution was developed in Python and relies on several key open-source libraries and algorithms.

Pandas

NumPy

SciPy

Matplotlib

Differential Evolution Algorithm: SciPy’s Differential Evolution algorithm was used for global optimization due to its robustness in non-linear, non-convex problems.

#References:- 

1. Ahmad, M. F., Isa, N. A. M., Lim, W. H., & Vembar, R. S. (2022). Differential evolution: A recent review based on state-of-the-art works. Alexandria Engineering Journal, 61(5), 3831–3872.

2. SciPy. `differential_evolution` – [Official Documentation](https://docs.scipy.org/doc/scipy/reference/generated/scipy.optimize.differential_evolution.html)

3. MathWorks. Differential Evolution Overview – [https://www.mathworks.com/help/gads/differential-evolution.html](https://www.mathworks.com/help/gads/differential-evolution.html)





