
2026-02-18 23:56

Status:

Tags: [[RISC-V]] 

# Instruction Fetch
The Instruction Fetch stage fetches the instruction and increments the Program Counter.

### Implementation
The memory has to be implemented as a BRAM to store the instructions. How do we assure that it is implemented as BRAM and not registers?

Also when defining the logic of the memory it is declared as 
````SystemVerilog
logic [31:0] inst_mem [0:1023]
`````
Since the first address of the memory is stored at the top [1024] also works and does the same but it is more safe to be explicit.

The memory now hold 1024 words of size 32 but the address is byte addressable so for the address the lower two bits are used to access the byte within a word.

````SystemVerilog
// Logic slices used (inefficient)
assign inst = mem[addr[11:2]];

//Using BRAM instead
module instruction_memory (
    input  logic        clk,     // Added clock
    input  logic [31:0] addr,
    output logic [31:0] inst
);
    logic [31:0] mem [0:1023];

    initial $readmemh("program.hex", mem);

    always_ff @(posedge clk) begin
        // The output is now registered
        inst <= mem[addr[11:2]]; 
    end
endmodule
`````
$readmemh is crucial since the BRAM needs to be loaded with the program and this takes care of that, loading the program.hex file.
### What makes it implement the BRAM?
It is crucial that the reset is not included in the always_ff block since the BRAM can not reset all memory locations at once, therefore it would have to implement something else. It obviously needs to be clocked as well and can not be asynchronous. 

However using the BRAM adds a 1 CC delay (latency to the pipeline)


# References
