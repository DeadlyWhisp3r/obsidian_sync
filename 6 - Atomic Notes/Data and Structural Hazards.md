
2026-03-12 00:41

Tags: [[RISC-V]]

# Data and Structural Hazards
When first running my complete top level test on the risc-v proccessor I ran into data and structural hazards while executing my Fibbonacci program. 

### Data Hazards
I have data hazards since the result from some operations are immediatly being used in the following instruction. Because I do not have forwarding this data has not yet reached the write back stage and been sent back to the register file so when it is being fetched it is using the old value. 

This can be solved by using forwarding where the result is being sent back to the stages quicker (Both the Memory stage and the Instruction decode stage). This makes the data available. You can also solve this problem by inserting the NOP instruction and stalling the pipeline if you see that the operand is being used in both the ex_stage and the id_stage.

### Structural Hazards
We also see structural hazards which are when branches are being evaluated we do not know if we should take branch or not. This needs some kind of branch prediction otherwise we have to flush out and waste a lot of our performance. It is better if we can predict well if the branch will be taken.

I will implement a recently taken state machine that remembers the last two branches. This scheme is good because in code we have a lot of if loops so assuming we get stuck in long loops this scheme will mostly work out.



# References
