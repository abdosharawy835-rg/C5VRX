# Breadboard wiring — step by step

## Netlist

```text
XIAO D4 / GPIO23 ---[ 8.2 kΩ ]---+
XIAO D5 / GPIO24 ---[ 3.9 kΩ ]---+
XIAO D6 / GPIO11 ---[ 2.0 kΩ ]---+
XIAO D7 / GPIO12 ---[ 1.0 kΩ ]---+---- CVBS_NODE ----> Yellow RCA centre (VIDEO)
XIAO D8 / GPIO8  ---[ 470 Ω   ]---+
XIAO D9 / GPIO9  ---[ 240 Ω   ]---+
                                  |
                               [ 200 Ω ]
                                  |
XIAO GND -------------------------+----> RCA shield (GND)
```

## Physical layout tips

- Use one dedicated breadboard row as `CVBS_NODE`.
- Put one resistor lead from each D-pin jumper into that row.
- Put the other lead of each resistor into a separate row connected to its
  matching XIAO pin jumper.
- Put the 200 Ω resistor from `CVBS_NODE` to the ground rail.
- Jumper XIAO GND to the ground rail.
- Avoid long loose wires; keep the six DAC branches short and tidy.

## Before power

With the XIAO unplugged:
1. Measure the six resistors and the 200 Ω load.
2. Check continuity from each DAC pin jumper to `CVBS_NODE` through its own
   resistor.
3. Check that `CVBS_NODE` is not shorted directly to GND or 3V3.
4. Check that the RCA shield is connected to the same GND rail.

The six bit branches must remain in the exact order shown. Do not connect the
optional 470 pF capacitor for the first prototype.
