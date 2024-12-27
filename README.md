# 16-bit-koggestone-adder
Kogge-Stone adder is renowned for its speed and efficiency, it also faces several significant  challenges, particularly in terms of hardware implementation and power consumption.


Verilog code

module ksa16(A, B, Cin, S, Cout);

 input [15:0] A, B; input Cin;

 output [15:0] S;

 output Cout;

 wire [15:0] P, G;

 wire [14:0] C;

 assign P[0] = A[0] ^ B[0];

 assign G[0] = A[0] & B[0];

 assign C[0] = Cin;

 generate

 genvar i;

 for (i = 1; i < 15; i = i + 1) begin

 assign P[i] = A[i] ^ B[i];

 assign G[i] = A[i] & B[i];

 assign C[i] = G[i-1] | (P[i-1] & C[i-1]);

 end

 endgenerate

 assign S = P ^ {C[14], C};

 assign Cout = G[14] | (P[14] & C[14]);

endmodule
