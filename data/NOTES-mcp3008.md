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

resistors were RC0805FR-071K8P

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



mcp3008_3V3_3V3_12750Hz_resistor_2870tf_mic5366@2V
  * hammer peak 554
  * hammer background
    * mean 10.63 sdev 1.01
  * keystick peak 770ish (lots of variability in underlying signal)
  * keystick background
    * mean 105.5 sdev 1.06

resistors were RG1608P-2871-D-T5

okay, here's another resistor board using 2870 ohm, thin film resistors.
they were chosen for low excess noise. the value was chosen to try and
use more of the range of the ADC. based on the 1800 resistor board,
all the values should be 1.595 times larger. so how'd we do? hammer
peak is a little lower than expected, keystick seems spot on.
hammer background was 0.6 higher than expected, hammer sdev was 2/3rds
of expected. keystick background was 1.4 under expectation, and sdev
was about 77% of expected.

so i think we saw the noise reduction we'd hope for from inherently
lower-noise resistors. since we only need one per channel, that's about
an additional $5.40 in BOM cost to use them. the tested parts were also
0.5% tolerance, whereas the 1800s in the previous test were 1%. that
might contribute to some of the variation in expected gain change.
