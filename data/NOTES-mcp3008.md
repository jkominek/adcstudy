note, the keystick peak is rather arbitrary, as it depends on how hard
i press the key down, and for some reason i was trying to measure the
'average' location by eye rather than the actual peak-peaks, or even the
highest peak. i should probably throw out all the keystick peak lines
and stop collecting them, at this point. sigh.


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



2024-06-01T15:48:33.751857_mcp3008_3V3_3V3_12750Hz_mcp6l04_1800,44pF_mic5366@2V
2024-06-01T15:48:41.738471_mcp3008_3V3_3V3_12750Hz_mcp6l04_1800,44pF_mic5366@2V_interference
  * hammer peak 404
  * hammer background
    * mean 5.48 sdev 1.36
  * keystick peak 530ish
  * keystick background
    * mean 73.47 sdev 1.41
== SCALED TO ACTUAL 2V
==  * hammer peak 342.5
==  * hammer background
==    * mean 4.78 sdev 1.17
==  * keystick peak 462ish
==  * keystick background
==    * mean 64.09 sdev 1.23


the keystick channel shows massive spikes on both the main data file,
as well as the interference file. something weird is going on.
looks like there was also some data loss in around time stamp 8250 in the
main file. not a big issue. higher peak heights than the data collected
without the capacitor. would've expected dampening, so that's odd.
elevated background and noise.

mcp3008_3V3_3V3_12750Hz_mcp6l04_1800,100pF_mic5366@2V
  * hammer peak 403
  * hammer background
    * mean 5.68 sdev 1.25
  * keystick peak 535ish
  * keystick background
    * mean 73.87 sdev 1.30
== SCALED TO ACTUAL 2V
==  * hammer peak 351.6
==  * hammer background
==    * mean 4.96 sdev 1.09
==  * keystick peak 466ish
==  * keystick background
==    * mean 64.43 sdev 1.13

none of the weird spikes here. i think something is wrong with channel #1
on this TIA board. worth investigating electrically, but not interesting
for the overall data collection, i don't think.

peaks and background levels are effectively identical to the 44pF board.
sdevs are very slightly lower. that's nice.

so what do we predict for the next set of channels, that use the 2870
thin film resistors, with these same capacitors? probably even higher
background levels, along with even lower sdev. peaks of 642.5 and
853ish?

mcp3008_3V3_3V3_12750Hz_mcp6l04_2870tf,44pF_mic5366@2V
  * hammer peak 644
  * hammer background
    * mean 12.29 sdev 1.94
  * keystick peak 820-850
  * keystick background
    * mean 119.46 sdev 2.44
== SCALED TO ACTUAL 2V
==  * hammer peak 562
==  * hammer background
==    * mean 10.72 sdev 1.69
==  * keystick peak 715-741
==  * keystick background
==    * mean 104.23 sdev 2.13

ok compared to the 1800 + capacitor tests, we got exactly what we expected.
values were scaled up by 1.595x, except the standard deviations which were
reduced, but only a bit this time.

i should note all of these capacitors are X7R, i should've used NP0 here,
since these are in the signal path.

we'll expect to see these same values again for the 100pF test, except
with slightly lower sdevs

mcp3008_3V3_3V3_12750Hz_mcp6l04_2870tf,100pF_mic5366@2V
  * hammer peak 640
  * hammer background
    * mean 12.07 sdev 1.55
  * keystick peak 865
  * keystick background
    * mean 122.5 sdev 3.17
== SCALED TO ACTUAL 2V
==  * hammer peak 558
==  * hammer background
==    * mean 10.53 sdev 1.35
==  * keystick peak 754
==  * keystick background
==    * mean 105.95 sdev 2.76

peaks were consistent (keystick is much more dependent on how i press the
key). i'd say the background was effectively equal to the 44pF configuration.

thinking these values were kind of weird, i went back and measured Vref.
despite it being a 2V MIC5366, it is actually outputing 1.745V. so all
the values are 14.61% higher than they ought to be.


mcp3008_3V3_3V3_12750Hz_mcp6l04_2870tf_mic5366@2V
  * hammer peak 553
  * hammer background
    * mean 9.04 sdev 1.51
  * keystick peak 735ish
  * keystick background
    * mean 101.26 sdev 1.49

no capacitor at all looks like a slight improvement over the 44 and 100pF
caps. odd that this has has worse hammer background than our original
measurement, though. it's the same configuration as that first test but
with a better gain resistor. though at a higher gain. noise goes up faster?
in that case we'd be better off with a low resistor for the TIA and then
a purely voltage amplification stage. which isn't what any of the advice
suggests.

(just to sanity check things i turned out the lights and covered up
the sensors a bit, and only got a 0.25% reduction in background. no
effect on sdev. no particular reason to believe that was real.)

