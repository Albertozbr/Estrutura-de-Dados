# Questão 06
A Torre de Hanói é um famoso quebra-cabeça matemático que consiste em três
hastes e um número de discos de tamanhos diferentes que podem ser encaixados uma
vez em cada haste. O objetivo é mover a pilha inteira de discos de uma haste para
outra, respeitando as seguintes regras:

● Só é permitido mover um disco de cada vez.
● Um disco maior nunca pode ser colocado sobre um disco menor.

Escreva um programa em C que resolva o problema da Torre de Hanói usando pilhas.
Seu programa deve incluir as seguintes funcionalidades:

● Definição de uma estrutura de dados do tipo pilha.

● Implementação das operações de empilhar (push) e desempilhar (pop) para a
pilha.

● Função para resolver a Torre de Hanói para um número específico de discos (no
mínimo 3 discos)..

● O programa deve imprimir cada movimento realizado, indicando a origem e o
destino do disco movido.

# Neste exercício usei Pilha estática. OBS: auxilio de IA para montar a função hanoi.
Exercício bom para relembra recursividade

Declarando as funções .h
```C
#ifndef EXEH_H
#define EXEH_H
#define TAM 10

typedef struct{
    int topo; 
    int dados[TAM];
}tipopilha;

void inicializar(tipopilha *pilha);
int cheia(tipopilha *pilha);
int vazia(tipopilha *pilha);
int inserir(tipopilha *pilha, int valor);
int remover(tipopilha *pilha);
void exibir(tipopilha *pilha);
void exibirTopo(tipopilha *pilha);
void hanoi(int n, tipopilha *ori, tipopilha *dest, tipopilha *aux, char nomeO, char nomeD, char nomeAux);


#endif
```
Desenvolvendo as funções .c
```C
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include "exeH.h"

void inicializar(tipopilha *pilha){
    pilha->topo = -1;
}
int cheia(tipopilha *pilha){
    if(pilha->topo == TAM -1){
        return 1;
    }else{
        return 0;
    }
}
int vazia(tipopilha *pilha){
    if(pilha->topo == -1){
        return 1;
    }else{
        return 0;
    }
}
int inserir(tipopilha *pilha, int valor){
    if(cheia(pilha) == 1){
        return -1;
    }else{
       return pilha->dados[++pilha->topo] = valor;
    }
}
int remover(tipopilha *pilha){
    if(vazia(pilha) == 1){
        return -1;
    }else{
        return pilha->dados[pilha->topo--];
    }
}
void exibir(tipopilha *pilha){
    int posicao = pilha->topo;

    if(vazia(pilha) == 1){
        printf("\nPILHA VAZIA\n");
    }else{
        while(posicao!=-1){
            printf("\t %d\n", pilha->dados[posicao--]);
        }
    }
}
void exibirtopo(tipopilha *pilha){
    if(vazia(pilha) == 1){
        printf("\nPILHA VAZIA\n");
    }else{
        printf("\n O topo eh: %d", pilha->dados[pilha->topo]);
    }
}
void hanoi(int n, tipopilha *ori, tipopilha *dest, tipopilha *aux, char nomeO, char nomeD, char nomeAux){
    //aqui irei usar recursividade

    if(n == 1){ // se tiver apenas um disco, então só movemos
        int disco = remover(ori);
        inserir(dest, disco);
        printf("Mover disco %d da haste %c para a haste %c\n", disco, nomeO, nomeD);
        return;// a recursivade terá que chegar nesse if toda vez para ser rodada
    }
    // mover n-1, no caso 2, da origem para auxiliar
    hanoi(n-1, ori, aux, dest, nomeO, nomeAux, nomeD);

    int disco = remover(ori);
    inserir(dest, disco);
    printf("Mover disco %d da haste %c para a haste %c\n", disco, nomeO, nomeD);

   hanoi(n-1, aux, dest, ori, nomeAux, nomeD, nomeO);
}

```

Main.c
```C
#include <stdio.h>
#include "exeH.h"

void main(){
    int valor = 0;
    tipopilha pA, pB, pC;

    pA.topo = -1;
    pB.topo = -1;
    pC.topo = -1;
    
    printf("Informe a quantidade de discos:\n");
    scanf("%d", &valor);

    if(valor<3){
        printf("Valor invalido, necessário ser > 3\n");
        return;
    }

    for(int i = valor; i >=1; i--){//For empilhara sempre do maior para o menor, ficando sempre o menor no topo
        inserir(&pA, i);
    }
        printf("Numero de discos %d\n", valor);

        hanoi(valor, &pA, &pB, &pC, 'A', 'B', 'C');
        
}
```
