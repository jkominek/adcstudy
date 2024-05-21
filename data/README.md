As of this file, all of this are recordings from a single sensor, located
on A#0. The "interference" files are produced by leaving A#0 alone, and
tapping the keys A0 and B0. The non-intereference files are of course,
from striking A#0.

The filenames go something like:

* timestamp
* ADC
* VDD
* VAA
* approx sample rate
* current to voltage conversion device
* gain-setting resistor value
* Vref source and voltage

TIAs flip the signal around, so that 1023-x (where x is any given data point)
produces the expected signal.

Each file has all 8 channels from the ADC in it, but the data only shows
up on a pair of them. Column 1 of the file is a timestamp, column 2 is
a hammer sensor, column 3 is a key stick sensor, etc etc. When a TIA is
in use, the 'empty' channels will all read 1023; the resistor board
produces 0s for the empty channels.

