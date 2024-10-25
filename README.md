# Verilog_codes
# Four bit Carry look adder 


module FourBit_CLA(
    //input CLK,
    input  [3:0] A,
    input  [3:0] B,
    input  CARRYIN,
    output [3:0] SUM,
    output CARRYOUT
    );
    
    wire [3:0]P; // propagate 
    wire [3:0]G; // Generate
    wire [3:0]CARRY;// Carry 
    
    // Propagate and generate logic      
    assign  P[0] = A[0] ^ B[0] ; // propagate = A XOR B
    assign  P[1] = A[1] ^ B[1] ; // propagate = A XOR B
    assign  P[2] = A[2] ^ B[2] ; // propagate = A XOR B
    assign  P[3] = A[3] ^ B[3] ; // propagate = A XOR B
    
    assign  G[0] = A[0] & B[0] ; // Generate = A AND B 
    assign  G[1] = A[1] & B[1] ; // Generate = A AND B 
    assign  G[2] = A[2] & B[2] ; // Generate = A AND B 
    assign  G[3] = A[3] & B[3] ; // Generate = A AND B 
    
    // Carry Look-Ahead logic using a generate block
    
    assign CARRY[0] = CARRYIN ; // initail carry 
    assign CARRY[1] = G[0] | (P[0] & CARRY[0]) ;
    assign CARRY[2] = G[1] | (P[1] & CARRY[1]) ;
    assign CARRY[3] = G[2] | (P[2] & CARRY[2]) ; 
    assign CARRY[4] = G[3] | (P[3] & CARRY[3]) ; 
   
    // Final Carry out   
    assign CARRYOUT = CARRY[4] ; // Final carry-out calculation  
        
     // Sum Calculations
    
    assign SUM[0] = G[0] ^ P[0]  ;
    assign SUM[1] = G[1] ^ P[1]  ;
    assign SUM[2] = G[2] ^ P[2]  ; 
    assign SUM[3] = G[3] ^ P[3]  ; 
                    
                    
endmodule
