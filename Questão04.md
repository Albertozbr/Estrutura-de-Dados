# Questão 04 
Seja S uma sequência formada por 20 números inteiros. Codifique um programa que
empilhe na pilha A os números pares e na pilha B os números ímpares.
# Neste exercício usei pilha Estática

Declarando as funções .h
```C
#ifndef EXEH_H
#define EXEH_H
#define TAM 20

typedef struct{
    int topo; 
    int dados[TAM];
}tipopilha;

void inicializar(tipopilha *pilha);
int cheia(tipopilha *pilha);
int vazia(tipopilha *pilha);
void inserir(tipopilha *pilha, int valor);
void remover(tipopilha *pilha);
void exibir(tipopilha *pilha);
void exibirTopo(tipopilha *pilha);

#endif
```
Desenvolvendo a lógica .c
```C
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include "exeH.h"

void inicializar(tipopilha *pilha){
    pilha->topo = -1;
}
int cheia(tipopilha *pilha){
    if(pilha->topo==TAM-1){
        return 1;
    }else{
        return 0;
    }
}
int vazia(tipopilha *pilha){
    if(pilha->topo==-1){
        return 1;
    }else{
        return 0;
    }
}
void inserir(tipopilha *pilha, int valor){
    if(cheia(pilha)==1){
        printf("\nPilha cheia\n");
    }else{
        pilha->dados[++pilha->topo] = valor;
    }
}
void remover(tipopilha *pilha){
    if(vazia(pilha)==1){
        printf("\nPILHA VAZIA\n");
    }else{
        pilha->dados[--pilha->topo];
    }
}
void exibir(tipopilha *pilha){
    int posicao = pilha->topo;

    printf("\nPILHA ATUAL\n");
    if(vazia(pilha) == 1){
        printf("\nPILHA VAZIA\n");
    }else{
        while(posicao!= -1){
            printf("\t %d \n", pilha->dados[posicao--]);
        }
    }
}
void exibirTopo(tipopilha *pilha){
    
    if(vazia(pilha) == 1){
        printf("\nPILHA VAZIA\n");
    }else{
           printf("Topo: %d", pilha->dados[pilha->topo]);
    }
}
```
Main.c
```C
#include <stdio.h>
#include "exeH.h"

void main(){
    int valor=0;
    tipopilha pilhaA;
    tipopilha pilhaB;

    pilhaA.topo = -1;
    pilhaB.topo = -1;
    int op = -1;

    while(op!=0){
        printf("\nDIGITE 0 PARA SAIR\n");
        printf("1-inserir os números\n");
        printf("2-Ver o topo\n");
        scanf("%d", &op);

        switch(op){
            case 1:
            
            for(int i=0;i<20;i++){
                printf("Digite o %d numero\n",i+1);
                scanf("%d", &valor);
                
                if(valor % 2 == 0){
                    inserir(&pilhaA, valor);
                }else{
                    inserir(&pilhaB, valor);
                }
            }
            exibir(&pilhaA);
            exibir(&pilhaB);
            break;

            case 2:
            printf("pilha A\n");
            exibirTopo(&pilhaA);
            printf("\npilha B\n");
            exibirTopo(&pilhaB);
            break;
            default:
            break;
        }
    }

}
```

