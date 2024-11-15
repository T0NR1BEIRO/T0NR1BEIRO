#include <stdio.h>
#include <string.h>

#define TAMANHO_LISTA 100
#define TAMANHO_STRING 50

char lista_compras[TAMANHO_LISTA][TAMANHO_STRING];
int tamanho_lista = 0;

// Função para adicionar item
void adicionar_item(char *item) {
    if (tamanho_lista < TAMANHO_LISTA) {
        strcpy(lista_compras[tamanho_lista], item);
        tamanho_lista++;
        printf("Item adicionado com sucesso!\n");
    } else {
        printf("Erro: Lista cheia!\n");
    }
}

// Função para remover item
void remover_item(char *item) {
    int encontrado = 0;
    for (int i = 0; i < tamanho_lista; i++) {
        if (strcmp(lista_compras[i], item) == 0) {
            encontrado = 1;
            for (int j = i; j < tamanho_lista - 1; j++) {
                strcpy(lista_compras[j], lista_compras[j + 1]);
            }
            tamanho_lista--;
            printf("Item removido com sucesso!\n");
            break;
        }
    }
    if (!encontrado) {
        printf("Item não encontrado na lista.\n");
    }
}

// Função para exibir lista
void exibir_lista() {
    if (tamanho_lista == 0) {
        printf("A lista está vazia.\n");
    } else {
        printf("Lista de compras:\n");
        for (int i = 0; i < tamanho_lista; i++) {
            printf("- %s\n", lista_compras[i]);
        }
    }
}

// Função para ordenar lista
void ordenar_lista() {
    char temp[TAMANHO_STRING];
    for (int i = 0; i < tamanho_lista - 1; i++) {
        for (int j = i + 1; j < tamanho_lista; j++) {
            if (strcmp(lista_compras[i], lista_compras[j]) > 0) {
                strcpy(temp, lista_compras[i]);
                strcpy(lista_compras[i], lista_compras[j]);
                strcpy(lista_compras[j], temp);
            }
        }
    }
    printf("Lista de compras ordenada em ordem alfabética.\n");
}

// Função para contar itens
void contar_itens() {
    printf("Total de itens na lista: %d\n", tamanho_lista);
}

// Função principal
int main() {
    int opcao;
    char item[TAMANHO_STRING];

    do {
        printf("\nMENU - Lista de Compras\n");
        printf("1. Adicionar item\n");
        printf("2. Remover item\n");
        printf("3. Exibir lista\n");
        printf("4. Ordenar lista\n");
        printf("5. Contar itens\n");
        printf("0. Sair\n");
        printf("Escolha uma opção: ");
        scanf("%d", &opcao);
        getchar(); // Limpar o buffer do teclado

        switch (opcao) {
            case 1:
                printf("Digite o nome do item para adicionar: ");
                fgets(item, TAMANHO_STRING, stdin);
                item[strcspn(item, "\n")] = '\0'; // Remover o caractere de nova linha
                adicionar_item(item);
                break;
            case 2:
                printf("Digite o nome do item para remover: ");
                fgets(item, TAMANHO_STRING, stdin);
                item[strcspn(item, "\n")] = '\0'; // Remover o caractere de nova linha
                remover_item(item);
                break;
            case 3:
                exibir_lista();
                break;
            case 4:
                ordenar_lista();
                break;
            case 5:
                contar_itens();
                break;
            case 0:
                printf("Saindo do programa...\n");
                break;
            default:
                printf("Opção inválida. Tente novamente.\n");
        }
    } while (opcao != 0);

    return 0;
}
