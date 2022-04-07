# Relatório
## Experimento
Foi criado um dicionário estático para armazenamento da sequência de stopwords e um dicionário dinâmico foi implementado como tabela hash.

Função Hash:
´´´
unsigned funcaoHash(char chave[], unsigned tamanhoVetor){ //função hash com chave do tipo string
    unsigned cont = 0;
    unsigned pos = 0;
    unsigned primo = 127;

    for(cont; chave[cont] != '\0'; cont++){
        pos = (pos * primo + chave[cont]) % tamanhoVetor;
    }
    return pos;
}
´´´

