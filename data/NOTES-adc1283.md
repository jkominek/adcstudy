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
  * hammer peak 2280
  * hammer background
    * mean 32.73 sdev 2.43
  * keystick background
    * mean 455.41 sdev 2.68

hammer background mean is twice what we'd expected from the mcp3008,
but sdev is slightly better than we'd expect. keystick background
doesn't show nearly the degradation.


adc1283_3V3_22300Hz_mcp6l04_2870tf,10nF_tps7171@1.9V
  * hammer peak 2305
  * hammer background
    * mean 52.28 sdev 2.00
  * keystick background
    * mean 448.20 sdev 2.23

mean and sdev are both worse than we saw on the mcp3008.
keystick background is only a little bit worse.


adc1283_3V3_22300Hz_tsv994_2870tf,2.2nF_tps7171@1.9V
  * hammer peak 2305
  * hammer background
    * mean 50.42 sdev 1.43
  * keystick background
    * mean 447.14 sdev 1.78

hammer background is worse than we'd expected from the readings off
the MCP3008 in the same configuration. hammer sdev is slightly better,
keystick sdev slightly worse. huh. background can be improved with
biasing.

we do have a blip around ~70k, which i'm assuming is another transmission
error. (original attempt to collect this turned up a different one which
was more important to fix, and has been.)


adc1283_3V3_22300Hz_tsv994_2870tf,10nF_tps7171@1.9V
  * hammer peak 2295
  * hammer background
    * mean 59.86 sdev 0.82
  * keystick background
    * mean 451.98 sdev 1.31

further background increase, though the sdev went down. hmm. would
definitely like to see this with C0G 10nFs, and the bias resistor.