`define DisplayTimeExpire 32'd3000
`define MoveTimeExpire 32'd4000000

module snaake(clk, rst, now, right, left, up, down, reset, gameOver);

input clk, rst, right, left, up ,down, reset;   //rst==1是暫停，rst==0是繼續遊戲，reset是重新遊戲
output reg [23:0]now;
output reg gameOver;

reg [23:0]display[127:0]; //ex. 第一格亮:11111110 1000000000000000
reg [6:0]displayCount;  //計算顯示的圖片個數
reg [6:0]count[127:0]; //int count[127];
reg [2:0]direction;
integer i; 
reg[1:0] eat = 0;  //判斷是否吃到蘋果，有吃到為1
reg [6:0]map[127:0];   //int map[127]，只有用到int map[12]，產生點點
reg [3:0]j = 0;   //現在出現的蘋果為map[j]
reg [4:0]lenth;   //蛇的長度 
reg [6:0]temp;
reg [15:0]gameOverDisplay[127:0];
reg [4:0] gameOverDisplayCount;


wire displayTimeout, moveTimeout;   //計算時間除頻器的時間
clk_div V_clk_div(clk, rst, displayTimeout);   //顯示蛇現在有多長的除頻器(只能讓蛇固定，不能移動)
clk_move move_clk_div(clk, rst, moveTimeout);    //顯示蛇移動的除頻器(讓蛇移動)

initial
begin
	lenth = 2;  //初始化蛇長 = 2，顯示出來是1
	gameOverDisplay[0] = 0;
	gameOverDisplay[1] = 17;
	gameOverDisplay[2] = 34;
	gameOverDisplay[3] = 51;
	gameOverDisplay[4] = 68;
	gameOverDisplay[5] = 85;
	gameOverDisplay[6] = 102; 
	gameOverDisplay[7] = 119;
	gameOverDisplay[8] = 7;
	gameOverDisplay[9] = 22;
	gameOverDisplay[10] = 37;
	gameOverDisplay[11] = 52;
	gameOverDisplay[12] = 67;
	gameOverDisplay[13] = 82;
	gameOverDisplay[14] = 97;
	gameOverDisplay[15] = 112;
end


//切換顯示狀態
always@(posedge displayTimeout)
begin
	if(!rst && gameOver == 0)
	begin
		displayCount = displayCount + 1;     //displayCount初始值 = 0
		if(count[displayCount] != 0)
		begin
			now = display[count[displayCount]];   //顯示蛇
		end
		if(displayCount > lenth)
		begin
			now = display[map[j]];   //顯示蘋果
			displayCount = 0;   //把計算圖片數歸零
		end
	end
	if(gameOver == 1)
	begin
		now = display[gameOverDisplay[gameOverDisplayCount]];
		gameOverDisplayCount = gameOverDisplayCount + 1;
		if(gameOverDisplayCount > 15)
		begin
			gameOverDisplayCount = 0;
		end
	end
end


