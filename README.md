# Flow Analysis in a PWR Fuel Rod Subchannel

A cross-validated **CFD study** of turbulent coolant flow in a Pressurized Water
Reactor (PWR) fuel-rod subchannel, solved independently in **ANSYS Fluent** and
**Siemens Star-CCM+** and benchmarked against a **Darcy–Weisbach** analytical solution.

> NEM 358 — Computational Fluid Dynamics Applications · Hacettepe University, Department of Nuclear Engineering.

---

## Problem Description

In a PWR, coolant flows through narrow passages formed between four adjacent fuel
rods — the **subchannel** — where turbulence intensity and heat transfer peak.
Because the real subchannel cross-section differs from a simple circular pipe
(low-velocity regions form at the concave corners between rods), purely analytical
correlations are insufficient and CFD is required to resolve the velocity and
pressure fields.

**Geometry:** a single bare-rod subchannel of a square-lattice fuel bundle.

| Parameter | Value |
| :--- | :--- |
| Rod diameter, D | 9.5 mm |
| Rod pitch, P | 12.6 mm |
| Active height, H | 3.66 m |
| Flow area, A | 8.788 × 10⁻⁵ m² |
| Hydraulic diameter, D_h | 11.78 mm |

---

## Methodology

### Governing Equations
Steady **RANS** equations under the incompressible-flow assumption, with two
different turbulence closures:

- **Star-CCM+:** realizable k-ε
- **ANSYS Fluent:** k-ω SST

Frictional pressure drop (Darcy–Weisbach) with the **Filonenko** friction factor:

```
ΔP_friction = f · (L/D_h) · (ρV²/2)
f = (0.790·ln(Re) − 1.64)⁻²
ΔP_total = ΔP_friction + ΔP_hydro
```

### Material Properties (water, IAPWS-IF97)
Evaluated at the bulk-mean temperature `T_avg = 309.4 °C`, `P = 15.51 MPa`:
`ρ = 734.5 kg/m³`, `μ = 9.0 × 10⁻⁵ Pa·s`.

### Mesh & Boundary Conditions
- **Star-CCM+:** surface remesher + trimmed cell + prism layer mesher, ≈ 920,000 cells
- **ANSYS Fluent:** sweep method (1000 axial divisions), 5-layer inflation, ≈ 873,000 cells
- Inlet: mass flux `G = 3729 kg/m²s`, turbulence intensity 5 %
- Outlet: pressure outlet (`P_gauge = 0`); rod walls: no-slip; side faces: symmetry
- Solvers: second-order upwind; convergence at residuals ~ 10⁻⁴

---

## Key Results

* The numerical results from **two independent CFD codes** were compared against
  each other and against the **Darcy–Weisbach / Filonenko** analytical reference.
* Both codes converged to within **~1 %** of one another and of the analytical
  pressure-drop result.
* Analyzed: solution convergence, inlet-surface pressure distribution, axial
  pressure profile, total pressure drop, outlet velocity contours/vectors, and
  the hydrodynamic entrance region.

---

## Contents

- `pwr-subchannel-flow-cfd.pdf` — full project report (methodology, results, step-by-step analytical pressure drop, plant-level inputs).

## Author

**Emre Sakarya** — Nuclear Engineering, Hacettepe University (Student ID: 2230386062).
