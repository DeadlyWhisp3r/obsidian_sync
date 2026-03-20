
2026-02-21 12:01

Tags: [[Computer architecture]] 

# Endianess
Endianess describes how data is stored within words or double words (32 and 64bit). There are two different endianess, big and little endian

| Endian        | Byte 3 | Byte 2 | Byte 1 | Byte 0 |
| ------------- | ------ | ------ | ------ | ------ |
| Little Endian | 0xc0   | 0x08   | 0x04   | 0x00   |
| Big Endian    | 0x00   | 0x04   | 0x08   | 0xc0   |

### Big endian
The computer stores the byte data in the big end of the word so the data located at address 0x0000 is stored in the highest byte of the word.


### Little endian
The opposite, the data is stored in the little end of the word. Data located at address 0x0000 is placed in the lowest byte of the word.



# References
