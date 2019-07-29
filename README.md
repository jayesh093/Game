//Implementation of Tic-Tac-Toe game
//Rules of the Game

//The game is to be played between two people (in this program between HUMAN and COMPUTER).
//One of the player chooses ‘O’ and the other ‘X’ to mark their respective cells.
//The game starts with one of the players and the game ends when one of the players has one whole row/ column/ diagonal filled with //his/her respective character (‘O’ or ‘X’).
//If no one wins, then the game is said to be draw.



#include<bits/stdc++.h>
using namespace std;

#define COMPUTER 1
#define HUMAN 2

#define SIDE 3 // Length of the board

// Computer will move with 'O'
// and human with 'X'
#define COMPUTERMOVE 'O'
#define HUMANMOVE 'X'

char winner=NULL;

// A function to initialise the game

void initialise(char board[][SIDE],int moves[]){

    // Initially the board is empty
    for(int i=0;i<SIDE;i++){
        for(int j=0;j<SIDE;j++){
            board[i][j]=' ';
        }
    }
    // Fill the moves with numbers
    for(int i=0;i<SIDE*SIDE;i++){
        moves[i]=i;
    }
    return;
}
void showInstructions(){
        printf("\t\t\t  Tic-Tac-Toe\n\n");
    printf("Choose a cell numbered from 1 to 9 as below"
            " and play\n\n");

    printf("\t\t\t  1 | 2  | 3  \n");
    printf("\t\t\t--------------\n");
    printf("\t\t\t  4 | 5  | 6  \n");
    printf("\t\t\t--------------\n");
    printf("\t\t\t  7 | 8  | 9  \n\n");

    printf("-\t-\t-\t-\t-\t-\t-\t-\t-\t-\n\n");

    return;


}
// A function to show the current board status
void showBoard(char board[][SIDE])
{
    printf("\n\n");

    printf("\t\t\t  %c | %c  | %c  \n", board[0][0],
                             board[0][1], board[0][2]);
    printf("\t\t\t--------------\n");
    printf("\t\t\t  %c | %c  | %c  \n", board[1][0],
                             board[1][1], board[1][2]);
    printf("\t\t\t--------------\n");
    printf("\t\t\t  %c | %c  | %c  \n\n", board[2][0],
                             board[2][1], board[2][2]);

    return;
}

// A function that returns true if any of the row
// is crossed with the same player's move

bool rowCrossed(char board[][SIDE]){
    for(int i=0;i<SIDE;i++){
        if(board[i][0]==board[i][1]&&
           board[i][1]==board[i][2]&&
           board[i][0]!=' '){
            winner=board[i][0];
            return(true);
        }
    }
    return(false);
}

// A function that returns true if any of the column
// is crossed with the same player's move
bool columnCrossed(char board[][SIDE])
{
    for (int i=0; i<SIDE; i++)
    {
        if (board[0][i] == board[1][i] &&
            board[1][i] == board[2][i] &&
            board[0][i] != ' '){
            winner=board[0][i];
            return (true);
            }
    }
    return(false);
}

// A function that returns true if any of the diagonal
// is crossed with the same player's move
bool diagonalCrossed(char board[][SIDE])
{
    if (board[0][0] == board[1][1] &&
        board[1][1] == board[2][2] &&
        board[0][0] != ' '){
        winner=board[0][0];
        return(true);
        }

    if (board[0][2] == board[1][1] &&
        board[1][1] == board[2][0] &&
        board[0][2] != ' '){
        winner=board[0][2];
        return(true);
         }

    return(false);
}



// A function that returns true if the game is over
// else it returns a false

bool gameOver(char board[][SIDE]){
    return(rowCrossed(board)||columnCrossed(board)||diagonalCrossed(board));
}

//Fill the Board According To player who enter the number
void fillNumber(int n,char board[][SIDE],char c){
    switch(n){
case 1:
    board[0][0]=c;
    break;
case 2:
    board[0][1]=c;
    break;
case 3:
    board[0][2]=c;
    break;
case 4:
    board[1][0]=c;
    break;
case 5:
    board[1][1]=c;
    break;
case 6:
    board[1][2]=c;
    break;
case 7:
    board[2][0]=c;
    break;
case 8:
    board[2][1]=c;
    break;
case 9:
    board[2][2]=c;
    break;
    }
}


// A function to play Tic-Tac-Toe
void  playTicTacToe(int whoseTurn){

        // A 3*3 Tic-Tac-Toe board for playing
        char board[SIDE][SIDE];

        int moves[SIDE*SIDE];

        // Initialise the game

        initialise(board,moves);

        // Show the instructions before playing

        showInstructions();

        int moveIndex = 0, x, y;

        // Keep playing till the game is over or it is a draw

        while(gameOver(board)==false && moveIndex!=SIDE*SIDE){

            if(whoseTurn==COMPUTER){
                cout<<"Computer Turn Enter 1 To 9:"<<endl;
                cin>>x;
                fillNumber(x,board,COMPUTERMOVE);
                showBoard(board);
                moveIndex ++;
                whoseTurn = HUMAN;

            }
            else if(whoseTurn==HUMAN){
                cout<<"Human Turn Enter 1 To 9:"<<endl;
                cin>>x;
                fillNumber(x,board,HUMANMOVE);
                showBoard(board);
                moveIndex ++;
                whoseTurn = COMPUTER;

            }

        }
        if (gameOver(board) == false &&  moveIndex == SIDE * SIDE)
        cout<<"It's a draw"<<endl;
    else{
        if (winner == HUMANMOVE)
           cout<<"HUMAN has won"<<endl;
        else if (winner ==COMPUTERMOVE )
            cout<<"COMPUTER has won"<<endl;
        else if(winner==NULL){
            cout<<"It's a draw"<<endl;
        }
    }


};

int main()
{
    // Let us play the game with COMPUTER starting first
    bool t=true;
    char cc;
    do{
    int n;
    cout<<"Let us play the game with COMPUTER and HUMAN"<<endl;
    cout<<"1 Press for First Start game Of HUMAN Symbol 'X' "<<endl;
    cout<<"2 Press for First Start game Of COMPUTER Symbol 'o'  "<<endl;
    cin>>n;
   if(n==1){
    playTicTacToe(HUMAN);
   }else if(n==2)
   {
       playTicTacToe(COMPUTER);
   }else{
    cout<<"Invalid  Choice"<<endl;
   }

   up:
    cout<<"Do You Want to Continues game then Press Y/N"<<endl;
    cin>>cc;
    if(cc=='Y' || cc=='y'){
        t=true;
    }else if(cc=='N' || cc=='n'){
        t=false;
     }else{
     cout<<"Invalid Choice"<<endl;
    cout<<"Re-Enter Choice"<<endl;
     goto up;
     }
    }while(t);
    return (0);
}
