# Questão 02
Escreva um programa que receba do usuário o nome e a idade de uma pessoa e
armazene essas informações numa estrutura de pilha (estática ou dinâmica). Utilizando
somente operações de empilhar e desempilhar, o seu programa deve remover um item
por meio do nome fornecido pelo usuário. Ao final da execução da função, a pilha deve
ser igual a original, exceto pela ausência do item removido.

main
```C
#include <stdio.h>
#include <string.h>
#include "exeH.h"

void main(){
    char nome[100];
    int idade;
    int op = -1;
    tipopilha pilha = NULL;

     while (op!=0)
    {
        exibir(pilha);
        printf("\nDIGITE 0 e escolhera a pessoa que deseja retirar\n");
        printf("1: Inserir\n");
        scanf("%d",&op);
        switch(op)
        {
        case 1:
            printf("Informe o nome:\n");
            scanf("%s", nome);

            printf("informe a idade:\n");
            scanf("%d", &idade);
            getchar();
        
            pilha = inserir(pilha, nome, idade);
            break;
            default:
            break;
        }
    }
    char buscarnome[100];
    printf("informe o nome da pessoa que deseja remover:\n");
    scanf("%s", buscarnome);

    tipopilha pilhaAux = NULL;
    int achou = 0;

    while(pilha!=NULL){
        if(strcmp(pilha->item, buscarnome)==0){
            pilha = remover(pilha);
            achou = 1;
            break;
        }else{
            pilhaAux = inserir(pilhaAux, pilha->item, pilha->idade); //copia os dados do proximo para a pilhaux
            pilha = remover(pilha);//remove o proximo já que está na pilha aux
        }
    }
    while(pilhaAux!=NULL){
        pilha = inserir(pilha, pilhaAux->item, pilhaAux->idade);

        pilhaAux = remover(pilhaAux);
    }

    printf("\nPILHA FINAL\n");
    exibir(pilha);
}
```
Desenvolvendo as funções .c
```C
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include "exeH.h"

tipopilha criarNome(char nome[], int idade){
    tipopilha novoNome = (tipopilha) malloc(sizeof(struct NOME));

    if(novoNome == NULL){
        printf("\nErro na aloação\n");
    }
    else{
        strcpy(novoNome->item, nome);//copiar o texto, strcpy(destino,origem), usado com string
        novoNome->idade = idade;
        novoNome->proximo = NULL;
    }
    return novoNome;
}
tipopilha inserir(tipopilha pilha, char nome[], int idade){
    tipopilha novoNome = criarNome(nome, idade);
    novoNome->proximo = pilha;
    return novoNome;
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
    if(pilha==NULL){
        printf("\nPIlha Vazia\n");
    }else{
        while (pilha!=NULL)
        {
            printf("\t %s %d \n", pilha->item, pilha->idade);
            pilha = pilha->proximo;
        }
        
    }
}
```
Declarando as funções .h
```C
#ifndef EXEH_H
#define EXEH_H

typedef struct NOME{
    char item[100];
    int idade;
    struct NOME *proximo;
}*tipopilha;

tipopilha criarNome(char nome[], int idade);
tipopilha inserir(tipopilha pilha, char nome[], int idade);
tipopilha remover(tipopilha pilha);
void exibir(tipopilha pilha);

#endif
```
