# 2D attractive Hubbard model data

Data for *Characterizations of the superconducting ground state in two-dimensional attractive Hubbard model*.

This repository contains finite-size PQMC data for the standard two-dimensional attractive Hubbard model and its extension with $t_2$ hopping, selected twist-averaged boundary condition (TABC) data, and processed data used for Figures 1, 8, and 9 of the paper.

## Directory structure

```text
.
├── Standard-Hubbard-Model/
│   └── U{U}n{n}/
│       ├── Total-Energy-Density.txt
│       ├── Dble-Occupancy.txt
│       ├── Condensate-Fraction.txt
│       ├── Mean-squared-Pairing-Order.txt
│       └── Rspace-Pair-Correlation-Function/
│           └── Rspace-Pair-Correlation-Function-L{L}.txt
├── t2-Hubbard-Model/
│   └── U6n0.875/
│       └── t2_{value}/
│           ├── Total-Energy-Density.txt
│           ├── Dble-Occupancy.txt
│           ├── Condensate-Fraction.txt
│           ├── Mean-squared-Pairing-Order.txt
│           └── Rspace-Pair-Correlation-Function/
│               └── Rspace-Pair-Correlation-Function-L{L}.txt
├── Data-for-figure1/
├── Data-for-figure8/
└── Data-for-figure9/
```

`Standard-Hubbard-Model/` contains the finite-size results for the standard Hubbard model, while `t2-Hubbard-Model/` contains results for the Hubbard model with $t_2$ hopping. Parameter directories follow the naming convention `U{U}n{n}`. For example, `U4n0.625` denotes $U/t=4$ and $n=0.625$.

The main parameter grid is:

- $U/t=2,4,6,8,10,12$;
- $n=0.250,0.375,0.500,0.625,0.750,0.875,1.000$;
- $L=4,8,12,16,20,24$.

## Standard Hubbard model: finite-size data

Each parameter directory contains the following five types of physical data:

- `Total-Energy-Density.txt`: total energy density;
- `Dble-Occupancy.txt`: double occupancy;
- `Condensate-Fraction.txt`: condensate fraction;
- `Mean-squared-Pairing-Order.txt`: mean-squared pairing order;
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

- $U/t=2$: $n=0.250,0.375,0.500,0.625,0.750,0.875$;
- $U/t=4$: $n=0.250,0.375,0.500,0.625$;
- $U/t=6$: $n=0.250$.

### Real-space pair correlation functions

The `Rspace-Pair-Correlation-Function/` directory contains one file for each system size:

```text
Rspace-Pair-Correlation-Function-L4.txt
Rspace-Pair-Correlation-Function-L8.txt
...
Rspace-Pair-Correlation-Function-L24.txt
```

Each file contains six columns and has no header. The first two columns specify the spatial indices, the middle two give the mean and statistical error of the real-space pair-correlation function, and the final two give the mean and statistical error of the vertex contribution to the real-space pair-correlation function. Each file for a system of linear size $L$ contains $L^2$ rows.

## Hubbard model with t2 hopping

The currently available summary data are for U/t=6 and n=0.875, with t2=-0.45,-0.30,-0.15,0.15,0.30,0.45. The corresponding directories are named `t2_{value}`. Each parameter directory contains the following five types of physical data:

- `Total-Energy-Density.txt`: total energy density;
- `Dble-Occupancy.txt`: double occupancy;
- `Condensate-Fraction.txt`: condensate fraction;
- `Mean-squared-Pairing-Order.txt`: mean-squared pairing order.
- `Rspace-Pair-Correlation-Function/`: real-space pair correlation functions.

## The `inf` row

In `Total-Energy-Density.txt` and `Dble-Occupancy.txt`, an `inf` row denotes an $L\to\infty$ estimate obtained from the largest system sizes judged to have converged. The last three available sizes are tested first. If those three points do not pass, the last two sizes are tested. For both observables, the difference between every pair of selected points must satisfy

$$
\left|x_i-x_j\right| < 2\left(\mathrm{err}_i+\mathrm{err}_j\right).
$$

When the convergence criterion is satisfied, the `inf` average and error are the arithmetic means of the selected averages and error bars, respectively:

$$
\begin{aligned}
x_\infty &= \frac{1}{N}\sum_i x_i, \\
\mathrm{err}_\infty &= \frac{1}{N}\sum_i \mathrm{err}_i, \\
N &\in \{2,3\}.
\end{aligned}
$$

PBC and TABC data are tested independently in files containing both boundary conditions. If one side does not converge, that side of the `inf` row is left blank. For example:

```text
inf                                                         -1.69396790e+00         9.34143940e-05
```

This example indicates that only the TABC data converged. For `U2n1.000`, the `inf` values of the energy and double occupancy were obtained by extrapolating quadratic polynomial fits, rather than by applying the finite-size convergence criterion described above.

For `Condensate-Fraction.txt` and `Mean-squared-Pairing-Order.txt`, the `inf` values are thermodynamic-limit estimates obtained by finite-size extrapolation. Linear fits are used for U/t=2 and n=0.250--0.875, whereas quadratic polynomial fits are used for all other parameter sets. When TABC data are available, the extrapolation combines the TABC results with PBC results from system sizes larger than the largest size accessible in the TABC calculations. This procedure is justified by the agreement between the TABC and PBC results under the adopted error-bar criterion at the largest TABC size.

For example, for U/t=4 and n=0.500, the largest TABC calculation is at L=16. The condensate-fraction results are

```text
L              PBC-ave                PBC-err                TABC-ave               TABC-err
16             1.74773914e-01         1.16479883e-04         1.75613750e-01         4.28767336e-04
```

The difference satisfies the criterion of being smaller than twice the sum of the two error bars:

$$
\begin{aligned}
\left|x_{\mathrm{PBC}}-x_{\mathrm{TABC}}\right|
&= 8.39836000\times10^{-4} \\
&< 2\left(\mathrm{err}_{\mathrm{PBC}}+\mathrm{err}_{\mathrm{TABC}}\right)
= 1.09049444\times10^{-3}.
\end{aligned}
$$

The two results therefore agree within the adopted error-bar criterion, allowing the larger PBC results at L=20 and L=24 to be included in the extrapolation. No extrapolated value is currently tabulated for `U2n0.250`, so the corresponding `inf` rows remain blank.

## Figure data

### `Data-for-figure1`

This directory contains ED and PQMC comparisons for four observables at $n=0.625$ and $L=4$:

```text
U/t            ED                       PQMC-ave                 PQMC-err
```

The files are `Total-Energy-Density.txt`, `Dble-Occupancy.txt`, `Condensate-Fraction.txt`, and `Mean-squared-Pairing-Order.txt`. They cover $U/t=0,1,\ldots,12$.

### `Data-for-figure8`

This directory contains matrix-form data for the total energy density and double occupancy. The averages and errors of each observable are stored separately in `_ave.txt` and `_err.txt` files. Rows correspond to $U/t$, and columns correspond to particle density $n$.

### `Data-for-figure9`

This directory contains matrix-form data for the condensate fraction and mean-squared pairing order. Averages and errors are stored separately. Rows correspond to $U/t$, and columns correspond to particle density $n$.
