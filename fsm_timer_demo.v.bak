
/*========================================================
		 Timer Demo
===========================================================

Description:
	This Moore FSM detects the non-overlapping sequence
	101, assuming the input stream arrives LSB-first.

Design Engineer:
	Chrischele T. Palacios
	
Date: 
11 May2026
---------------------------------------------------------*/
	
module timer_demo(out,timer,state,t,clk,ovr,rst_n);
	//ports
	input  	 	     t;
	input 		   clk;
	input 		   ovr;
	input 	         rst_n;
	output reg	   out;
	output reg [3:0] timer;
	output reg [3:0] state;
	
	// state assignment
	localparam  [3:0] S0 = 4'b0000;
	localparam  [3:0] S1 = 4'b0001;
	localparam  [3:0] S2 = 4'b0010;
	localparam  [3:0] S3 = 4'b0011;
	reg [3:0] nxt; //nex state
	reg [3:0] pre; //pre state
	
	// input block
	always @(t,pre)begin
	 case (pre) 
		S0: nxt = t? S1:S0;
		S1: nxt = t? S1:S2;
		S2: nxt = t? S3:S0;
		S3: nxt = t? S1:S0;
		default: nxt = S0;
		endcase
	end
	
	
	// sequential block
	always @(posedge clk, negedge rst_n)begin
		if(!rst_n) pre <= S0;
		else       pre <= nxt;
	end
	
	
	// output block
	always @(pre)begin
	case (pre)
	 S0: begin 
		out = 0;
		state = S0;
	     end
	 S1: begin 
		out = 0;
		state = S1;
	     end
 	 S2: begin 
		out = 0;
		state = S2;
	     end
	 S3: begin 
		out = 1;
		state = S3;
	     end
	 
	 default: begin 
	         out = 0;
		 state = 0;
		end
	endcase
 end
endmodule