
2026-04-08 00:51

Tags: [[Project primus-risc-v]]

# UART
This is only for bootloading so we do not have to make a new bitstream each time we want a new program.

## My Understanding
The UART protocol starts with a start bit which is uart_rx = 0 and then sends the data and stops which is a 1. The data on the uart buffer is sampled in the middle of a sending window which depends on the baud rate. Counting the number of falling edge. 

The data accumulated in the buffers are only valid when the uart_rx/tx_valid is high.


### UART Protocol & 32-bit Transmission
Core Principle

UART is inherently a byte-serial protocol. It physically transmits one bit at a time, framed into 8-bit characters. At the hardware level, there is no concept of a multi-byte transfer.
Transmission Lifecycle (Per Byte)

For every byte transmitted:

    Poll: CPU polls the STATUS register until tx_ready == 1.

    Write: CPU writes 1 byte to the UART_TX register.

    Shift: UART module shifts out: Start Bit → 8 Data Bits → Stop Bit.

        Timing: 10 bits total at 115200 baud ≈ 87 µs per byte.

    Ready: Only then is tx_ready high again.

Implementation: Sending a 32-bit Word

To send a 32-bit word in a bootloader, you must perform four separate writes. This example uses Little-Endian byte order.
1. The Word-to-Byte Logic
Code snippet

send word in t0, byte by byte (little-endian)

```
call tx_byte          # send t0[7:0]
srli t0, t0, 8

call tx_byte          # send t0[15:8]
srli t0, t0, 8

call tx_byte          # send t0[23:16]
srli t0, t0, 8

call tx_byte          # send t0[31:24]
```

2. The tx_byte Subroutine

This routine polls the status bit before writing the data to the transmission register.
Code snippet
```
tx_byte:
  li   t1, 0x2008     # STATUS address

wait:
  lw   t2, 0(t1)      # Load status
  andi t2, t2, 0x1    # Test tx_ready bit
  beq  t2, x0, wait   # If 0, keep polling

  sw   a0, -8(t1)     # Write to UART_TX (0x2000)
  ret
```
Hardware Context: FIFOs

    [!INFO] Hardware Evolution
    Real-world UARTs like the 16550 (a standard in PCs since the 1980s) utilize a small FIFO (typically 16 bytes) to buffer outgoing data. This prevents the CPU from having to poll as tightly.

    However, even with a FIFO, the underlying physical layer still transmits one bit at a time. A "no-FIFO" implementation is perfectly acceptable for bootloaders where code simplicity is prioritized over raw throughput.

## Implementation
![[Pasted image 20260408010857.png]]

# References
