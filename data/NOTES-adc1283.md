  * and we begin a new file for the ADC1283 test data
  * not bothering with keystick peaks anymore.
  * sample rate is approximate, i might measure it and update this with
    the actual value. i was targetting something between 20k and 25k, since
    25k is the max according to the data sheet.
  * note these files only specify 3V3 once, because they just have a
    VDD and VAA (supplied by the voltage reference), not VDD, VAA and Vref,
    as the MCP3008 had.
    * it would've been possible to configure the setup to test the MCP3008
      with VDD=5V and VAA=3V3 which is why both numbers are recorded. but
      since i wouldn't want to actually use the part in 5V VDD, i didn't
      bother.

adc1283_3V3_22300Hz_mcp6l04_2870tf,2.2nF_tps717@1.9V_bias470k
  * hammer peak 2281
  * hammer background
    * mean 18.60 sdev 3.05
  * keystick background
    * mean 445.55 sdev 3.30

okay like the corresponding record from the MCP3008 file, the bias
resistor is only on the hammer channel, not the keystick. that said.
looks solid. there's a weird blip and a discontinuity, i expect that's
a result of my glasgow applet doing the data capture, i had similar
things happen during development and didn't quite sort it all
out. doesn't reflect on what the part is actually doing, just my
ability to transfer it out.

background means and sdevs went up by a bit more than 4x, which is
disappointing, but not the end of the world. our peak-to-noise ratio
is in the ballpark of the mcp3008's, and i think remains sufficient.

quickly plotting the same thing quantized to 10 bits, overtop of this,
shows that the extra resolution doesn't magically capture blatantly
interesting features of the data that were missing. this part is about
reducing the cost, and increasing the possible sample rate.

adc1283_3V3_22300Hz_mcp6l04_2870tf,10nF_tps7171@1.9V
  * hammer peak 2302
  * hammer background
    * mean 38.68 sdev 2.46
  * keystick background
    * mean 443.38 sdev 2.78

keystick background stayed the same, so the hammer background going up
is just because this channel doesn't have the bias resistor to bring
the background down. that resistor is doing some good work. but we didn't
get much reduction in sdev. do we need more capacitance? will it help?
should i try and check this at a similar sample rate to the MCP3008?
maybe the cap just isn't able to keep up with the charge demands of the
higher sample rate?