i should recapture the original mcp6l04 w/1800 gain signal and see if it
holds up. maybe there's just a lot of variability? maybe that was just a
really good 6L04?

mcp3008_3V3_3V3_12750Hz_mcp6l04_2870tf,1pF_mic5366@2V
  * hammer peak 552
  * hammer background
    * mean 8.72 sdev 1.54
  * keystick peak 730s
  * keystick background
    * mean 102.26 sdev 1.62

basically the same as not having 1pF. which is to be expected, 1pF is
probably less than the stray capacitance on the board.

mcp3008_3V3_3V3_12750Hz_tlv9064_2870tf_mic5366@2V
  * hammer peak 553.5
  * hammer background
    * mean 11.48 sdev 4.29
  * keystick peak 740ish
  * keystick background
    * mean 107.00 sdev 3.22

first test with the TLV9064. background is definitely higher, and we've got
quite a bit more noise. it's very visible on the plots. i'm assuming
the much higher GBW is amplifying some stuff that's otherwise being filtered
out? we only build this with 0pF and 1pF, would it be worth trying with
100pF? best input bias and 2nd best offset voltage in the cheap class
doesn't seem to have helped it any. if the gain theory is right we should
see the TLV4314 do better than the TLV9054.

mcp3008_3V3_3V3_12750Hz_tlv9064_2870tf,1pF_mic5366@2V.csv
  * hammer peak 553
  * hammer background
    * mean 10.75 sdev 3.61
  * keystick peak 690s
  * keystick background
    * mean 107.39 sdev 3.13

basically the same, with maybe some of the noise filtered. still really
bad. sigh.

mcp3008_3V3_3V3_12750Hz_tsv994_2870tf_mic5366@2V
  * hammer peak 550
  * hammer background
    * mean 2.04 sdev 5.44
  * keystick peak 740s
  * keystick background
    * mean 104.63 sdev 4.60

lowest hammer background yet, but there's a lot of very spiky noise on it.
it'd be great if the capacitor on the feedback cleaned that up.

mcp3008_3V3_3V3_12750Hz_tsv994_2870tf,47pF,NP0_mic5366@2V
  * hammer peak 549
  * hammer background
    * mean 10.29 sdev 1.77
  * keystick peak 735ish
  * keystick background
    * mean 107.20 sdev 2.08

well. that's weird. the capacitor brought the sdev down quite a bit, but
the background mean went up more than i'd expect. i find it hard to believe
that the amp-to-amp variation of Voffset is so high. signal is plenty
clean, though. looks like we had some data loss around sample 8000.

mcp3008_3V3_3V3_12750Hz_tlv4314_2870tf_mic5366@2V
  * hammer peak 550
  * hammer background
    * mean 9.34 sdev 2.63
  * keystick peak 700s? lot of variation this time
  * keystick background
    * mean 106.82 sdev 2.60

looks cleanish, but sdev isn't as good as others. mean is a smidge lower.
curious to see what the cap does.

mcp3008_3V3_3V3_12750Hz_tlv4314_2870tf,47pF,NP0_mic5366@2V
  * hammer peak 550
  * hammer background
    * mean 11.89 sdev 2.10
  * keystick peak 730s
  * keystick background
    * mean 105.54 sdev 2.03

worse hammer background, but the sdev is lowered slightly. seems to
be consistent with putting a capacitor on things? leakage?


mcp3008_3V3_3V3_12750Hz_resistor_2870tf,1pF_mic5366@2V
  * hammer peak 543
  * hammer background
    * mean 10.34 sdev 1.45
  * keystick peak 730s
  * keystick background
    * mean 105.25 sdev 1.36

basically just worse than not having the resistor there.

mcp3008_3V3_3V3_12750Hz_resistor_2870tf,47pF,NP0_mic5366@2V
  * hammer peak 542
  * hammer background
    * mean 9.94 sdev 1.23
  * keystick peak 720s
  * keystick background
    * mean 105.09 sdev 1.14

that's an across the board improvement from 1pF, and close to being
in the ballpark of having no capacitor there. backgrounds are a smidge
lower, but the noise is a smidge higher.

mcp3008_3V3_3V3_12750Hz_resistor_2870tf,100pF_mic5366@2V
  * hammer peak 542
  * hammer background
    * mean 9.77 sdev 1.02
  * keystick peak 700s
  * keystick background
    * mean 103.87 sdev 1.02

alright, that's actually better than the original no-capacitor version.
what about more capacitance?

mcp3008_3V3_3V3_12750Hz_resistor_1800,tps717@1.9V
  * hammer peak 359
  * hammer background
    * mean 7.73 sdev 0.94
  * keystick peak 480s
  * keystick background
    * mean 69.88 sdev 0.87

