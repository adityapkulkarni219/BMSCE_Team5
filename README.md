![](../../workflows/gds/badge.svg) ![](../../workflows/docs/badge.svg) ![](../../workflows/test/badge.svg) ![](../../workflows/fpga/badge.svg)

# Tiny Tapeout 4-Bit Shift Register Verilog Project

A 4-bit Shift Register was designed and implemented as part of the Tiny Tapeout project using Verilog HDL. The design supports serial data input and synchronous clock-driven shifting, enabling storage and transfer of 4-bit data sequences. It was synthesized and verified through simulation to ensure correct functionality, including reset operation and proper shifting behavior.

## Block Diagram
<img width="1536" height="1024" alt="Block diagram" src="https://github.com/user-attachments/assets/e8a98752-10a3-415d-bce5-242682052ae5" />

## Input's and Output's
The shift register has:
•	Inputs:
  o	clk → Clock signal
  o	reset → Clears the register to 0
  o	load → If 1, loads data directly from parallel_load
  o	direction → Shift direction (0 = right, 1 = left)
  o	serial_input → Bit shifted in during shift operations
  o	parallel_load[3:0] → 4-bit data to load in parallel
•	Output:
  o	parallel_out[3:0] → Current value of the shift register

## Working
The steps of working are as follows:
1. Reset
   When reset=1, no matter what else is happening, the register is cleared to 0000.
2. Parallel Load
   When load=1, the register ignores shifting and directly loads the 4-bit input parallel_load.
   Example: if parallel_load = 1011, then parallel_out = 1011 on next clock.
3. Shift Operations
   1. Shift Right (direction = 0)
      •	Shifts everything to the right.
      •	parallel_out[3] gets the new serial_input.
      •	Bits [3:1] shift into [2:0].
      •	The old parallel_out[0] is dropped.
      Example:
        -> parallel_out = 1011, serial_input=1
        -> After clock → parallel_out = 1101.
   2.Shift Left (direction = 1)
      •	Shifts everything to the left.
      •	parallel_out[0] gets the new serial_input.
      •	Bits [2:0] shift into [3:1].
      •	The old parallel_out[3] is dropped.
      Example:
        -> parallel_out = 1011, serial_input=0
        -> After clock → parallel_out = 0110  
4. Default
   If somehow direction is invalid (shouldn’t happen since it’s 1 bit), output clears to 0000.
## Waveforms
<img width="1919" height="344" alt="Waveform" src="https://github.com/user-attachments/assets/68eb8180-6bab-4bac-bd78-df2dbf10a6c1" />

## Enable GitHub actions to build the results page

- [Enabling GitHub Pages](https://tinytapeout.com/faq/#my-github-action-is-failing-on-the-pages-part)

## Resources

- [FAQ](https://tinytapeout.com/faq/)
- [Digital design lessons](https://tinytapeout.com/digital_design/)
- [Learn how semiconductors work](https://tinytapeout.com/siliwiz/)
- [Join the community](https://tinytapeout.com/discord)
- [Build your design locally](https://www.tinytapeout.com/guides/local-hardening/)

## What next?

- [Submit your design to the next shuttle](https://app.tinytapeout.com/).
- Edit [this README](README.md) and explain your design, how it works, and how to test it.
- Share your project on your social network of choice:
  - LinkedIn [#tinytapeout](https://www.linkedin.com/search/results/content/?keywords=%23tinytapeout) [@TinyTapeout](https://www.linkedin.com/company/100708654/)
  - Mastodon [#tinytapeout](https://chaos.social/tags/tinytapeout) [@matthewvenn](https://chaos.social/@matthewvenn)
  - X (formerly Twitter) [#tinytapeout](https://twitter.com/hashtag/tinytapeout) [@tinytapeout](https://twitter.com/tinytapeout)
