data_structure_final_project
void algorithm_A(Board board, Player player, int index[]){
    int row, col;
    int cap,orb;
    int color = player.get_color();
    int place[5][6] = {0};
    int rand_num;
    int tem_place_max = 0;
    int tem_row;
    int tem_col;
    place[0][0] = 2;
    place[0][5] = 2;
    place[4][0] = 2;
    place[4][5] = 2;
    for(int i=1 ; i<5 ; i++)
    {
    	place[0][i] = 1;
    	place[4][i] = 1;
    }
    for(int i=1 ; i<4 ; i++)
    {
    	place[i][0] = 1;
    	place[i][5] = 1;
    }
    int x,y,z,t;
    int tem;
    for(int i=0 ; i<5 ; i++)
    {
    	for(int j=0 ; j<6 ; j++)
    	{
    		x = y = z = t = 4;
    		if(board.get_cell_color(i, j) != color && board.get_cell_color(i, j) != 'w')
    		{
    			place[i][j] = 0;
    			continue;
    		}
    		cap = board.get_capacity(i,j);
			orb = board.get_orbs_num(i,j);
    		if(i-1 >= 0)
			{
				if(board.get_cell_color(i-1, j) != color && board.get_cell_color(i-1, j) != 'w')
				{
					x = board.get_capacity(i-1,j) - board.get_orbs_num(i-1,j);
				}
			}
			if(i+1 <= 4)
			{
				if(board.get_cell_color(i+1, j) != color && board.get_cell_color(i+1, j) != 'w')
				{
					y = board.get_capacity(i+1,j) - board.get_orbs_num(i+1,j);
				}	
			}
			if(j-1 >= 0)
			{
				if(board.get_cell_color(i, j-1) != color && board.get_cell_color(i, j-1) != 'w')
				{
					z = board.get_capacity(i,j-1) - board.get_orbs_num(i,j-1);
				}	
			}
			if(j+1 <= 5)
			{
				if(board.get_cell_color(i, j+1) != color && board.get_cell_color(i, j+1) != 'w')
				{
					t = board.get_capacity(i,j+1) - board.get_orbs_num(i,j+1);
				}	
			}
			if(x<y)
			{
				tem = y;
				y = x;
				x = tem;
			}
			if(x<z)
			{
				tem = z;
				z = x;
				x = tem;
			}
			if(x<t)
			{
				tem = t;
				t = x;
				x = tem;
			}
			if(y<z)
			{
				tem = z;
				z = y;
				y = tem;
			}
			if(y<t)
			{
				tem = t;
				t = y;
				y = tem;
			}
			if(z<t)
			{
				tem = t;
				t = z;
				z = tem;
			}
			if(cap-orb == 1)
			{
				if(t == 1)
				{
					place[i][j] += 10;
					if(z == 1)
					{
						place[i][j] += 10;
						if(y == 1)
						{
							place[i][j] += 10;
							if(x == 1)
							{
								place[i][j] += 10;
							}
						}
					}
				}
			}
			else
			{
				if(cap-orb <= t)
				{
					place[i][j] += 2;
					if(z != 4)
					{
						place[i][j] += 2;
						if(y != 4)
						{
							place[i][j] += 2;
							if(x != 4)
							{
								place[i][j] += 2;
							}
						}
					}
				}
				else
				{
					if(t == 1)
					{
						place[i][j] -=2;
						if(z == 1)
						{
							place[i][j] -= 2;
							if(y == 1)
							{
								place[i][j] -= 2;
								if(x == 1)
								{
									place[i][j] -= 2;
								}
							}
						}
					}
					else if(t == 2)
					{
						place[i][j] -= 1;
					}
					else if(t == 3)
					{
						place[i][j] += 0;
					}
					else
					{
						place[i][j] += 1;
					}
				}
			}
			if(tem_place_max < place[i][j])
			{
				tem_place_max = place[i][j];
				tem_row = i;
    			tem_col = j;
			}
    	}
    }
    index[0] = tem_row;
    index[1] = tem_col;
}