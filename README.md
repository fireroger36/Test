# Relatório
## Experimento
Existem 3 tipos de dicionário:

    Estáticos: Não precisam de alterações, portanto são criados apenas uma vez. O foco é a busca, visto que os elementos devem estar ordenados. São implementados com vetores.
    Semi-dinâmicos: Podem precisar de poucas alterações, então são criados com alguns pontos que podem ser mudados. Inserção e busca possuem um bom custo, porém a remoção é problemática. São implementados usando hashing com endereçamento direto.
    Dinâmicos: Podem precisar de várias alterações, então possuem capacidade completa de alterações. Todas as operações (inserção, busca, remoção) possuem custos ótimos. Podem ser implementados com árvores ou hashing com endereçamento aberto.

Para resolver o problema do indice remissivo, foram criados um dicionário estático para armazenamento da sequência de stopwords e um dicionário dinâmico implementado com hashing com endereçamento aberto (tabela hash).

Abaixo segue a função Hash utilizada:
```
unsigned funcaoHash(char chave[], unsigned tamanhoVetor){ //função hash com chave do tipo string
    unsigned cont = 0;
    unsigned pos = 0;
    unsigned primo = 127;

    for(cont; chave[cont] != '\0'; cont++){
        pos = (pos * primo + chave[cont]) % tamanhoVetor;
    }
    return pos;
}
```
Todas as palavras do livro, exceto as stopwords, foram inseridas na tabela hash. As páginas em que cada palavra aparece aparece por ordem de importância, com base no TF-IDF.

##Resultados
Para cada consulta no índice, é chamada a função de buscar no índice. A função de busca calcula a função hash para aquela palavra e, em seguida, chama a função de busca no dicionário dinâmico.


Função de busca no índice:
```
tipoDado *buscarNaTabelaHash(tipoTabelaHash *tabelaHash, char *chave){
    unsigned pos = funcaoHash(chave, tabelaHash->tamanhoTabHash);

    return buscarPorChaveNaLista(&(tabelaHash->tabHash[pos]), chave);
}
```

Função de busca no dicionário dinâmico:
```
tipoDado *buscarPorChaveNaLista(tipoLista *lista, char *chave){
    tipoNo *aux;
    aux = lista->prim;
    while((aux!=NULL) && (strcmp(aux->dado.palavra, chave) != 0)){
        aux = aux->prox;
    }
    if(aux){
        return &aux->dado;
    }
    return NULL;
}
```
