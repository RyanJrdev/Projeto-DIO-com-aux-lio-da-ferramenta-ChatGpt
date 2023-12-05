#include <stdio.h>

// Fun��o para exibir o tabuleiro
void exibirTabuleiro(char tabuleiro[3][3]) {
    printf("\n  1   2   3\n");
    for (int i = 0; i < 3; i++) {
        printf(" -------------\n");
        printf("%c|%c|%c| %d\n", tabuleiro[i][0], tabuleiro[i][1], tabuleiro[i][2], i + 1);
    }
    printf(" -------------\n");
}

// Fun��o para verificar se h� um vencedor
int verificarVencedor(char tabuleiro[3][3]) {
    // Verificar linhas e colunas
    for (int i = 0; i < 3; i++) {
        if (tabuleiro[i][0] == tabuleiro[i][1] && tabuleiro[i][1] == tabuleiro[i][2] && tabuleiro[i][0] != ' ')
            return 1; // Vencedor nas linhas
        if (tabuleiro[0][i] == tabuleiro[1][i] && tabuleiro[1][i] == tabuleiro[2][i] && tabuleiro[0][i] != ' ')
            return 1; // Vencedor nas colunas
    }

    // Verificar diagonais
    if (tabuleiro[0][0] == tabuleiro[1][1] && tabuleiro[1][1] == tabuleiro[2][2] && tabuleiro[0][0] != ' ')
        return 1; // Vencedor na diagonal principal
    if (tabuleiro[0][2] == tabuleiro[1][1] && tabuleiro[1][1] == tabuleiro[2][0] && tabuleiro[0][2] != ' ')
        return 1; // Vencedor na diagonal secund�ria

    return 0; // Sem vencedor
}

// Fun��o para verificar se o movimento � v�lido
int verificarMovimento(char tabuleiro[3][3], int linha, int coluna) {
    return tabuleiro[linha][coluna] == ' ';
}

// Fun��o principal
int main() {
    char tabuleiro[3][3] = {{' ', ' ', ' '}, {' ', ' ', ' '}, {' ', ' ', ' '}};
    int linha, coluna, jogador = 1, movimentoValido, totalJogadas = 0;

    do {
        exibirTabuleiro(tabuleiro);

        // Alternar entre os jogadores
        jogador = (jogador % 2) ? 1 : 2;

        printf("\nJogador %d, fa�a sua jogada (linha e coluna): ", jogador);
        scanf("%d %d", &linha, &coluna);

        // Verificar se o movimento � v�lido
        movimentoValido = verificarMovimento(tabuleiro, linha - 1, coluna - 1);

        if (movimentoValido) {
            // Realizar a jogada
            tabuleiro[linha - 1][coluna - 1] = (jogador == 1) ? 'X' : 'O';
            totalJogadas++;
        } else {
            printf("Jogada inv�lida. Tente novamente.\n");
        }

        // Verificar se h� um vencedor
        if (verificarVencedor(tabuleiro)) {
            exibirTabuleiro(tabuleiro);
            printf("\nParab�ns, Jogador %d! Voc� venceu!\n", jogador);
            break;
        }

        // Verificar se � um empate
        if (totalJogadas == 9) {
            exibirTabuleiro(tabuleiro);
            printf("\nO jogo terminou em empate!\n");
            break;
        }

        jogador++;
    } while (1);

