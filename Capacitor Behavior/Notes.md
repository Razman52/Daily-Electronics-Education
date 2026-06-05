# Capacitors
Capacitors store energy in the form of a potential charge difference across their parallel plates.

In the scenario shown here ![cap-behavior](cap-behavior.png) the voltage at the node following the cap falls with each static on period of Vsource, and increases in every static off period of Vsource.
- Once the voltage switches on/off the voltage at node prior to cap drops/rises by Vsource **while the Vdrop across cap stays same**. this is why negative voltage is then seen in node 2.

**tried to do prefix for Mega, but in LTSpice that is actually '3Meg', so '3M' still means milli**.

Interesting behavior, i performed a step parameter function from 1m to 1 Ohm for every 100m, only the 1 mOhm R results in a fluctuation a visible voltage drop across C1 when on/voltage rise across C1 when Vsource off.

Check out the difference in Voltage drop across Cap, note R = 1m 10m 20m list. ![Low R List](lowRlist.png)

Increase in R results in slower Cap charging/dissipation. the Voltage across the cap is so different because of ^ R = ^ dI/dt for cap? higher time constant?![dI-behave](dI-behave.png)

Also, a larger cap = greater time to charge/discharge cap: ![Clist](Clist.png)

**they are both linearly proportional:**
Test 1) C = 100u, R = 1k
Test 2) C = 10u, R = 10k
    - same trend!

**Tau = RC**, = standard time th cap charges & discharges in RC circuit
- also equals the time it takes for cap to charge to 63.2% of its max voltage. (4Tau = 98.2%, 5Tau = 99.3%)

## C, V, Q Eqn

Q = CV, I = C(dV/dt).
Thus when the voltage is constant, cap = **open circuit **
![OpenCircuit](openCircuitBehavior.png)
Current has equivalent relationship to Voltage at node 2 (makes sense because Resistance stays constant and doesn't change)

C depends on permittivity of dielectric, Area, and distance. C = [(perm)A]/d