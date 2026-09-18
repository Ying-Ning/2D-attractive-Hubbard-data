# 2D attractive Hubbard model data

Data for *Characterizations of the superconducting ground state in two-dimensional attractive Hubbard model*.

This repository contains finite-size PQMC data for the two-dimensional attractive Hubbard model, selected twist-averaged boundary condition (TABC) data, and processed data used for Figures 1, 8, and 9 of the paper.

## Directory structure

```text
.
├── FInite-size-Result/
│   └── U{U}n{n}/
│       ├── Energy.txt
│       ├── Dble-Occupancy.txt
│       ├── Condensate-Fraction.txt
│       ├── Kspace-Pair-Structure-Factor.txt
│       └── Rspace-Pair-Correlation-Function/
│           └── Rspace-Pair-Correlation-Function-L{L}.txt
├── Data-for-figure1/
├── Data-for-figure8/
└── Data-for-figure9/
```

The capitalization of `FInite-size-Result` is retained exactly as it appears in the repository. Parameter directories follow the naming convention `U{U}n{n}`. For example, `U4n0.625` denotes U/t=4 and n=0.625.

The main parameter grid is:

- U/t=2,4,6,8,10,12;
- n=0.250,0.375,0.500,0.625,0.750,0.875,1.000;
- L=4,8,12,16,20,24.

## Finite-size data

Each parameter directory contains the following five types of physical data:

- `Energy.txt`: energy;
- `Dble-Occupancy.txt`: double occupancy;
- `Condensate-Fraction.txt`: condensate fraction;
- `Kspace-Pair-Structure-Factor.txt`: momentum-space pair structure factor, normalized by L^2;
- `Rspace-Pair-Correlation-Function/`: real-space pair correlation functions.

### Summary data format

Files containing only periodic boundary condition (PBC) data have the following format:

```text
L              PBC-ave                PBC-err
4             -2.95468337e+00         1.58140473e-03
...
```

Files containing TABC data have the following format:

```text
L              PBC-ave                PBC-err                TABC-ave               TABC-err
4             -1.73158147e+00         8.04957634e-05
8             -1.70016971e+00         4.74734868e-05        -1.69348087e+00         6.25319198e-04
...
```

TABC columns are currently available for the following parameters:

- U/t=2: n=0.250,0.375,0.500,0.625,0.750,0.875;
- U/t=4: n=0.250,0.375,0.500,0.625;
- U/t=6: n=0.250.

### Real-space pair correlation functions

The `Rspace-Pair-Correlation-Function/` directory contains one file for each system size:

```text
Rspace-Pair-Correlation-Function-L4.txt
Rspace-Pair-Correlation-Function-L8.txt
...
Rspace-Pair-Correlation-Function-L24.txt
```

Each file contains six columns and has no header. The first two columns specify the spatial indices, the middle two give the mean and statistical error of the real-space pair-correlation function, and the final two give the mean and statistical error of the vertex contribution to the real-space pair-correlation function. Each file for a system of linear size L contains L^2 rows.

## The `inf` row

In `Energy.txt` and `Dble-Occupancy.txt`, an `inf` row denotes an L -> infinity estimate obtained from the largest system sizes judged to have converged. The last three available sizes are tested first. If those three points do not pass, the last two sizes are tested. Every pair of selected points must satisfy

```text
|x_i-x_j| < 3 * (err_i + err_j)
```

When the convergence criterion is satisfied, the `inf` average and error are the arithmetic means of the selected averages and error bars, respectively:

```text
x_inf = (1/N) * sum_i(x_i)
err_inf = (1/N) * sum_i(err_i)
N = 2 or 3
```

PBC and TABC data are tested independently in files containing both boundary conditions. If one side does not converge, that side of the `inf` row is left blank. For example:

```text
inf                                                         -1.69396790e+00         9.34143940e-05
```

This example indicates that only the TABC data converged. For `U2n1.000`, the `inf` values of the energy and double occupancy were obtained by extrapolating quadratic polynomial fits, rather than by applying the finite-size convergence criterion described above.

## Figure data

### `Data-for-figure1`

This directory contains ED and PQMC comparisons for four observables at n=0.625 and L=4:

```text
U/t            ED                       PQMC-ave                 PQMC-err
```

The files are `Energy.txt`, `Dble-Occupancy.txt`, `Condensate-Fraction.txt`, and `Kspace-Pair-Structure-Factor.txt`. They cover U/t=0,1,...,12.

### `Data-for-figure8`

This directory contains matrix-form data for the energy and double occupancy. The averages and errors of each observable are stored separately in `_ave.txt` and `_err.txt` files. Rows correspond to U/t, and columns correspond to particle density n.

### `Data-for-figure9`

This directory contains matrix-form data for the condensate fraction and momentum-space pair structure factor. Averages and errors are stored separately. Rows correspond to U/t, and columns correspond to particle density n.
