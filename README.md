# 1D-Bar-Vibration

# Detailed Comments and Theory on the Vibration and Structural Analysis Codes

## Theory Behind the Code

This code implements finite element and finite difference methods to analyze the dynamic behavior of various mechanical systems, including a 1D bar, a beam, and a rectangular plate. The analyses include the computation of natural frequencies, mode shapes, and time-domain responses.

---

### 1D Bar Analysis (Axial Vibration)

#### Governing Equations:
- **Stiffness Matrix (Local):**
  \[
  k_e = \frac{E A}{L_e} \begin{bmatrix}
  1 & -1 \\
  -1 & 1
  \end{bmatrix}
  \]

- **Mass Matrix (Local):**
  \[
  m_e = \frac{\rho A L_e}{6} \begin{bmatrix}
  2 & 1 \\
  1 & 2
  \end{bmatrix}
  \]

#### Assembly and Boundary Conditions:
- The global stiffness and mass matrices are assembled from the local element matrices.
- Boundary conditions, such as fixing one end of the bar, reduce the size of the matrices.

#### Natural Frequencies and Mode Shapes:
- Solve the generalized eigenvalue problem:
  \[
  K \phi = \lambda M \phi
  \]
  - Natural frequencies: \( \omega = \sqrt{\lambda} \).
  - Mode shapes: Corresponding eigenvectors \( \phi \).

#### Visualization:
- Mode shapes are plotted along the length of the bar.

---

### Beam Analysis (Euler-Bernoulli Beam)

#### Governing Equations:
- **Stiffness Matrix (Local):**
  \[
  K_e = \frac{E I}{L_e^3} \begin{bmatrix}
  12 & 6L_e & -12 & 6L_e \\
  6L_e & 4L_e^2 & -6L_e & 2L_e^2 \\
  -12 & -6L_e & 12 & -6L_e \\
  6L_e & 2L_e^2 & -6L_e & 4L_e^2
  \end{bmatrix}
  \]

- **Mass Matrix (Local):**
  \[
  M_e = \frac{\rho A L_e}{420} \begin{bmatrix}
  156 & 22L_e & 54 & -13L_e \\
  22L_e & 4L_e^2 & 13L_e & -3L_e^2 \\
  54 & 13L_e & 156 & -22L_e \\
  -13L_e & -3L_e^2 & -22L_e & 4L_e^2
  \end{bmatrix}
  \]

#### Boundary Conditions:
- Fixed boundary conditions (e.g., clamped at one end) are applied by modifying the global matrices.

#### Natural Frequencies and Mode Shapes:
- Solve the generalized eigenvalue problem for the reduced matrices:
  \[
  K_{\text{reduced}} \phi = \lambda M_{\text{reduced}} \phi
  \]

#### Visualization:
- Transverse displacement mode shapes are plotted along the length of the beam.

---

### Plate Analysis (2D Finite Difference Approximation)

#### Governing Equations:
- For a membrane, the eigenvalue problem is:
  \[
  K w = \lambda M w
  \]
  - Stiffness matrix \( K \) approximates \(-T \nabla^2\).
  - Mass matrix \( M \) is lumped for simplicity.

#### Finite Difference Assembly:
- Discretize the domain using a 5-point Laplacian scheme:
  \[
  K[i, j] = \begin{cases}
  4 & \text{if } i=j \\
  -1 & \text{if } i \text{ and } j \text{ are neighbors}
  \end{cases}
  \]

#### Boundary Conditions:
- Dirichlet boundary conditions enforce zero displacement at edges by assigning large values to corresponding stiffness entries.

#### Natural Frequencies and Mode Shapes:
- Solve the eigenvalue problem for the global matrices.
  - Natural frequencies: \( \omega = \sqrt{\lambda} \).
  - Mode shapes: Eigenvectors reshaped into 2D grids.

#### Visualization:
- Contour plots of mode shapes over the plate surface.

---

### Summary of Key Results
- **1D Bar:** Natural frequencies and axial mode shapes.
- **Beam:** Natural frequencies and transverse displacement mode shapes.
- **Plate:** Natural frequencies and 2D mode shapes (membrane behavior).

This code provides a robust framework for understanding and visualizing the dynamic behavior of structures modeled using finite element and finite difference methods.