backgrounds are slightly higher than when we used the 1800 with a MIC5366,
but the noise is lower. generally pretty nice looking signal.

mcp3008_3V3_3V3_12750Hz_resistor_2870tf_tps717@1.9V
  * hammer peak 571
  * hammer background
    * mean 13.15 sdev 1.27
  * keystick peak 755ish
  * keystick background
    * mean 111.32 sdev 2.02

bunch of unpleasant noisy spikes on the keystick channel. weird.
peaks are where we'd expect them based on the previous channel, and the
change in gain. background increase is worse than expected. keystick
sdev isn't too surprising considering the strange spikes. they're not
nearly as bad in the background region that i sampled, either.

mcp3008_3V3_3V3_12750Hz_resistor_2870tf,100pF_tps717@1.9V
  * hammer peak 571
  * hammer background
    * mean 12.64 sdev 0.96
  * keystick peak 
  * keystick background
    * mean 110.21 sdev 1.10

having trouble with the keystick signal, it dropped out some here, but
we continued to see the strange noise in the interference file for the
keystick. i wonder if i've got some wiring issue with it. mostly interested
in the hammer signal, so i'm just going to keep going.

100pF of capacitance seems to have reduced background and brought the
noise down quite a bit. peak shape on the hammer strikes remains distinct,
so i'm not worried about filtering at 100pF. let's see how 1nF does.

mcp3008_3V3_3V3_12750Hz_resistor_2870tf,1nF_tps717@1.9V
  * hammer peak 569
  * hammer background
    * mean 12.55 sdev 0.57
  * keystick peak
  * keystick background
    * mean 110.18 sdev 0.50

easily the cleanest signal yet. peaks still seem distinct but look
kind of "idealized". i wouldn't be surprised if at 10nF they begin to
lose their shape.

so, ok, 1nF of filtering is reasonable for this signal. if we could
get a peak to background ratio of 569:7 or so (81:1) with this kind
of sdev, i think i'd be satisfied.

that hammer background of 12.55 is (12.55/1023)*1.9V = 23.3mV
with a gain of 2870, that represents (23.3mV)/2870 = 8.118 microamp
leaking through the phototransistor. our best ever (mcp6l04 w/1800 gain)
corresponded to 4.34 microamp through the phototransistor.

based on figure 9 of the CNY70 datasheet, we'd be seeing 4-8 microamp
of current if Vce were 5V, and the reflective card was ~7.5 to 10mm
away. we're at a lower Vce (1.3V to 3.3V, depending), and our target
for the hammer at least is quite a bit further away.

the fig9 collector current seems to be asymptotically approaching 4uA,
suggesting that that might be the intrinsic dark current of the device,
at 5V Vce. certainly that's the absolute best we've ever seen, so it
doesn't seem out of the question.

so can we drain 4uA off of the signal, to balance that out? looks pretty
easy with the TIA's, we put a high value (500k?) resistor between the
signal and ground, and that should trickle 4uA out, which will force
the amp to adjust. they've certainly got the head room for it.

but then we've got to duplicate that noise filtering effect with one
of the opamps. ideally a cheap one.

mcp3008_3V3_3V3_12750Hz_mcp6l04_2870tf,2.2nF_tps717@1.9V
  * hammer peak 577
  * hammer background
    * mean 9.93 sdev 0.51
  * keystick peak 760s
  * keystick background
    * mean 110.69 sdev 0.59

great noise reduction, hammer background is average-ish, at least.
peak shape still looks good. hard to imagine 10pF will meaningfully
reduce the sdev further, but i'll be curious to see what it does.

mcp3008_3V3_3V3_12750Hz_mcp6l04_2870tf,10nF_tps717@1.9V
  * hammer peak 574
  * hammer background
    * mean 8.04 sdev 0.36
  * keystick peak
  * keystick background
    * mean 109.04 sdev 0.41

well, okay, that reduced the sdev further. seems to have reduced
background as well? this really seems about as good as i think i
could hope for. that hammer background of 8.04 corresponds to a
current of 5.2uA through the phototransistor.

mcp3008_3V3_3V3_12750Hz_tsv994_2870tf,2.2nF_tps717@1.9V
  * hammer peak 575
  * hammer background
    * mean 10.80 sdev 0.41
  * keystick peak
  * keystick background
    * mean 111.13 sdev 0.40

signal is clean enough, but background levels are slightly
higher. 6L04 really seems to be a champ for that. will we see
the background levels drop slightly with the 10nF cap?

mcp3008_3V3_3V3_12750Hz_tsv994_2870tf,10nF_tps717@1.9V
  * hammer peak 573
  * hammer background
    * mean 10.01 sdev 0.09
  * keystick peak
  * keystick background
    * mean 111.04 sdev 0.19

yow, that's a huge improvement in noise. basically the same
background as the 2.2nF.