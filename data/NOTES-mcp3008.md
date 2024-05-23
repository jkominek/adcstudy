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

also maybe try resistors with low excess noise.

mcp3008_3V3_3V3_12750Hz_mcp6v84_1800_mic5266@2V
  * hammer peak 491
  * hammer background
    * mean 11.1 sdev 2.08
  * keystick peak 345ish
  * keystick background
    * mean 52.06 sdev 1.95

well the 6V84 seems worse in most every way. not holding out much
hope for the 6H84, as it seems to demonstrate noise even when
disconnected from signal.

mcp3008_5V_5V_12750Hz_mcp6h84_1800_mic5266@2V
  * hammer peak 353
  * hammer background
    * mean 7.59 sdev 1.97
  * keystick peak 475ish
  * keystick background
    * mean 67.79 sdev 2.18

the 6H84 needs to be run at a higher voltage to behave right.
even so, performance isn't great. lots of noise. i'm wondering
if the additional gain just means it can amplify noise that the
others don't pass through. would it be helped with some filtering
capacitance?


this does suggest that the TIA helps, with a significant reduction
in background, and a slight one in noise. and reducing/eliminating
background signal is good, because it lets us detect the start of
motion that much sooner, and more accurately.

seems to be worth continuing some tests with the TIAs. having seen
the performance of the 6V84 and 6H84, i'm interested in looking for
low-noise, low-input bias opamps, basically without regard for
their bandwidth. slew rate is nearly inconsequential, it looks
like we're slewing at 0.0001 V/us in our current test data. i don't
think they've ever made opamps with that little slew.
