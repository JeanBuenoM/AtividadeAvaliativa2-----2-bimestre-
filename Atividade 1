#include <stdio.h>
#include <stdlib.h>

typedef struct NoInt {
    int valor;
    struct NoInt *prox;
} NoInt;

typedef struct No {
    char musica[100];
    struct No *prox;
    struct No *ant;
} No;

void copiarString(char *dest, const char *src, int max) {
    int i = 0;
    while (i < max - 1 && src[i] != '\0') {
        dest[i] = src[i];
        i++;
    }
    dest[i] = '\0';
}

void inserirPosicao(NoInt **head, int valor, int posicao) {
    if (posicao < 0) {
        printf("Posição invalida.\n");
        return;
    }

    NoInt *novo = (NoInt *)malloc(sizeof(NoInt));
    if (!novo) {
        printf("Erro de alocação de memória.\n");
        return;
    }
    novo->valor = valor;
    novo->prox = NULL;

    if (posicao == 0) {
        novo->prox = *head;
        *head = novo;
        return;
    }

    NoInt *atual = *head;
    int i = 0;
    while (atual != NULL && i < posicao - 1) {
        atual = atual->prox;
        i++;
    }

    if (atual == NULL) {
        printf("Posição inválida.\n");
        free(novo);
        return;
    }

    novo->prox = atual->prox;
    atual->prox = novo;
}

int buscarValor(NoInt *head, int valor) {
    int posicao = 0;
    NoInt *atual = head;
    while (atual != NULL) {
        if (atual->valor == valor)
            return posicao;
        atual = atual->prox;
        posicao++;
    }
    return -1;
}

void inverterLista(NoInt **head) {
    NoInt *anterior = NULL;
    NoInt *atual = *head;
    NoInt *proximo = NULL;

    while (atual != NULL) {
        proximo = atual->prox;
        atual->prox = anterior;
        anterior = atual;
        atual = proximo;
    }

    *head = anterior;
}

void dividirLista(NoInt *head, NoInt **lista1, NoInt **lista2) {
    if (head == NULL) {
        *lista1 = NULL;
        *lista2 = NULL;
        return;
    }

    NoInt *rapido = head;
    NoInt *lento = head;

    while (rapido->prox != NULL && rapido->prox->prox != NULL) {
        rapido = rapido->prox->prox;
        lento = lento->prox;
    }

    *lista1 = head;
    *lista2 = lento->prox;
    lento->prox = NULL;
}

void exibirLista(NoInt *head) {
    if (head == NULL) {
        printf("Lista vazia.\n");
        return;
    }
    NoInt *atual = head;
    while (atual != NULL) {
        printf("%d", atual->valor);
        if (atual->prox != NULL)
            printf(" -> ");
        atual = atual->prox;
    }
    printf(" -> NULL\n");
}

void liberarLista(NoInt **head) {
    NoInt *atual = *head;
    while (atual != NULL) {
        NoInt *temp = atual;
        atual = atual->prox;
        free(temp);
    }
    *head = NULL;
}

void adicionarMusica(No **head, char *nome) {
    No *novo = (No *)malloc(sizeof(No));
    if (!novo) {
        printf("Erro de alocação de memória.\n");
        return;
    }
    copiarString(novo->musica, nome, 100);

    if (*head == NULL) {
        novo->prox = novo;
        novo->ant = novo;
        *head = novo;
        return;
    }

    No *ultimo = (*head)->ant;
    ultimo->prox = novo;
    novo->ant = ultimo;
    novo->prox = *head;
    (*head)->ant = novo;
}

void proximaMusica(No **atual) {
    if (*atual == NULL) {
        printf("Playlist vazia.\n");
        return;
    }
    *atual = (*atual)->prox;
    printf(">> Tocando agora: %s\n", (*atual)->musica);
}

void musicaAnterior(No **atual) {
    if (*atual == NULL) {
        printf("Playlist vazia.\n");
        return;
    }
    *atual = (*atual)->ant;
    printf(">> Tocando agora: %s\n", (*atual)->musica);
}

void exibirPlaylist(No *head) {
    if (head == NULL) {
        printf("Playlist vazia.\n");
        return;
    }
    No *atual = head;
    printf("\nPlaylist: ");
    do {
        printf("[%s]", atual->musica);
        if (atual->prox != head)
            printf(" <-> ");
        atual = atual->prox;
    } while (atual != head);
    printf(" <->\n");
    printf("            ^");
    No *p = head;
    int n = 0;
    do { n++; p = p->prox; } while (p != head);
    int i;
    for (i = 0; i < n * 6; i++) printf("_");
    printf("|\n\n");
}

int totalMusicas(No *head) {
    if (head == NULL)
        return 0;
    int count = 1;
    No *atual = head->prox;
    while (atual != head) {
        count++;
        atual = atual->prox;
    }
    return count;
}

