# Funky Chess Board


- Description:
    A knight is a piece used in the game of chess. The chessboard itself is square array of cells. Each time a knight moves, its resulting position is two rows and one column, or two columns and one row away from its starting position. Thus a knight starting on row r, column c – which we’ll denote as (r,c) – can move to any of the squares (r-2,c-1), (r-2,c+1), (r-1,c-2), (r-1,c+2), (r+1,c-2), (r+1,c+2), (r+2,c-1), or (r+2,c+1). Of course, the knight may not move to any square that is not on the board.


    Suppose the chessboard is not square, but instead has rows with variable numbers of columns, and with each row offset zero or more columns to the right of the row above it. The figure to the left illustrates one possible configuration. How many of the squares in such a modified chessboard can a knight, starting in the upper left square (marked with	an asterisk), not reach in any number of moves without resting in any square more than once? Minimize this number.

    ![Imgur](https://i.imgur.com/05Pl2xt.png)

    If necessary, the knight is permitted to pass over regions that are outside the borders of the modified chessboard, but as usual, it can only move to squares that are within the borders of the board. 

- Constraints: 
    The maximum dimensions of the board will be 10 rows and 10 columns. That is, any modified chessboard specified by the input will fit completely on a 10 row, 10 column board.

- Input Format: First line contains an integer <b><i>n</i></b>, representing the side of     square of chess board.
    The next <b><i>n</i></b> line contains <b><i>n</i></b> integers separated by single spaces in which j<sub>jth</sub> integer is 1 if that cell(i,j) is part of chessboard and 0 otherwise.
    
     - Sample Input: 3
        1 1 1
        1 1 1
        1 1 1
        Output Format: Print the minimum number of squares that the knight can not reach.
     - Sample Output: 1

- Solution

```
#include<iostream>
#include<stdio.h>
#include<stdlib.h>
using namespace std;

int n,cols,empty,board[10][10],sum=0,hi;

void set(int i,int j,int count){
    if(i<0 || i>=10 || j<0 || j>=10 || board[i][j] == 0)
        return;
    int ans = 0;
    board[i][j] = 0;//unsets the (i,j) cell
    hi = max(hi,count+1);//hi stores the maximum of value of visited squares
    //try all 8 possible moves for knight
    set(i-1,j-2,count+1);
    set(i-2,j-1,count+1);
    set(i+1,j-2,count+1);
    set(i+2,j-1,count+1);
    set(i-1,j+2,count+1);
    set(i-2,j+1,count+1);
    set(i+1,j+2,count+1);
    set(i+2,j+1,count+1);
    board[i][j] = 1;//sets (i,j) cell again(backtracking)
}
int main(){
	cin>>n;
    sum = 0;
    for(int i=0;i<n;i++){
        for(int j=0;j<n;j++){
        	cin>>board[i][j];
        	if(board[i][j])
        		sum++; // sum stroes total number of valid cells on chessboard
        }
    }
	hi=0;
	set(0,0,0);
    cout<<sum-hi<<"\n";
    return 0;
}
```