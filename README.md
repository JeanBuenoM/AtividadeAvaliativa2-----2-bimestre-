Parte 1 — Inserção em Posição
A função percorre a lista até o nó anterior à posição desejada e reencadeia os ponteiros. Casos especiais (lista vazia, posição 0, posição inválida) são tratados antes da travessia. O uso de ponteiro duplo **head permite modificar o head original quando a inserção ocorre no início.
Exemplo: inserir 99 na posição 1 em 10 -> 20 -> 30 resulta em 10 -> 99 -> 20 -> 30.
Parte 2 — Busca por Valor
Percorre a lista nó a nó mantendo um contador de posição. Retorna o índice da primeira ocorrência ou -1 se o valor não existir.
Parte 3 — Inversão da Lista
Usa três ponteiros (anterior, atual, proximo) para inverter as ligações sem criar nenhum nó novo. A cada passo, atual->prox é redirecionado para o nó anterior, e os ponteiros avançam até o fim da lista.
Exemplo: 10 -> 20 -> 30 se torna 30 -> 20 -> 10.
Parte 4 — Divisão em Duas Listas
Aplica a técnica do ponteiro rápido/lento: rapido avança dois nós por iteração enquanto lento avança um. Quando rapido chega ao fim, lento está no meio exato. O corte é feito ali, sem precisar contar os elementos antes.
Em listas com tamanho ímpar, a primeira metade recebe o elemento a mais.
Exemplo: 10 -> 20 -> 30 -> 40 -> 50 é dividida em 10 -> 20 -> 30 e 40 -> 50.
Parte 5 — Playlist Circular Duplamente Encadeada
Cada nó possui ponteiros prox e ant, e a lista mantém a circularidade: o último nó aponta para o head e o head->ant aponta para o último. Ao adicionar uma música, quatro ponteiros são atualizados para preservar essa invariante.
A navegação avança ou recua o ponteiro atual, que circula indefinidamente. A exibição usa do/while com head como sentinela para saber quando uma volta completa foi concluída, evitando loop infinito.
Exemplo: [Rock] <-> [Jazz] <-> [Pop] navega como Rock → Jazz → Pop → Rock → ...
