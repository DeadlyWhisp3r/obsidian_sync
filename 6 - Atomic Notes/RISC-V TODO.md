
2026-03-18 21:44

Tags: [[RISC-V]]

# RISC-V TODO
Todo list for my project

#### Branch prediction state machine
Implement the branch predictioni state machine using two bits.

#### Load a proper program
Load a proper program and see in simulation and then proceed to try the same program on the actual fpga. Maybe connect the 7 segment display and wire them to some registers.



There is a latency on the subtraction of the looping condition register. 3 times it gets called before actually starting to decrement.

it seems to be because of the pipeline flushing...


UART had problems with the stalling, it did not take into account when forwarding that if you had the x0 register it might give an actual value instead of the hardcoded 0es.

![[Pasted image 20260410032530.png]]
Im not 100% conviced yet

Byt addressable LB, SB, instruction. Need to implement a byte strobe so i do not overwrite any data when performing such instructions. 
addr[1:0] in the mem stage will tell you which byte you want within the word

added weird opeators such as | imem_we_b which means that is turns the 4 bit value in to a one if any of the bits is one and the it checks if it is going to come to the imem. Compare that to dmem_we & {4{!addr_is_uart && !addr_is_mem}} which keeps the byte enabled signals.

Bug in the rtl where the forwarding used rs1/2_addr_q2 for the write back stage which did not work for bubbles which made the instruction go to wb stage and then it was needed. The forwarding should actually happen with the address that is in the wb stage which is the address from the mem_stage.

Another bug was that the rs1/2_o used the stale value if forwarding was needed from the wb_stage.  so therefore we use the actual w_data_i if the we_i signal is high.

it also had a bug where the bram port b wasw unconnected and then that data was delayed by 1 CC so it had to use the forwrding alu result.

With the extended memory the uart map was inflicting upon the stack making the program hang

33 CCs divider because of fpga limitations

The uart main.c program was printing weird characters and also later printing wrong register names. The root cause turned out to be a single line in ex_stage.sv: when a non-writing instruction (branch, store, NOP) passes through EX, rd_addr_q2 was holding the previous reg-writer's address instead of clearing to zero. This let it falsely match registers read by later            
  instructions, forwarding whatever happened to be in MEM at the time — which was always the wrong value.

#### Ddr2
https://github.com/ChrisPVille/mig_example/blob/master/Nexys%204%20Onboard%20DDR2%20MIG%20Configuration.pdf

MMCM issue with too many instanciated, had to remove the clk_wiz that made the 50 mhz signal and instead make a 200 which fed into the mig and then the mig converted it to 50 mhz with the built in MMCM.

Just checking now if old code and bootloader works. Restore back to the new one using ddr2 and such later.
# References
