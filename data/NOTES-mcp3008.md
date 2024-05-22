* LM324 vs MCP6L04 @ 1800ohm
  * Hammer background level seems lower on the 6L04, keystick
    background seems lower on the LM324.

mcp3008_3V3_3V3_12750Hz_mcp6l04_1800_mic5366@2V
  * hammer peak 356
  * hammer background
    * mean  4.00 sdev 0.937
  * keystick peak 488.2
  * keystick background
    * mean 64.16 sdev 1.025

mcp3008_3V3_3V3_12750Hz_lm324_1800_mic5366@2V
  * hammer peak 357
  * hammer background
    * mean  5.97 sdev 0.950
  * keystick peak 487
  * keystick background
    * mean 61.99 sdev 1.095

so we see very slightly lower noise in the MCP6L04. hammer background
level is also lower, which is probably more important than keystick
background.

peaks are basically identical.

mcp3008_3V3_3V3_12750Hz_resistor_1800_mic5366@2V
  * hammer peak 360
  * hammer background
    * mean 6.28 sdev 0.993
  * keystick peak  lots of variability, "480s" is reasonable
  * keystick background
    * mean 67.06 sdev 0.861

hammer peak is slightly higher, but that might not be real. keystick
peak was highly variable in the sample data, but seemed consistent.

the resistor has higher background levels than the others, but improved
noise on the keystick background. so... on the inherently higher noise
task, the opamp isn't helping eliminate the noise. should we be trying
to put a tiny amount of capacitance on the TIA loop?

this does suggest that the TIA helps, with a significant reduction
in background, and a slight one in noise. and reducing/eliminating
background signal is good, because it lets us detect the start of
motion that much sooner, and more accurately.

seems to be worth continuing some tests with the TIAs. i'll try some
more expensive opamps, and should produce a rev of the board with space
for some caps in the feedback loop.
