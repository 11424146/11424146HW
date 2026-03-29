# Engineering Mathematics - HW1

## 1. Separable Variables
**Q4:** Solve $\frac{dy}{dx} = y \ln y$

**Solution:**
Separate variables:
$$\frac{1}{y \ln y} dy = dx$$

Integrate:
$$\int \frac{1}{y \ln y} dy = \int dx$$

Let $u = \ln y$, $du = \frac{1}{y} dy$:
$$\int \frac{1}{u} du = \int dx$$
$$\ln|\ln y| = x + C$$

Let $c_1 = \pm e^C$:
$$\ln y = c_1 e^x$$
$$y = e^{c_1 e^x}$$

---

## 2. Euler-Cauchy Equation
**Q14:** Solve $x^2 y'' + 3xy' + y = 0$

**Solution:**
Let $y = x^m$. Then:
$y' = m x^{m-1}$
$y'' = m(m-1)x^{m-2}$

Substitute:
$$x^2(m(m-1)x^{m-2}) + 3x(mx^{m-1}) + x^m = 0$$
$$x^m (m^2 + 2m + 1) = 0$$

Characteristic equation:
$$(m+1)^2 = 0$$

Repeated root $m = -1$. General solution:
$$y(x) = c_1 x^{-1} + c_2 x^{-1} \ln x$$
