# Questão 1

Digamos que nosso alfabeto contém apenas as letras a, b e c. Qualquer string desse
conjunto tem a forma WcM, onde W é uma sequência das letras ab, e M é o inverso de
W. Por exemplo: ababcbaba. Escreva um programa que decida se uma determinada
string pertence ou não ao formato WcM. Utilize uma estrutura de pilha para resolver o
problema.

Declarando as Funções
```C
#ifndef EXEH_H
#define EXEH_H

typedef struct LETRA{
    char item;
    struct LETRA *proximo;
}*tipopilha;

tipopilha criaritem(char letra);
tipopilha inserir(tipopilha pilha, char letra);
char lerTopo(tipopilha pilha);
tipopilha remover(tipopilha pilha);
void exibir(tipopilha pilha);
#endif
```
A lógica e o código
```C
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include "exeH.h"

tipopilha criaritem(char letra){
    tipopilha novaLetra = (tipopilha) malloc(sizeof(struct LETRA));

    if(novaLetra == NULL){
        printf("\nErro na aloação de memória\n");
    }else{
        novaLetra->item = letra;
        novaLetra->proximo = NULL;
    }
    return novaLetra;
}

tipopilha inserir(tipopilha pilha, char letra){
    tipopilha novaLetra = criaritem(letra);
    novaLetra->proximo = pilha;
    return novaLetra;
}
char lerTopo(tipopilha pilha){
    if(pilha == NULL){
        return '\0';
    }else{
        return pilha->item;
    }
}

tipopilha remover(tipopilha pilha){
    if(pilha == NULL){
        printf("\nPilha vazia\n");
    }else{
        tipopilha pilhaAux = pilha->proximo;
        free(pilha);
        pilha = NULL;
        return pilhaAux;
    }
}
void exibir(tipopilha pilha){
    printf("--PILHA ATUAL--");
    if(pilha == NULL){
        printf("\nPilha Vazia\n");
    }else{
        while(pilha!=NULL){
            printf("\t %c \n", pilha->item);
            pilha = pilha->proximo;
        }
    }
}
```
Main
```C
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include "exeH.h"

void main(){
    char palavra[100];
    tipopilha pilha = NULL;

    int acharC = 0;

    printf("informe a palavra, EX:(abcbaba), e veremos se é do formato WcM\n");
    scanf("%s", palavra);

    int tamanho = strlen(palavra);//aqui ve quantas letras tem na palavra

    for(int i=0; i<tamanho;i++){
        char letraA = palavra[i];

        if(letraA == 'c'){
            acharC = 1;
        }
        else if(acharC == 0){
            pilha = inserir(pilha, letraA);
        }
        else if(acharC == 1){
            char letraDoTopo = lerTopo(pilha);

            if(letraA != letraDoTopo){
                printf("formato inválido\n");
                return;
            }
            pilha = remover(pilha);
        } 
    }
    if(pilha == NULL){
        printf("Formato WcM, válido\n");
    }else{
        printf("Formato WcM inválido\n");
    }

}
```
