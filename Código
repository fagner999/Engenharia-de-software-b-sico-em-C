#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>  // Para usar a função usleep
#include <time.h>    // Para monitorar o tempo

// Funções e variáveis globais
void imprimirMundo(int linhas, int colunas, int mundo[linhas][colunas]);
int contarVizinhos(int linhas, int colunas, int mundo[linhas][colunas], int x, int y);
void proximaGeracao(int linhas, int colunas, int mundo[linhas][colunas]);
void inicializarMundo(int linhas, int colunas, int mundo[linhas][colunas]);

int main() {
    int ImputLinha, ImputColuna, ImputTempo;

    // Solicita ao usuário o número de linhas e colunas
    printf("Digite o número de linhas desejadas: ");
    scanf("%d", &ImputLinha);

    printf("Digite o número de colunas desejadas: ");
    scanf("%d", &ImputColuna);

    // Solicita ao usuário o limite de tempo
    printf("Digite o limite de tempo em segundos: ");
    scanf("%d", &ImputTempo);

    while (1) {  // Loop infinito para reiniciar o jogo

        // Declaração da matriz usando as dimensões fornecidas pelo usuário
        int mundo[ImputLinha][ImputColuna];
        for (int i = 0; i < ImputLinha; i++) {
            for (int j = 0; j < ImputColuna; j++) {
                mundo[i][j] = 0;
            }
        }

        // Inicializa o mundo
        inicializarMundo(ImputLinha, ImputColuna, mundo);

        // Captura o tempo inicial
        time_t tempoInicial = time(NULL);

        while (1) {
            // Captura o tempo atual
            time_t tempoAtual = time(NULL);

            // Verifica se o tempo limite foi atingido
            if (difftime(tempoAtual, tempoInicial) >= ImputTempo) {
                printf("Tempo limite atingido. Reiniciando o jogo...\n");
                sleep(2);  // Pausa de 2 segundos antes de reiniciar
                break;  // Sai do loop interno e reinicia o jogo
            }

            system("clear");  // Limpa a tela para uma nova geração
            imprimirMundo(ImputLinha, ImputColuna, mundo);
            proximaGeracao(ImputLinha, ImputColuna, mundo);
            usleep(200000);  // Pausa para visualizar a evolução (200 milissegundos)
        }
    }

    return 0;
}

// Função para imprimir o mundo
void imprimirMundo(int linhas, int colunas, int mundo[linhas][colunas]) {
    for (int i = 0; i < linhas; i++) {
        for (int j = 0; j < colunas; j++) {
            if (mundo[i][j] == 1)
                printf("O");  // Célula viva
            else
                printf(".");  // Célula morta
        }
        printf("\n");
    }
}

// Função para contar os vizinhos vivos de uma célula
int contarVizinhos(int linhas, int colunas, int mundo[linhas][colunas], int x, int y) {
    int vizinhosVivos = 0;

    // Verifica as 8 direções ao redor da célula
    for (int i = -1; i <= 1; i++) {
        for (int j = -1; j <= 1; j++) {
            if (i == 0 && j == 0)
                continue;  // Ignora a própria célula
            int nx = x + i;
            int ny = y + j;
            if (nx >= 0 && nx < linhas && ny >= 0 && ny < colunas) {
                vizinhosVivos += mundo[nx][ny];
            }
        }
    }
    return vizinhosVivos;
}

// Função para gerar a próxima geração
void proximaGeracao(int linhas, int colunas, int mundo[linhas][colunas]) {
    int novoMundo[linhas][colunas];

    for (int i = 0; i < linhas; i++) {
        for (int j = 0; j < colunas; j++) {
            novoMundo[i][j] = 0;  // Inicializa a nova geração
        }
    }

    for (int i = 0; i < linhas; i++) {
        for (int j = 0; j < colunas; j++) {
            int vizinhos = contarVizinhos(linhas, colunas, mundo, i, j);

            if (mundo[i][j] == 1) {
                // Aplica as regras 1 e 3
                if (vizinhos < 2 || vizinhos > 3)
                    novoMundo[i][j] = 0;  // Célula morre
                else
                    novoMundo[i][j] = 1;  // Célula sobrevive
            } else {
                // Aplica a regra 4
                if (vizinhos == 3)
                    novoMundo[i][j] = 1;  // Célula nasce
            }
        }
    }

    // Atualiza o mundo para a próxima geração
    for (int i = 0; i < linhas; i++) {
        for (int j = 0; j < colunas; j++) {
            mundo[i][j] = novoMundo[i][j];
        }
    }
}

// Função para inicializar o mundo com algumas células vivas (manual ou aleatório)
void inicializarMundo(int linhas, int colunas, int mundo[linhas][colunas]) {
    // Exemplo manual de células vivas
    if (linhas > 3 && colunas > 3) {  // Verifica se o mundo é grande o suficiente
        mundo[1][2] = 1;
        mundo[2][3] = 1;
        mundo[3][1] = 1;
        mundo[3][2] = 1;
        mundo[3][3] = 1;
    }
}
