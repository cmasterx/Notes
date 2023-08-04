# Coils
Design considerations for devices that uses inductors as a significant component for its functionality, such as:
- Motors
- Relays

# Flyback Diode
Flyback diodes are required so that when the inductor is switched off, the current within the inductor (a.k.a. **_kickback_**) can discharge using itself rather than the current discharging back into the circuit.

## Implementations
### Simple Flyback Diode - Naive Design
A flyback diode placed in parallel and reverse polarity to the inductor protects the circuit from kickback. However, a simple flyback diode is non-ideal for applications requiring fast response. Due to the forward voltage drop of a flyback diode, energy dissipation to heat is limited to the forward drop voltage (on a conventional diode, this is **~0.7V**).

### Series Resistor with Flyback Diode
Placing a resistor in series to the flyback diode allows a higher voltage difference between the two ends of an inductor during the _off_ state. The flyback diode will still induce a forward voltage drop. However in addition to the diode voltage drop, the resistor will dissipate heat with:

$$
W_I = W_D + W_R
$$

$$
W_D = V_D*I_I
$$

$$
W_R = V_R*I_I
$$

$$
V_R = (V_I-V_D) * R_R
$$

where:
- $I_I$ = is the current through the inductor
- $W_I$ is the heat dissipation of the whole system (i.e. the inductor and all components)
- $W_D$ is the heat dissipation (in Watts) induced by the flyback diode
- $W_R$ is the heat dissipation (in Watts) induced by the series resistor
- $V_I$ is the voltage difference of the inductor
- $V_D$ is the forward voltage drop (in Volts) of the flyback diode
- $V_R$ is the voltage induced on the series resistor
- $R_R$ is the resistance value of the series resistor

All three equations must satisfy to determine the expected heat dissipation $W_I$.

### Zenner Diode in Series with Flyback Diode
Placing a Zenner diode, polarized to the same direction as the input voltage to the inductor, in series with the flyback diode induces a heat dissipation of:

$$
W_I = W_Z + W_D
$$

where $W_Z$ is the heat dissipation induced by the Zenner diode. The heat dissipation of the Zenner diode is:

$$
W_Z = V_Z + I_I
$$

where $V_Z$ is the breakdown voltage of the Zenner diode.

Thus, the voltage difference on the inductor while there is sufficient energy within the inductor, $V_I$ is:
$$
V_I = V_Z + V_D
$$

Careful consideration is required in selecting a Zenner diode for the system to ensure that $V_Z$ meets system requirements and that when there is not enough energy within the inductor to sustain the combined voltage drop of the Zenner forward voltage and flyback diode voltage drop, $V_I$, the circuit can handle the oscillation kickback, $V_{oscillation}$:

$$
V_{input} - V_{kickback} \le V_{oscillation}  \le V_{input} + V_{kickback}
$$
$$
V_{kickback} < V_Z + V_D
$$

where:
- $V_{input}$ is the input voltage induced on the inductor during the _on_ state
- $V_{kickback}$ is the maximum voltage that $V_{input}$ can oscillate

$V_{kickback}$ must be so that $V_{kickback} < V_Z + V_D$ must be satisfied because if the inductor has enough energy stored that it can theoretically sustain $V_I \ge V_Z + V_D$, the Zenenr and flyback diode will activate, clamping $V_I$ to $V_I = V_Z + V_D$.

# References
- [Flyback Diodes w/ Relays](https://electronics.stackexchange.com/questions/115857/flyback-diodes-and-relays)
- [Improving Flyback Characteristics with Resistor or Zenner Diode in Series w/ Flyback Diode](https://electronics.stackexchange.com/questions/171974/can-a-zener-diode-that-protects-a-switch-against-inductance-when-the-switch-open)
