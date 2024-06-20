# LCD_FPGA
### It's a GitHub for LCD on FPGA (DE2115), the code clearly separates the combinational logic and sequential logic. Easy to understand.
You don't need to process logic in the sequential logic that takes a longer time to synthesize, just modify the logic in the combinational logic.

### There are two ways to handle the busy flag
- Receive the LCDdata[7], if it is 0, it means you can move on.
- Ignore the Busy flag, but make sure you have waited enough time to move on. It takes longer to handle than the first way.
The code take both of these ways to show how to handle LCD busy flag, hope it can help you handle the trouble.

Every time we need to refresh these commands, so you can see it in the every begin of the loop.

localparam [69:0] initialize = {
    // wait 15 ms
- 10'b0000110000, // Function set
    // wait 4.1 ms
- 10'b0000110000, // Function set
    // wait 100 us
- 10'b0000110000, // Function set
    // wait busy flag
- 10'b0000111000,  // Function set
    // wait busy flag
- 10'b0000001100,// Display on 
    // wait busy flag
- 10'b0000000001, // Clear display
    // wait busy flag
- 10'b0000000110 // Entry mode set
    // initial done
};



If you want to know the details of LCD protocol, please see the ref: http://media.ee.ntu.edu.tw/personal/pcwu/dclab/dclab_08.pdf 
