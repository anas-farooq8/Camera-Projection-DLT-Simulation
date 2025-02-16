# Camera-Projection-DLT-Simulation

## Overview

This repository presents a rigorous Python-based simulation for camera forward projection and parameter estimation utilizing the Direct Linear Transform (DLT) algorithm. The simulation systematically examines the process of projecting three-dimensional world points onto a two-dimensional image plane, estimating the camera projection matrix, and decomposing this matrix to recover intrinsic and extrinsic camera parameters. Furthermore, it incorporates stochastic noise to emulate real-world measurement inaccuracies.

## Key Features

- **Camera Parameter Definition:** Derivation of intrinsic and extrinsic camera parameters using Euler angles and translation vectors.
- **3D-to-2D Projection:** Projection of non-coplanar 3D points onto a 2D image plane via the projection matrix.
- **DLT-Based Estimation:** Computation of the camera projection matrix using a DLT framework from noisy 3D–2D correspondences.
- **Projection Matrix Decomposition:** Extraction of intrinsic parameters, rotation matrix, translation vector, and camera center from the estimated projection matrix.
- **Empirical Simulation of Real-World Scenarios:** Simulation of a structured room corner with markers across three perpendicular planes, incorporating synthetic measurement noise.
- **Graphical Representation:** Interactive visualization of 3D world points and corresponding 2D image projections, supplemented by error analysis.

## Installation Instructions

### Repository Cloning

```bash
git clone https://github.com/yourusername/Camera-Projection-DLT-Simulation.git
cd Camera-Projection-DLT-Simulation
```

### Software Dependencies

- Python
- Required Libraries: `numpy`, `matplotlib`, `scipy`

```bash
pip install numpy matplotlib scipy
```

## Functional Modules

### `create_rotation_matrix(yaw, pitch, roll)`

Generates a 3×3 rotation matrix derived from specified Euler angles (yaw, pitch, roll).

### `createGTCameraParameters(focal_length_x, focal_length_y, principal_point_x, principal_point_y, R, camera_translation_vector_from_world_origin)`

Computes the ground truth intrinsic matrix **K**, extrinsic matrix **[R | t]**, and projection matrix **P**.

### `project_world_to_camera(points_3d, P, image_width, image_height)`

Projects 3D world coordinates to a 2D image plane using projection matrix **P**. Outputs normalized 2D image coordinates and a boolean mask indicating boundary constraints.

### `find_projection_matrix(world_points, image_points)`

Employs the DLT algorithm to estimate the projection matrix from 3D–2D correspondences using singular value decomposition (SVD), with subsequent scaling and sign adjustments.

### `decompose_projection_matrix(P)`

Decomposes a 3×4 projection matrix into intrinsic parameters, a rotation matrix **R**, translation vector **t**, and camera center **C** using RQ decomposition.

### `plotWorldPoints(ax, points, rotation_matrix, camera_origin)`

Visualizes 3D world points alongside the camera coordinate system.

### `plotImagePixelPoints(ax, image_points, image_width, image_height)`

Plots 2D image points while adjusting for the image coordinate system’s origin (top-left).

## Experimental Framework

### **Task 1: Camera Forward Projection Simulation**

#### Objective:

To compute and visualize the projection of predefined 3D points onto a 2D image plane using a known projection matrix.

#### Methodology:

1. Define 3D world points and camera parameters.
2. Construct the ground truth projection matrix **P**.
3. Compute the 2D image coordinates of projected 3D points.
4. Visualize the spatial configuration and projected image points.

### **Task 2: Camera Projection Matrix Estimation via DLT**

#### Objective:

To derive the camera projection matrix from noisy 3D–2D correspondences using the DLT algorithm.

#### Methodology:

1. Utilize the observed noisy 2D projections and corresponding 3D world points.
2. Construct the DLT-based system of equations and solve via SVD.
3. Normalize and refine the computed projection matrix.
4. Compare the estimated **P** with the reference **P**.

### **Task 3: Projection Matrix Decomposition and Error Analysis**

#### Objective:

To extract intrinsic and extrinsic parameters from the estimated projection matrix and assess reprojection accuracy.

#### Methodology:

1. Decompose the estimated **P** via RQ factorization.
2. Utilize the estimated projection matrix to reconstruct 2D image points.
3. Compute the Euclidean reprojection error between observed and reconstructed 2D points.
4. Visualize comparative discrepancies in reprojections.
