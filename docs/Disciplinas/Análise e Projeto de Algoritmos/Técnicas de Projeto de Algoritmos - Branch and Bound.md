# Técnicas de Projeto de Algoritmos: Branch and Bound
Essa estratégia consistem em abrir uma árvore de possibilidades (literalmente todas) e ir podando ramos (**branches**) a fim de evitar recálculo ou ainda para manter caminhos mais eficazes.
As podas podem seguir uma série de diferentes regras, como impossibilidade de executar uma relação (caso seja em um grafo), outro caminho mais curto já existe (aqui entenda curto como o de *menor resistência* ou o que tem uma soma de pesos menor) e etc.
O conjunto *S* de soluções candidatas para a execução do algoritmo é chamado **espaço de busca** (uma árvore sem as podas).
Sempre entenda a enumeração antes e defina boas escolhas iniciais, elas ditarão quanto tempo o algoritmo precisará procurar e entrar em branches para achar soluções mais eficazes.

Observe a implementação genérica de BB (Branch and Bound)
```Java
1.  encontre uma solução inicial C_h para o problema de otimização
2.  B <- F(X_h)     // B conterá as melhores soluções obtidas
3.  while S não estiver vazia do
4.      retire m nó N da fila S de soluções parciais
5.      if N representa uma solução candidata única x e f(x) < B then
6.          B <- f(x)   // x é a melhor solução até o momento, registre isso
7.      else
8.          ramifique (branch) N para produzir novos nós N_i
9.          for cada novo nó N_i do
10.             if f(N_i) > B then
11.                 // não faça nada: o nó não leva a solução ótima
12.             else
13.                 armazene N_i na fila de soluções parciais S
```
Lembre-se: o custo aceitável sempre depende do problema


- possíveis soluções -> branch
- poda de enumerações -> bound
- percorre árvore de enumeração (state-space tree)
- poda por não ser caminho promissor quando é maior do que o que já foi avaliado
    - se existe outro caminho com custo menor aquele igual com custo maior é podado
    - podem existir mais soluções dependendo do jeito que o problema é dado
- força bruta mais sofisticado
    - se um caminho entra em algo esquisito ele cai fora
- no geral usado pra menor custo - minimização
- Pesquise: **Problema do Caixeiro viajante com Branch and Bound**


### Referências
- Material do professor João Gluz (Unisinos)
- Material do professor Abdul Bari. Disponível em:
    [Algoritmos e Programação](https://www.youtube.com/channel/UCZCFT11CWBi3MHNlGf019nw)
- material da professora Andriele Busatto (Unisinos)
