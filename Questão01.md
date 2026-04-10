# Questão 1

Digamos que nosso alfabeto contém apenas as letras a, b e c. Qualquer string desse
conjunto tem a forma WcM, onde W é uma sequência das letras ab, e M é o inverso de
W. Por exemplo: ababcbaba. Escreva um programa que decida se uma determinada
string pertence ou não ao formato WcM. Utilize uma estrutura de pilha para resolver o
problema.

# Utilizei pilha estática para resolver este exercício
Declarando as Funções
```C
#ifndef EXEH_H
#define EXEH_H
#define TAM 10

typedef struct ITEM{
    int topo;
    char dados[TAM];
}tipopilha;

void inicializar(tipopilha *pilha);
int cheia(tipopilha *pilha);
int vazia(tipopilha *pilha);
int inserir(tipopilha *pilha, char letra);
int verificarWcM(char palavra[], int tamanho);
int lerTopo(tipopilha *pilha);

#endif    
```
A lógica e o código
```C
#include <stdio.h>
#include <stdlib.h>
#include "exeH.h"
#include <string.h>

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
int inserir(tipopilha *pilha, char letra){
    if(cheia(pilha)==1){
        return -1;
    }else{
        return pilha->dados[++pilha->topo] = letra; // ++ antes, o elevador antes sobe para depois deixar a caixa
    }
}
int remover(tipopilha *pilha){
    if(vazia(pilha)==1){
        return -1;
    }else{
        return pilha->dados[pilha->topo--];
    }
}
int lerTopo(tipopilha *pilha){
    if(vazia(pilha)==1){
        return 1;
    }else{
        return pilha->dados[pilha->topo];
    }
}
int verificarWcM(char palavra[], int tamanho){
    tipopilha pilha;
    inicializar(&pilha);
    int achouC = 0;

    for(int i = 0; i<tamanho; i++){
       char LetraA = palavra[i];

       if(LetraA == 'c'){ // se for c então já achou
            achouC = 1;
       }else if(achouC == 0){ // senao se, montar o W
        inserir(&pilha, LetraA);
       }else if(achouC == 1){ // se achar o c então vamos montar e verificar se o W está certo
            if(vazia(&pilha)==1){ // verificação caso a palavra nao termine
                return 0;
            }
            char letraTopo = remover(&pilha); // falamos que a letra do topo é a mesma que iremos remover
            
            if(LetraA != letraTopo){ // se essa letra que acabamos de remover for diferente a letra letra que estamos empilhando, então não é válido
                return 0;
            }
       }
    }
    if(vazia(&pilha)==1){ //se a pilha esvaziar todo é pq é valido, no tudo deu certo, return 1.
        return 1;
    }else{
        return 0;
    }
    
}

 
```
Main
```C
#include <stdio.h>
#include <stdlib.h>
#include "exeH.h"
#include <string.h>

void main(){
    tipopilha pilha;
    inicializar(&pilha);
    char palavra[10];

    printf("informe a palavra ex: (ababcbaba):");
    scanf("%s", palavra);

    int tamanho = strlen(palavra);

    int r=verificarWcM(palavra,tamanho);
    if(r==1){
        printf("certo");
    }else{
        printf("errado");

    }

}
```
