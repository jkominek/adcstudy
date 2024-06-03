# what is this?

A set of kicad 8 boards for investigating various combinations of ADC
and analog frontend for my [piano
conversion](https://github.com/jkominek/piano-conversion) project.

There might be some errors and problems with them, but I'm not currently
aware of any issues.

# please describe the boards

The ADC boards are designed to plug into a [Glasgow Interface
Explorer](https://glasgow-embedded.org/latest/intro.html), but that's
done via 2.54mm pin headers, so you can hook them up to anything with
some jumper wires. The Glasgow header has the various digital signals
necessary for the board, and provides VDD. (Which the Glasgow can adjust.)
Whichever of my applets are complete-enough are available in
[my fork of the Glasgow repo](https://github.com/jkominek/glasgow).

The other side of the ADC board is designed to plug into an analog
frontend board. It should provide VAA to the AFE board, and receives
back Vref, and AINx+ and AINx-. + and/or - might be Vref, or ground,
or whatever. The ADC board might also ignore one or of the two and
reference the other to... whatever it wants. The MCP3008 board for
instance uses AINx- only, and references GND and Vref.

The AFE boards take in VAA, and produce Vref, along with the Ax+ and Ax-
signals. One of them will probably be fixed. In the middle it can do
whatever it wants, and then the other end should be a 2x8 connector
which (in my application) is used for 8 phototransistors. The positive
pin of each pair is intended for the collector, and the negative pin
for the emitter.

You can of course plug whatever you want into those pins.

# what's wrong with them

Haven't tested the ADS131M08, ADC1283 or resistor ladder boards yet,
though I did correct the systemic issues of which I was aware.

# what choices do the boards give me

You can put the headers on in whichever orientation you want, though if
you're hooking it up to a Glasgow like I am, there are only a couple
options that make sense.

The opamp footprint is the most common four amp footprint, so you can
stick any of a bunch of opamps in there.

There are a number of voltage reference ICs that'll work in the provided
footprint. I've been putting on MIC5366-2.0 because I have a bunch of
them.

The MCP3008 board lets you feed VDD through to VAA with just some passive
filtering, or you can put in a linear regulator.

Obviously you can swap the gain setting resistors.

# quick what's best

For these sorts of signals, the MCP6L04 seems good enough, with the TSV994
probably a runner up because it is more expensive. A thin film gain resistor
and a capacitor in parallel with that resistor which is in the ballpark
of 10nF.

I've got some more ideas for tweaking the TIA configuration with just
passives.
