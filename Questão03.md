# Questão 03
Faça um programa que verifique se uma dada cadeia de caracteres é ou não
palíndroma. Uma cadeia é palíndroma quando lida da esquerda para a direita e da
direita para a esquerda são iguais. Por exemplo: “ARARA” é palíndroma. Para resolver o
problema use uma estrutura de dados de pilha.

Declarando as funções .h
```C
#ifndef EXEH_H
#define EXEH_H

typedef struct ITEM{
    char item;
    struct ITEM *proximo;
}*tipopilha;

tipopilha criarItem(char letra);
tipopilha inserir(tipopilha pilha, char letra);
tipopilha remover(tipopilha pilha);
void exibir(tipopilha pilha);
char lerTopo(tipopilha pilha);

#endif
```
Desenvolvendo as funções .c
```C
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include "exeH.h"

tipopilha criarItem(char letra){
    tipopilha novaPalavra = (tipopilha)malloc(sizeof(struct ITEM));

    if(novaPalavra==NULL){
        printf("\nERRO\n");
    }else{
        novaPalavra->item = letra; //nova palavra abre o vagao item e coloca a letra lá
        novaPalavra->proximo = NULL;
    }
    return novaPalavra;
}
tipopilha inserir(tipopilha pilha, char letra){
    tipopilha novaPalavra = criarItem(letra);
    novaPalavra ->proximo = pilha;
    return novaPalavra;
}
tipopilha remover(tipopilha pilha){
    if(pilha==NULL){
        printf("\nErro\n");
    }else{
        tipopilha pilhaAux = pilha->proximo;
        free(pilha);
        pilha = NULL;
        return pilhaAux;
    }
}
void exibir(tipopilha pilha){
    printf("\nPILHA ATUAL\n");
    if(pilha==NULL){
        printf("\nPILHA VAZIA\n");
    }else{
        while(pilha!=NULL){
            printf("\t %c \n", pilha->item);
            pilha = pilha->proximo;
        }   
    }
}

char lerTopo(tipopilha pilha){
    if(pilha==NULL){
        return '\0';
    }else{
        return pilha->item;
    }
}
```
Main.c
```C
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include "exeH.h"

void main(){
    char palavra[50];
    tipopilha pilha = NULL;

    printf("Informe a palavra e veremos se eh palindromo\n");
    scanf("%s", palavra);

    int tamanho = strlen(palavra); //vê o tamanho do vetor
   
    for(int i=0;i<tamanho;i++){
        char letraAtual = palavra[i];
        pilha = inserir(pilha, letraAtual);//aqui colocar apenas a letra atual que está passando no for
    }
    exibir(pilha);
    for(int i=0; i<tamanho; i++){
        char letraIda = palavra[i];
        char letraVolta = lerTopo(pilha);

        if(letraIda != letraVolta){
            printf("\n '%s' nao é paladrimo", palavra);
            return;
        }else{
            pilha = remover(pilha);
        }
    }
    printf("A palavra '%s', eh palindromo\n", palavra);
}
```


