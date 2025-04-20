* an AFE board that's just a resistor ladder, so all the channels get some
  input, and you've got a vague idea what it is.
* more ADC boards
* interested in doing voltage amplification of the phototransistor/resistor
  output, rather than TIA. i don't think that will be better, but i'm
  curious.
* TSV994A <- lower input voltage offset than the TSV994. same price or
  cheaper, depending on site?
* BD7284YFV-CE2 looks very promising; superior to TSV994 in every way except
  GBW, which is still sufficient. halves the input bias current and noise of
  both the MCP6L04 and TSV994, while reducing offset voltage by 10-100x.
* TI OPA4314 might also be worth a shot; offset voltage is worse, but input
  bias is better. noise figure is comparable. slew and bandwidth are lower,
  so it might not amplify high frequency noise as bad?

* i've got a tia rev2 board with unlabelled stuff on it that i need to
  remember why i made, and then take measurements from it. maybe even
  finish it? doesn't look like i put on passives.
* i think i've also made some other board i need to measure? need to
  sort through the loose PCBs
