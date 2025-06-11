# Binary GCD Module Verilog

This hardware module implements the binary Euclidean algorithm, also known as Stein's algorithm, to determine the greatest common divisor (GCD) of two integers.
The width of the operands can be set as a parameter (WIDTH), with a default value of 32 bits.
The functionality of the module has been formally verified for an 8-bit width.

## Interface

The module implements a basic handshaking interface.
A new operation is triggered by raising the *start_i* signal while the *ready_o* signal is high.
After the computation finishes, the *done_o* signal is asserted for one clock cycle.

| **Port** | **Type** | **Width** | **Desciption**                         |
|----------|----------|-----------|----------------------------------------|
| clk_i    | input    | 1         | Clock signal                           |
| rst_i    | input    | 1         | Reset signal (active high)             |
| start_i  | input    | 1         | Trigger new computation                |
| a_i      | input    | WIDTH     | Operand                                |
| b_i      | input    | WIDTH     | Operand                                |
| res_o    | output   | WIDTH     | Computed GCD                           |
| ready_o  | output   | 1         | Module is ready for the next operation |
| done_o   | output   | 1         | Result (res_o) is valid                |

## Performance

The module's latency depends on the operand values and ranges from a minimum **2** clock cycles (when one operand is zero) to a maximum of **2+2*WIDTH** clock cycles.

## Verification

Formal verification has been used to confirm that the functionality is correct for an 8-bit operand width.
The properties can be found in the *sva* subfolder.
