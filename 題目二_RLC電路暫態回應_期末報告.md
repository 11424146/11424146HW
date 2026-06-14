# Engineering Mathematics Final Report (Topic 2)

Class: CS A  
Student ID: `11424146`  
Name: `鄭沂加`  
Date: 2026/06/14

---

## Topic 2: Transient Response of a Series RLC Circuit

### 1. Problem

Switch-mode power supplies often use a series **RLC filter** on the output side.  
At `t=0`, a DC source is connected to the circuit.  
The capacitor and inductor start from zero energy.

Given:

- `R = 8 Ω`
- `L = 1 H`
- `C = 0.25 F`
- `Us = 12 V`
- `u_C(0) = 0 V`
- `i_L(0) = 0 A`

Goal: find the capacitor voltage `u_C(t)` for `t >= 0` using Laplace transform, and explain the transient behavior.

---

### 2. Assumptions

1. All elements are ideal (linear `R`, `L`, `C`).  
2. The circuit is series-connected: source, resistor, inductor, capacitor.  
3. The input is a step voltage: `Us u(t)`.  
4. Initial capacitor voltage and inductor current are both zero.  
5. Current direction follows the usual sign convention for series RLC analysis.

---

### 3. Differential Equation

For a series RLC circuit:

$$
L\frac{di}{dt}+Ri+u_C=U_s
$$

Also,

$$
i=C\frac{du_C}{dt}
$$

Substitute into the KVL equation:

$$
LC\frac{d^2u_C}{dt^2}+RC\frac{du_C}{dt}+u_C=U_s
$$

With the given values:

$$
0.25\frac{d^2u_C}{dt^2}+2\frac{du_C}{dt}+u_C=12
$$

Multiply both sides by `4`:

$$
\frac{d^2u_C}{dt^2}+8\frac{du_C}{dt}+4u_C=48
$$

Initial conditions:

$$
u_C(0)=0,\quad \frac{du_C}{dt}(0)=0
$$

Check damping:

$$
\omega_0=\frac{1}{\sqrt{LC}}=2\text{ rad/s},\quad
\alpha=\frac{R}{2L}=4,\quad
\zeta=\frac{\alpha}{\omega_0}=2>1
$$

So the system is **overdamped** (no oscillation).

---

### 4. Laplace Transform Solution

Take Laplace transform of

$$
LCu_C''+RCu_C'+u_C=U_s
$$

with zero initial conditions:

$$
U_C(s)(LCs^2+RCs+1)=\frac{U_s}{s}
$$

Substitute `L=1`, `C=0.25`, `R=8`, `Us=12`:

$$
U_C(s)=\frac{12}{s(0.25s^2+2s+1)}
=\frac{48}{s(s^2+8s+4)}
$$

Factor the quadratic:

$$
s^2+8s+4=(s+4-2\sqrt3)(s+4+2\sqrt3)
$$

Let

$$
s_1=-4+2\sqrt3,\quad s_2=-4-2\sqrt3
$$

Partial fractions:

$$
\frac{48}{s(s-s_1)(s-s_2)}
=\frac{A}{s}+\frac{B}{s-s_1}+\frac{C}{s-s_2}
$$

Solve:

$$
A=12,\quad
B=-4\sqrt3-6,\quad
C=2\sqrt3-3
$$

So

$$
U_C(s)=\frac{12}{s}+\frac{-4\sqrt3-6}{s+4-2\sqrt3}+\frac{2\sqrt3-3}{s+4+2\sqrt3}
$$

Inverse Laplace transform:

$$
u_C(t)=12+(-4\sqrt3-6)e^{(-4+2\sqrt3)t}+(2\sqrt3-3)e^{(-4-2\sqrt3)t},\quad t\ge 0
$$

Numerically:

$$
u_C(t)=12-12.928e^{-0.536t}+0.928e^{-7.464t}\text{ V}
$$

---

### 5. Meaning of the Result

1. **Steady state**  
   When `t → ∞`, both exponential terms go to zero, so

   $$
   \lim_{t\to\infty}u_C(t)=12\text{ V}=U_s
   $$

   The capacitor is fully charged to the source voltage.

2. **Transient shape**  
   Because `ζ=2>1`, the response has no overshoot.  
   Voltage rises smoothly from `0 V` to `12 V`.

3. **Two time constants**  
   - Slow mode: `1/|s_1| ≈ 1.87 s`  
   - Fast mode: `1/|s_2| ≈ 0.134 s`  

   The slow mode mainly decides how long the circuit needs to reach steady state.

4. **Engineering use**  
   In power-supply filtering, this model helps us estimate output settling time and choose `R`, `L`, and `C` values.

---

### 6. Example

Use the given parameters and evaluate at several times:

| `t (s)` | `u_C(t) (V)` |
|--------:|-------------:|
| 0.5     | 2.13         |
| 1.0     | 4.44         |
| 2.0     | 7.57         |
| 5.0     | 11.11        |

At `t=5 s`, the voltage is already about `92.6%` of the final value `12 V`.  
Because the system is overdamped, the curve rises quickly at first, then slows down near `12 V`.

Check initial conditions:

$$
u_C(0)=12-12.928+0.928=0
$$

$$
\frac{du_C}{dt}(0)=(-4\sqrt3-6)(-4+2\sqrt3)+(2\sqrt3-3)(-4-2\sqrt3)=0
$$

Both match the problem statement.

---

### 7. Conclusion

This second-order RLC circuit can be modeled by a linear ODE and solved efficiently with Laplace transform.  
The final answer shows that capacitor voltage starts at zero and approaches the DC source voltage without oscillation.  
For filter design, increasing `R` or changing `L`, `C` will change damping and settling time, but the basic analysis method stays the same.

Final answer:

$$
u_C(t)=12+(-4\sqrt3-6)e^{(-4+2\sqrt3)t}+(2\sqrt3-3)e^{(-4-2\sqrt3)t},\quad t\ge 0
$$

---

## References

1. Course notes: second-order circuits, Laplace transform, and transient response.  
2. Format reference: [題目二_降落傘終端速度_期中報告.md](./題目二_降落傘終端速度_期中報告.md)  
3. Problem source: [工程數學 期末報告 題目.docx](./工程數學%20期末報告%20題目.docx)
