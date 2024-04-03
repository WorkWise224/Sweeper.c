# Sweeper.c


*
  Minesweeper 
  finish  gridFinished function
  print a message if they win 

  
  
  


*/

#include <stdio.h>
#include <stdlib.h> //rand
#include <time.h>

#define MAX_SIZE 20
#define BLANK -1
#define BOMB 9


void printGrid( const int b_grid[MAX_SIZE][MAX_SIZE], int n);
void nukeGrid( int b_grid[MAX_SIZE][MAX_SIZE], int n);
void placeBombs( int b_grid[MAX_SIZE][MAX_SIZE], int n, int numBombs);
int countSurroundingBombs(const int b_grid[MAX_SIZE][MAX_SIZE], int n, int r, int c);
void printBombCounts(const  int b_grid[MAX_SIZE][MAX_SIZE], int n);
void takeMove( int b_grid[MAX_SIZE][MAX_SIZE], int n, int r, int c);
char gridFinished(int b_grid[MAX_SIZE][MAX_SIZE], int n);

int main()
{
	int grid[MAX_SIZE][MAX_SIZE] = {{0}};
	int n = 10; //play on a 6 by 6 grid
	int row, col;
	
	nukeGrid(grid, n);

	placeBombs(grid, n, 8);
		printGrid(grid, n);
		
	printf("\n");
//	   printBombCounts(grid, n);
	do{
	
		printf("enter the row and col: ");
		scanf("%d%d", &row, &col);
		if (grid[row][col]==BOMB){
			printf("Sorry, you are dead\n");
		}else{
			takeMove(grid, n, row, col);
		}
		
			printGrid(grid, n);
			printf("\n");
			
	}while(grid[row][col]!=BOMB && !gridFinished(grid,n) );
	
	//print a message if they win
	
   
	return 0;
}

void nukeGrid(int b_grid[MAX_SIZE][MAX_SIZE], int n)
{
	int i, j;
	
	for (i = 0; i < n; ++i){
		for (j = 0; j < n; ++j){
		     b_grid[i][j] = BLANK;
		}//for j
		
	}//for i
	
}

void printGrid(const int b_grid[MAX_SIZE][MAX_SIZE], int n)
{
	int i, j;
	
	for (i = 0; i < n; ++i){
		for (j = 0; j < n; ++j){
			if (b_grid[i][j] == BOMB || b_grid[i][j] == BLANK)
				printf(" * ", b_grid[i][j]);
			else
		       printf("%3d", b_grid[i][j]);
		}//for j
		printf("\n");	
	}//for i
}

void printBombCounts(const int b_grid[MAX_SIZE][MAX_SIZE], int n)
{
	int i, j;
	
	for (i = 0; i < n; ++i){
		for (j = 0; j < n; ++j){
		    printf("%3d", countSurroundingBombs(b_grid, n, i, j));
		}//for j
		printf("\n");	
	}//for i
}

void placeBombs(int b_grid[MAX_SIZE][MAX_SIZE], int n, int numBombs)
{
	int row, col, i;
	
	for(i = 0; i < numBombs; ++i){
		do{
			row = getRand(0, n-1);
	        col = getRand(0, n-1);
		}while( b_grid[row][col] == BOMB);
		
	
	         b_grid[row][col] = BOMB;
	}
}


int countSurroundingBombs(const int b_grid[MAX_SIZE][MAX_SIZE], int n, int r, int c)
{
	int count = 0;
	
	//top row
	if (b_grid[r-1][c-1] == BOMB){
		++count;
	}
	if (b_grid[r-1][c] == BOMB){
		++count;
	}
	if (b_grid[r-1][c+1] == BOMB){
		++count;
	}
	//middle row
	if (b_grid[r][c-1] == BOMB){
		++count;
	}
	if (b_grid[r][c + 1] == BOMB){
		++count;
	}
	
	//bottom row
	if (b_grid[r+1][c-1] == BOMB){
		++count;
	}
	if (b_grid[r+1][c] == BOMB){
		++count;
	}
	if (b_grid[r+1][c+1] == BOMB){
		++count;
	}


	return count;
}

void takeMove( int b_grid[MAX_SIZE][MAX_SIZE], int n, int r, int c)
{
	
	if (b_grid[r][c] == BLANK){
		int count = countSurroundingBombs(b_grid, n, r, c);
		b_grid[r][c] = count;
		
		if (count == 0){
			int row, col;
			
			
			row = r -1; col = c-1;
			if (row >= 0 && row < n && col >= 0 && col <n)
				takeMove(b_grid, n, row, col);
				
			row = r -1; col = c;
			if (row >= 0 && row < n && col >= 0 && col <n)
				takeMove(b_grid, n, row, col);
				
				row = r -1; col = c+1;
			if (row >= 0 && row < n && col >= 0 && col <n)
				takeMove(b_grid, n, row, col);
			//middle row	
			row = r; col = c-1;
			if (row >= 0 && row < n && col >= 0 && col <n)
				takeMove(b_grid, n, row, col);
				
			row = r; col = c+1;
			if (row >= 0 && row < n && col >= 0 && col <n)
				takeMove(b_grid, n, row, col);
			
			//bottom row	
				row = r +1; col = c-1;
			if (row >= 0 && row < n && col >= 0 && col <n)
				takeMove(b_grid, n, row, col);
				
			row = r +1; col = c;
			if (row >= 0 && row < n && col >= 0 && col <n)
				takeMove(b_grid, n, row, col);
				
				row = r+1; col = c+1;
			if (row >= 0 && row < n && col >= 0 && col <n)
				takeMove(b_grid, n, row, col);
				
			
			
		}
		
		
	}
	
}

int getRand(int start, int end)
{	
	int nums;
	static char firstTime = 1;
	
	
	if (firstTime){
		srand(time(NULL));
		firstTime = 0;
	}

	nums = end - start + 1;



	return rand()%nums + start;
}

/*
	search the grid of BLANKS, if you find  a blank
	return 0;
	if no blanks
	return 1

*/

char gridFinished(int b_grid[MAX_SIZE][MAX_SIZE], int n)
{
	
	
	return 0;
}
