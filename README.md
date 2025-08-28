
---

# FPGA-Based Door Lock System Using Sequence Detector

## 📌 Project Overview

This project implements a **sequence detector** on an FPGA to simulate a digital door lock system. Inputs are given through DIP switches, and a push button (**P45**) triggers verification. A **seven-segment display** serves two functions:

* **Normal Mode**: Shows the decimal value of the binary input sequence entered through DIP switches.
* **Verification Mode (after pressing P45)**:

  * **O → Door Open** (correct sequence entered)
  * **C → Door Closed** (incorrect sequence entered)

---

## 🛠️ Hardware Requirements

* FPGA Development Board (e.g., Xilinx/Altera/Intel)
* On-board DIP switches
* Push button (P45 or equivalent)
* Seven-segment display

---

## 💻 Software/Tools

* Verilog / VHDL (HDL implementation)
* Xilinx ISE 

---

## ⚙️ Working Principle

1. User enters a binary sequence via DIP switches.
2. The seven-segment display shows the **decimal equivalent** of that binary input.
3. When the **P45 button** is pressed, the FPGA compares the input with the predefined valid sequence.
4. The display then changes to:

   * **O** → Open (if sequence matches)
   * **C** → Closed (if sequence does not match)

---

## 🧩 Verilog Snippet (Seven-Segment Display)

```verilog
module sevenseg_display(input [3:0] bin_in, input match, input check_btn, 
                        output reg [6:0] seg);
    // Common cathode 7-seg mapping: {a,b,c,d,e,f,g}
    always @(*) begin
        if (check_btn) begin
            if (match) 
                seg = 7'b0000001; // "O" (all except middle segment)
            else 
                seg = 7'b1000110; // "C"
        end else begin
            case(bin_in) // Show decimal digits
                4'b0000: seg = 7'b0000001; // 0
                4'b0001: seg = 7'b1001111; // 1
                4'b0010: seg = 7'b0010010; // 2
                4'b0011: seg = 7'b0000110; // 3
                4'b0100: seg = 7'b1001100; // 4
                4'b0101: seg = 7'b0100100; // 5
                4'b0110: seg = 7'b0100000; // 6
                4'b0111: seg = 7'b0001111; // 7
                4'b1000: seg = 7'b0000000; // 8
                4'b1001: seg = 7'b0000100; // 9
                default: seg = 7'b1111111; // Blank
            endcase
        end
    end
endmodule
```

---

## 📊 Applications

* Digital door lock systems
* Access control mechanisms
* Security authentication modules

---

## 🚀 Future Scope

* Replace DIP switches with keypad input
* Add LCD/LED matrix display
* Store multiple access codes
* IoT-based remote door access

---
