#include <iostream>

void printField(char field[3][3])//create field
{
    system("cls");
    std::cout << "   0 1 2 \n";
    std::cout << "  -------\n";
    for (int i = 0; i < 3; i++)
    {
        std::cout << i << " |";
        for (int j = 0; j < 3; j++)
        {
            std::cout << field[i][j] << "|";
        }
        std::cout << (i != 2 ? "\n  |-|-|-|\n" : "\n  -------\n");
    }
}

void Move(char Player, char field[3][3], int& occupiedCells)
{
    bool flag = true;
    do
    {
        int i, j;
        std::cout << "Player " << Player << " choose unoccupied cell\n";//player's move
        std::cin >> i >> j;
        flag = (field[i][j] != ' ' || i < 0 || i > 2 || j < 0 || j > 2);//checking the field and occupied cell
        if (flag)
            std::cout << "Please, make another choice\n";
        else
        {
            field[i][j] = Player;
            occupiedCells++;
        }
    } while (flag);
}

bool haveWinner(char& winner, char field[3][3]) //check for winner
{
    for (int i = 0; i < 3; i++)
    {
        if (field[i][0] == field[i][1] && field[i][0] == field[i][2]) //horizontal
        {
            winner = field[i][0];
            if (winner != ' ')
                return true;
        }
        if (field[0][i] == field[1][i] && field[0][i] == field[2][i]) //vertical
        {
            winner = field[0][i];
            if (winner != ' ')
                return true;
        }
    }
    if (field[0][0] == field[1][1] && field[0][0] == field[2][2]) // first diagonal
    {
        winner = field[1][1];
        if (winner != ' ')
            return true;
    }
    if (field[0][2] == field[1][1] && field[0][2] == field[2][0]) // second diagonal
    {
        winner = field[1][1];
        if (winner != ' ')
            return true;
    }
    return false;
}

int main()
{
    char field[3][3] = {
      { ' ', ' ', ' ' },
      { ' ', ' ', ' ' },
      { ' ', ' ', ' ' },
    };
    char winner = ' ';
    printField(field);
    char players[] = { 'x', 'o' };
    int occupiedCells = 0;
    for (int i = 0; !haveWinner(winner, field) && occupiedCells != 9; i++) {
        Move(players[i % 2], field, occupiedCells);
        printField(field);
    }
    if (winner != ' ')
        std::cout << winner << " wins\n";
    else
        std::cout << "Draft\n";
    return 0;
}