void liberarPlaylist(No **head) {
    if (*head == NULL)
        return;
    No *atual = (*head)->prox;
    while (atual != *head) {
        No *temp = atual;
        atual = atual->prox;
        free(temp);
    }
    free(*head);
    *head = NULL;
}

void menuListaInt(void) {
    NoInt *lista = NULL;
    NoInt *lista1 = NULL;
    NoInt *lista2 = NULL;
    int opcao, valor, posicao, resultado;

    do {
        printf("GERENCIADOR DE LISTA DE INTEIROS\n");
        printf("1.Inserir em posição\n");
        printf("2.Buscar valor\n");
        printf("3.Inverter lista\n");
        printf("4.Dividir lista em duas\n");
        printf("5.Exibir lista\n");
        printf("0.Voltar ao menu principal\n");
        printf("Opcão: ");
        scanf("%d", &opcao);

        switch (opcao) {
            case 1:
                printf("Valor a inserir: ");
                scanf("%d", &valor);
                printf("Posição (inicia em 0): ");
                scanf("%d", &posicao);
                inserirPosicao(&lista, valor, posicao);
                printf("Lista atual: ");
                exibirLista(lista);
                break;

            case 2:
                printf("Valor a buscar: ");
                scanf("%d", &valor);
                resultado = buscarValor(lista, valor);
                if (resultado == -1)
                    printf("Valor %d não encontrado.\n", valor);
                else
                    printf("Valor %d encontrado na posição %d.\n", valor, resultado);
                break;

            case 3:
                if (lista == NULL) {
                    printf("Lista vazia.\n");
                    break;
                }
                inverterLista(&lista);
                printf("Lista invertida: ");
                exibirLista(lista);
                break;

            case 4:
                if (lista == NULL) {
                    printf("Lista vazia, nada a dividir.\n");
                    break;
                }
                dividirLista(lista, &lista1, &lista2);
                printf("Lista 1: ");
                exibirLista(lista1);
                printf("Lista 2: ");
                exibirLista(lista2);
                lista = lista1;
                liberarLista(&lista2);
                printf("(Lista principal passou a ser a Lista 1)\n");
                break;

            case 5:
                printf("Lista atual: ");
                exibirLista(lista);
                break;

            case 0:
                printf("Voltando ao menu principal...\n");
                break;

            default:
                printf("Opção inválida. Tente novamente.\n");
        }
    } while (opcao != 0);

    liberarLista(&lista);
}

void menuPlaylist(void) {
    No *head = NULL;
    No *atual = NULL;
    int opcao;
    char nome[100];

    do {
        printf("PLAYLIST CIRCULAR DUPLAMENTE ENC.\n");
        if (atual != NULL)
            printf("| >> Atual: %-27s |\n", atual->musica);
        else
            printf("Nenhuma música selecionada\n");
        printf("1.Adicionar musica\n");
        printf("2.Próxima música\n");
        printf("3.Música anterior\n");
        printf("4.Exibir playlist\n");
        printf("5.Total de músicas\n");
        printf("0.Voltar ao menu principal\n");
        printf("Opção: ");
        scanf("%d", &opcao);

        switch (opcao) {
            case 1:
                printf("Nome da música: ");
                scanf(" %[^\n]", nome);
                adicionarMusica(&head, nome);
                if (atual == NULL)
                    atual = head;
                printf("Música \"%s\" adicionada.\n", nome);
                break;

            case 2:
                if (head == NULL) {
                    printf("Playlist vazia.\n");
                } else {
                    if (atual == NULL)
                        atual = head;
                    proximaMusica(&atual);
                }
                break;

            case 3:
                if (head == NULL) {
                    printf("Playlist vazia.\n");
                } else {
                    if (atual == NULL)
                        atual = head;
                    musicaAnterior(&atual);
                }
                break;

            case 4:
                exibirPlaylist(head);
                break;

            case 5:
                printf("Total de músicas na playlist: %d\n", totalMusicas(head));
                break;

            case 0:
                printf("Voltando ao menu principal...\n");
                break;

            default:
                printf("Opção inválida. Tente novamente.\n");
        }
    } while (opcao != 0);

    liberarPlaylist(&head);
}

int main(void) {
    int opcao;

    do {
        printf("MENU PRINCIPAL\n");
        printf("1.Gerenciador de Lista de Inteiros\n");
        printf("2.Playlist de Musicas\n");
        printf("0.Sair\n");
        printf("Opção: ");
        scanf("%d", &opcao);

        switch (opcao) {
            case 1:
                menuListaInt();
                break;
            case 2:
                menuPlaylist();
                break;
            case 0:
                printf("Encerrando programa.\n");
                break;
            default:
                printf("Opção inválida. Tente novamente.\n");
        }
    } while (opcao != 0);

    return 0;
}