//切換移動狀態
always@(posedge moveTimeout)
begin
	if(!rst)
	begin    //記下每個點亮的表示方法
		display[0] = 24'b111111101000000000000000;
		display[1] = 24'b111111100100000000000000;
		display[2] = 24'b111111100010000000000000;
		display[3] = 24'b111111100001000000000000;
		display[4] = 24'b111111100000100000000000;
		display[5] = 24'b111111100000010000000000;
		display[6] = 24'b111111100000001000000000;
		display[7] = 24'b111111100000000100000000;
		display[8] = 24'b111111100000000010000000;
		display[9] = 24'b111111100000000001000000;
		display[10] = 24'b111111100000000000100000;
		display[11] = 24'b111111100000000000010000;
		display[12] = 24'b111111100000000000001000;
		display[13] = 24'b111111100000000000000100;
		display[14] = 24'b111111100000000000000010;
		display[15] = 24'b111111100000000000000001;
		display[16] = 24'b111111011000000000000000;
		display[17] = 24'b111111010100000000000000;
		display[18] = 24'b111111010010000000000000;
		display[19] = 24'b111111010001000000000000;
		display[20] = 24'b111111010000100000000000;
		display[21] = 24'b111111010000010000000000;
		display[22] = 24'b111111010000001000000000;
		display[23] = 24'b111111010000000100000000;
		display[24] = 24'b111111010000000010000000;
		display[25] = 24'b111111010000000001000000;
		display[26] = 24'b111111010000000000100000;
		display[27] = 24'b111111010000000000010000;
		display[28] = 24'b111111010000000000001000;
		display[29] = 24'b111111010000000000000100;
		display[30] = 24'b111111010000000000000010;
		display[31] = 24'b111111010000000000000001;
		display[32] = 24'b111110111000000000000000;
		display[33] = 24'b111110110100000000000000;
		display[34] = 24'b111110110010000000000000;
		display[35] = 24'b111110110001000000000000;
		display[36] = 24'b111110110000100000000000;
		display[37] = 24'b111110110000010000000000;
		display[38] = 24'b111110110000001000000000;
		display[39] = 24'b111110110000000100000000;
		display[40] = 24'b111110110000000010000000;
		display[41] = 24'b111110110000000001000000;
		display[42] = 24'b111110110000000000100000;
		display[43] = 24'b111110110000000000010000;
		display[44] = 24'b111110110000000000001000;
		display[45] = 24'b111110110000000000000100;
		display[46] = 24'b111110110000000000000010;
		display[47] = 24'b111110110000000000000001;
		display[48] = 24'b111101111000000000000000;
		display[49] = 24'b111101110100000000000000;
		display[50] = 24'b111101110010000000000000;
		display[51] = 24'b111101110001000000000000;
		display[52] = 24'b111101110000100000000000;
		display[53] = 24'b111101110000010000000000;
		display[54] = 24'b111101110000001000000000;
		display[55] = 24'b111101110000000100000000;
		display[56] = 24'b111101110000000010000000;
		display[57] = 24'b111101110000000001000000;
		display[58] = 24'b111101110000000000100000;
		display[59] = 24'b111101110000000000010000;
		display[60] = 24'b111101110000000000001000;
		display[61] = 24'b111101110000000000000100;
		display[62] = 24'b111101110000000000000010;
		display[63] = 24'b111101110000000000000001;
		display[64] = 24'b111011111000000000000000;
		display[65] = 24'b111011110100000000000000;
		display[66] = 24'b111011110010000000000000;
		display[67] = 24'b111011110001000000000000;
		display[68] = 24'b111011110000100000000000;
		display[69] = 24'b111011110000010000000000;
		display[70] = 24'b111011110000001000000000;
		display[71] = 24'b111011110000000100000000;
		display[72] = 24'b111011110000000010000000;
		display[73] = 24'b111011110000000001000000;
		display[74] = 24'b111011110000000000100000;
		display[75] = 24'b111011110000000000010000;
		display[76] = 24'b111011110000000000001000;
		display[77] = 24'b111011110000000000000100;
		display[78] = 24'b111011110000000000000010;
		display[79] = 24'b111011110000000000000001;
		display[80] = 24'b110111111000000000000000;
		display[81] = 24'b110111110100000000000000;
		display[82] = 24'b110111110010000000000000;
		display[83] = 24'b110111110001000000000000;
		display[84] = 24'b110111110000100000000000;
		display[85] = 24'b110111110000010000000000;
		display[86] = 24'b110111110000001000000000;
		display[87] = 24'b110111110000000100000000;
		display[88] = 24'b110111110000000010000000;
		display[89] = 24'b110111110000000001000000;
		display[90] = 24'b110111110000000000100000;
		display[91] = 24'b110111110000000000010000;
		display[92] = 24'b110111110000000000001000;
		display[93] = 24'b110111110000000000000100;
		display[94] = 24'b110111110000000000000010;
		display[95] = 24'b110111110000000000000001;
		display[96] = 24'b101111111000000000000000;
		display[97] = 24'b101111110100000000000000;
		display[98] = 24'b101111110010000000000000;
		display[99] = 24'b101111110001000000000000;
		display[100] = 24'b101111110000100000000000;
		display[101] = 24'b101111110000010000000000;
		display[102] = 24'b101111110000001000000000;
		display[103] = 24'b101111110000000100000000;
		display[104] = 24'b101111110000000010000000;
		display[105] = 24'b101111110000000001000000;
		display[106] = 24'b101111110000000000100000;
		display[107] = 24'b101111110000000000010000;
		display[108] = 24'b101111110000000000001000;
		display[109] = 24'b101111110000000000000100;
		display[110] = 24'b101111110000000000000010;
		display[111] = 24'b101111110000000000000001;
		display[112] = 24'b011111111000000000000000;
		display[113] = 24'b011111110100000000000000;
		display[114] = 24'b011111110010000000000000;
		display[115] = 24'b011111110001000000000000;
		display[116] = 24'b011111110000100000000000;
		display[117] = 24'b011111110000010000000000;
		display[118] = 24'b011111110000001000000000;
		display[119] = 24'b011111110000000100000000;
		display[120] = 24'b011111110000000010000000;
		display[121] = 24'b011111110000000001000000;
		display[122] = 24'b011111110000000000100000;
		display[123] = 24'b011111110000000000010000;
		display[124] = 24'b011111110000000000001000;
		display[125] = 24'b011111110000000000000100;
		display[126] = 24'b011111110000000000000010;
		display[127] = 24'b011111110000000000000001;
		
		//蘋果的位置，蘋果用這12顆下去跑
		map[0] = 18;
		map[1] = 92;
		map[2] = 70;
		map[3] = 50;
		map[4] = 100;
		map[5] = 40;
		map[6] = 81;
		map[7] = 29;
		map[8] = 60;
		map[9] = 99;
		map[10] = 29;
		map[11] = 115;
		
		if(!reset)   //按了reset後
		begin
			case(lenth)    //把所有本來亮的都歸零
				2:
				begin
					for(i = 0; i < 2; i = i + 1)
					begin
						count[i] = 0;
					end
				end
				3:
				begin
					for(i = 0; i < 3; i = i + 1)
					begin
						count[i] = 0;
					end
				end
				4:
				begin
					for(i = 0; i < 4; i = i + 1)
					begin
						count[i] = 0;
					end
				end
				5:
				begin
					for(i = 0; i < 5; i = i + 1)
					begin
						count[i] = 0;
					end
				end
				6:
				begin
					for(i = 0; i < 6; i = i + 1)
					begin
						count[i] = 0;
					end
				end
				7:
				begin
					for(i = 0; i < 7; i = i + 1)
					begin
						count[i] = 0;
					end
				end
				8:
				begin
					for(i = 0; i < 8; i = i + 1)
					begin
						count[i] = 0;
					end
				end
				9:
				begin
					for(i = 0; i < 9; i = i + 1)
					begin
						count[i] = 0;
					end
				end
				10:
				begin
					for(i = 0; i < 10; i = i + 1)
					begin
						count[i] = 0;
					end
				end
				11:
				begin
					for(i = 0; i < 11; i = i + 1)
					begin
						count[i] = 0;
					end
				end
				12:
				begin
					for(i = 0; i < 12; i = i + 1)
					begin
						count[i] = 0;
					end
				end
				13:
				begin
					for(i = 0; i < 13; i = i + 1)
					begin
						count[i] = 0;
					end
				end
				14:
				begin
					for(i = 0; i < 14; i = i + 1)
					begin
						count[i] = 0;
					end
				end
			endcase
			lenth = 2;
			gameOver = 0;
		end
		if(eat == 1)  //如果吃到蘋果
		begin
			if(j < 11)  //map[j]，(map是存蘋果位置)，就讓蘋果移到下一個位置
			begin
				j = j + 1;
			end
			else    //如果超出蘋果map陣列的數量
			begin
				j = 0;   //把陣列數量歸零，從map[0]開始跑
			end
			eat = 0;   //把eat歸零，下一次吃到蘋果的時候會再=1
		end
		if(count[lenth - 1] == map[j])    //如果吃到蘋果(蛇的頭跟蘋果的位置一樣)
		begin
			if(lenth < 15)
			begin
				count[lenth] = map[j];   //把蘋果加到頭的下一個
				lenth = lenth + 1;    //蛇的長度加1
			end
			eat = 1;     //吃到蘋果
		end
		
		
		if(!right)
		begin
			direction = 1;
		end
		if(!left)
		begin
			direction = 2;
		end
		if(!up)
		begin
			direction = 3;
		end
		if(!down)
		begin
			direction = 4;
		end
		case(lenth)  //把蛇移動到下一個位置，除了頭之外其他的身節都會移動
				2:
				begin
					for(i = 0; i < 1; i = i + 1)     
					begin
						count[i] = count[i + 1];
					end
				end
				3:
				begin
					for(i = 0; i < 2; i = i + 1)
					begin
						count[i] = count[i + 1];
					end
				end
				4:
				begin
					for(i = 0; i < 3; i = i + 1)
					begin
						count[i] = count[i + 1];
					end
				end
				5:
				begin
					for(i = 0; i < 4; i = i + 1)
					begin
						count[i] = count[i + 1];
					end
				end
				6:
				begin
					for(i = 0; i < 5; i = i + 1)
					begin
						count[i] = count[i + 1];
					end
				end
				7:
				begin
					for(i = 0; i < 6; i = i + 1)
					begin
						count[i] = count[i + 1];
					end
				end
				8:
				begin
					for(i = 0; i < 7; i = i + 1)
					begin
						count[i] = count[i + 1];
					end
				end
				9:
				begin
					for(i = 0; i < 8; i = i + 1)
					begin
						count[i] = count[i + 1];
					end
				end
				10:
				begin
					for(i = 0; i < 9; i = i + 1)
					begin
						count[i] = count[i + 1];
					end
				end
				11:
				begin
					for(i = 0; i < 10; i = i + 1)
					begin
						count[i] = count[i + 1];
					end
				end
				12:
				begin
					for(i = 0; i < 11; i = i + 1)
					begin
						count[i] = count[i + 1];
					end
				end
				13:
				begin
					for(i = 0; i < 12; i = i + 1)
					begin
						count[i] = count[i + 1];
					end
				end
				14:
				begin
					for(i = 0; i < 13; i = i + 1)
					begin
						count[i] = count[i + 1];
					end
				end
				15:
				begin
					for(i = 0; i < 14; i = i + 1)
					begin
						count[i] = count[i + 1];
					end
				end
				16:
				begin
					for(i = 0; i < 15; i = i + 1)
					begin
						count[i] = count[i + 1];
					end
				end
			endcase
		case(direction)   //按了哪個方向
			3'b001:    //右
			begin
				if(count[lenth - 1] == 15 || count[lenth - 1] == 31 || count[lenth - 1] == 47 || count[lenth - 1] == 63 || count[lenth - 1] == 79 ||count[lenth - 1] == 95 || count[lenth - 1] == 111 || count[lenth - 1] == 127)
				//當蛇往右移動碰到右邊的邊界時
				begin
					count[lenth - 1] = count[lenth - 1] - 15;   //頭會回到那一橫排的最左邊重新往右跑
				end
				else
				begin
					count[lenth - 1] = count[lenth - 1] + 1;   //把蛇的頭往右移，剩下蛇身的位置會在前面的程式碼執行(count[i] = count[i+1])，讓每一個蛇的點都移到下一個位置
				end
			end
			3'b010:   //左
			begin 
				if(count[lenth - 1] == 0 || count[lenth - 1] == 16 || count[lenth - 1] == 32 || count[lenth - 1] == 48 || count[lenth - 1] == 64 ||count[lenth - 1] == 80 || count[lenth - 1] == 96 || count[lenth - 1] == 112)
				//當蛇往左移動碰到左邊的邊界時
				begin
					count[lenth - 1] = count[lenth - 1] + 15;   //頭會回到那一橫排的最右邊重新往左跑
				end
				else
				begin
				count[lenth - 1] = count[lenth - 1] - 1;   //把蛇的頭往左移
				end
			end
			3'b011:   //上
			begin 
				count[lenth - 1] = count[lenth - 1] - 16;   //把蛇的頭往上移
			end
			3'b100:   //下
			begin
				count[lenth - 1] = count[lenth - 1] + 16;  //把蛇的頭往下移
			end
			endcase
			temp = lenth - 1;
		case(temp)  
				1:
				begin
					for(i = 0; i < 1; i = i + 1)
					begin
						if(count[temp] == count[i])
						begin
							gameOver = 1;
						end
					end
				end
				2:
				begin
					for(i = 0; i < 2; i = i + 1)
					begin
						if(count[temp] == count[i])
						begin
							gameOver = 1;
						end
					end
				end
				3:
				begin
					for(i = 0; i < 3; i = i + 1)
					begin
						if(count[temp] == count[i])
						begin
							gameOver = 1;
						end
					end
				end
				4:
				begin
					for(i = 0; i < 4; i = i + 1)
					begin
						if(count[temp] == count[i])
						begin
							gameOver = 1;
						end
					end
				end
				5:
				begin
					for(i = 0; i < 5; i = i + 1)
					begin
						if(count[temp] == count[i])
						begin
							gameOver = 1;
						end
					end
				end
				6:
				begin
					for(i = 0; i < 6; i = i + 1)
					begin
						if(count[temp] == count[i])
						begin
							gameOver = 1;
						end
					end
				end
				7:
				begin
					for(i = 0; i < 7; i = i + 1)
					begin
						if(count[temp] == count[i])
						begin
							gameOver = 1;
						end
					end
				end
				8:
				begin
					for(i = 0; i < 8; i = i + 1)
					begin
						if(count[temp] == count[i])
						begin
							gameOver = 1;
						end
					end
				end
				9:
				begin
					for(i = 0; i < 9; i = i + 1)
					begin
						if(count[temp] == count[i])
						begin
							gameOver = 1;
						end
					end
				end
				10:
				begin
					for(i = 0; i < 10; i = i + 1)
					begin
						if(count[temp] == count[i])
						begin
							gameOver = 1;
						end
					end
				end
				11:
				begin
					for(i = 0; i < 11; i = i + 1)
					begin
						if(count[temp] == count[i])
						begin
							gameOver = 1;
						end
					end
				end
				12:
				begin
					for(i = 0; i < 12; i = i + 1)
					begin
						if(count[temp] == count[i])
						begin
							gameOver = 1;
						end
					end
				end
				13:
				begin
					for(i = 0; i < 13; i = i + 1)
					begin
						if(count[temp] == count[i])
						begin
							gameOver = 1;
						end
					end
				end
				14:
				begin
					for(i = 0; i < 14; i = i + 1)
					begin
						if(count[temp] == count[i])
						begin
							gameOver = 1;
						end
					end
				end
			endcase
	end
end
endmodule


//除頻器
module clk_div(clk, rst, div_clk);
input clk, rst;
output div_clk;

reg div_clk;
reg [31:0]count;

always@(posedge clk)
begin
	if(rst)
	begin
		count <= 32'd0;
		div_clk <= 1'b0;
	end
	else
	begin
		if(count == `DisplayTimeExpire)
		begin
			count <= 32'd0;
			div_clk <= ~div_clk;
		end
		else
		begin
			count <= count + 32'd1;
			div_clk <= div_clk;
		end
	end
end
endmodule


module clk_move(clk, rst, div_clk);
input clk, rst;
output div_clk;

reg div_clk;
reg [31:0]count;

always@(posedge clk)
begin
	if(rst)
	begin
		count <= 32'd0;
		div_clk <= 1'b0;
	end
	else
	begin
		if(count == `MoveTimeExpire)
		begin
			count <= 32'd0;
			div_clk <= ~div_clk;
		end
		else
		begin
			count <= count + 32'd1;
			div_clk <= div_clk;
		end
	end
end
endmodule
