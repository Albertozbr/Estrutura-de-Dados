# Questão 05 
Crie a função intercalaPilha(pilha p1, pilha p2) que deve testar se duas pilhas
estáticas possuem o mesmo tamanho e em caso afirmativo intercalar os elementos da
pilha 1 com a pilha 2 e armazenar em uma pilha 3 (também estática).

# Neste exercício eu usei pilha estática
Referente ao tamano 10, e cada pilha apenas ter 4 valores. O tamanho 10 serve para que quando formos montar a pilha 3 não ter o risco de dar erro por conta de pilha cheia, 
então já declaramos um tamanho maior para que somado a p1 intercalada a p2, dê o tamanho

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
tipopilha intercalar(tipopilha p1, tipopilha p2);

#endif
```
Desenvolvendo as funções .C
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
int inserir(tipopilha *pilha, int valor){
    if(cheia(pilha)==1){
        return -1;
    }else{
       return pilha->dados[++pilha->topo] = valor;
    }
}
int remover(tipopilha *pilha){
    if(vazia(pilha)==1){
       return -1;
    }else{
        return pilha->dados[pilha->topo--];
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
tipopilha intercalar(tipopilha p1, tipopilha p2){
    tipopilha p3;
    p3.topo = -1;

    if(p1.topo != p2.topo){
        printf("\nERRO\n");
        return p3;
    }
    while(p1.topo != -1){

        int valor1 = remover(&p1);
        inserir(&p3, valor1);

        int valor2 = remover(&p2);
        inserir(&p3, valor2);
    }
    printf("\nPILHA 3\n");
    return p3;
}
```

Main.c 
```C
#include <stdio.h>
#include "exeH.h"

void main(){
    int valor=0;
    tipopilha p1;
    tipopilha p2;
    tipopilha p3;

    p1.topo = -1;
    p2.topo = -1;
    int op = -1;

    while(op!=0){
        printf("\nDIGITE 0 PARA VER A P3\n");
        printf("1-inserir pilha 1\n");
        printf("2-inserir pilha 2\n");
        scanf("%d", &op);

        switch(op){
            case 1:
            
            for(int i=0;i<4;i++){
                printf("Digite o %d numero\n",i+1);
                scanf("%d", &valor);
                inserir(&p1, valor);
            }
            break;
             case 2:
             for(int i=0;i<4;i++){
                printf("Digite o %d numero\n",i+1);
                scanf("%d", &valor);
                inserir(&p2, valor);
            }
            break;

            default:
            break;
        }
    }
    p3 = intercalar(p1, p2);
    exibir(&p3);
}
```
