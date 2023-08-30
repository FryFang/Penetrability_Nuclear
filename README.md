# Penetrability_Nuclear
Calculate the penetrability and the single-particle partial width for a nuclear reaction assuming the particle experiences Coulomb potential of a point nucleus.

## Pacakge requirements:
1. NumPy
2. mpmath

## Background:
Consider the three-dimensional time-independent Schr&ouml;dinger equation

```math
\frac{\hbar}{2m}(\frac{\partial^2 \psi}{\partial x^2} + \frac{\partial^2 \psi}{\partial y^2} + \frac{\partial^2 \psi}{\partial z^2}) + V(x,y,z) \psi = E \psi.
```

For a central pontential $V(r)$, we can replace the cartesian coordinate $x$, $y$, and $z$ with the spherical coordinates $r$, $\theta$, and $\phi$. The wave function $\psi$ can then be separated into three different functions $\psi(r, \theta, \phi) = R(r) \Theta(\theta) \Phi(\phi)$. This makes the Schr&oumldinger equation to be separable as well and we have three sets of differential equations for the radial and angular portions. The product of the two angular portions are the *spherical harmonics*[^1].

For the radial differential equation 
```math
\frac{\hbar}{2m}(\frac{d^2 R}{dr^2} + \frac{2}{r} \frac{d R}{dr}) + [V(r) + \frac{l(l+1)\hbar^2}{2mr^2}]R = ER.
```
If we substitute $rR(r)$ with $u(r)$, the equation can be re-written as
```math
\frac{d^2 u_l}{dr^2} + \frac{2m}{\hbar^2}[E - V(r) - \frac{l(l+1)\hbar^2}{2mr^2}]u_l = 0,
```
or if one replace $E$ with $p^2/(2m) = \hbar^2 k^2/(2m)$
```math
\frac{d^2 u_l}{dr^2} + [k^2 - \frac{l(l+1)}{r^2} - \frac{2m}{\hbar^2} V(r)]u_l = 0
```
Now we can use the Coulomb potential $V(r) = \frac{Z_p Z_t e^2}{r}$, and define two new dimensionless parameters $\rho = Kr = 0.218735r\sqrt{\mu E}$ and $\eta = 0.157489 Z_p Z_t \sqrt{\mu/{E}}$, where the subscript $p$ and $t$ represent projectile and target respectively, and $\mu$ is the reduced mass. The equation finally turned into
```math
\frac{d^2 u_l}{d\rho^2} + [1 - \frac{l(l+1)}{\rho^2} - \frac{2 \eta}{\rho}]u_l = 0
```
The solutions to this differential equation are the regular and irregular Coulomb functions, $F_l(\eta, \rho)$ and $G_l(\eta, \rho)$ respectively. The details of each functions can be seen here[^2]. These two functions should also satisfy the Wronskian relation
```math
F_l' G_l - F_l G_l' = 1 \;\mathrm{and}\; F_l G_{l+1} - F_{l+1} G_l = 1/R_{l+1},
```
where
```math
R_l = \sqrt{(l^2+\eta^2)}/l.
```

Note: The single-partical partial width calculation here only considers the Coulomb potential, but for a more realistic situation, the Wood-Saxon potential should be used.

[^1]: [Spherical Harmonic](https://mathworld.wolfram.com/SphericalHarmonic.html)
[^2]: [Coulomb Wave Function](https://mathworld.wolfram.com/CoulombWaveFunction.html)
