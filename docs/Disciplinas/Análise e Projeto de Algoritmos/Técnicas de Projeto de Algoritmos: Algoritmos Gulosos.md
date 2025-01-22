# Técnicas de Projeto de Algoritmos: Algoritmos Gulosos
Esse tipo de algorimo tem o objetivo direto de encontrar caminhos e participar de tomadas de decisão. Os problemas **maximizam** ou **minimizão** uma das variáveis do sistema. Claro que para que as decisões sejam tomadas de maneira coerente, restrições devem ser aplicadas ao sistema. 

Problemas de otimização tem diversas formas de serem abordados:
- algoritmos gulosos
- programação dinâmica
- branch and bound
- heurísticas
- algoritmos aproximativos

Uma das formas de identificar um problema como sendo cabível de aplicar um algoritmo guloso é saber se subproblemas do problema original podem ser repetidos diversas vezes para chegar à uma solução para o problema geral.
Todas as etapas fazem a melhor escolha do momento e não se considera o âmbito total na hora da decisão.
Pode ser aplicado em algoritmos de troco, seleção de atividades *Minimum Spanning Tree*, *Shortest Path*, etc.

```python
# Estrutura geral

função AlgoritmoGuloso(C: conjunto) {
    S ← inicializa como um conjunto vazio
    enquanto C não estiver vazio e não solução(S) faça
        x ← seleciona C
        C ← C - {x}
        se é viável S∪{x} então
            S ← S∪{x}
        fim se
    fim enquanto
    se solução(S) então
        retorne S
    senão
        retorne “Não existe solução!”
    fim se
fim função
```

- Existem algumas técnicas para chegar em tomadas de decisão usando limites e circunstânceas, alg. gulosos é uma delas
    - a resposta é um conjunto
- Usualmente surge de algoritmos que precisam guardar tempo ou ainda necessidade de espaço
- Estrutura geral utiliza S como resposta 
- Um algoritmo guloso puxa uma heurística e a aplica no conjunto de soluções possíveis e aplica até não conseguir mais
- Existe um ponto em que ele analisa as possibilidades e quando nenhuma é viável não tem solução
    - existir um problema depende dos limites colocados na solução
- dá pra aplicar em várias estruturas de dados, não necessariamente só grafos
- transformar o problema em uma recursão facilita na hora de enxergar o problema - todavia pode ser que seja interessante fazer o problema iterativo pra não explodir a pilha (varia de ambiente pra ambiente)
- em problemas de recursao se sai do grande até o base (quebrando o máximo possível)
- atividades não podem se sobrepor no tempo (exemplo)
    - precisamos aplicar uma heurística e um algoritmo guloso pra resolver
    - ordena as atividades que terminam antes e escolhe (alg. guloso)
    - se escolher a que termina antes sobra mais tempo pras demais

## Àrvore geradora mínima
Consiste na montagem de uma árvore, não necessariamente a menor como o nome pode sugerir, mas sim a com os caminhos mais curtos, mesmo que um número maior de arestas possa ser necessário; essa árvore gera o grafo com o mínimo de arestas com o mínimo de distância entre os vértices.
G = (V, A) → onde V representa o conjunto de vértices, e A o conjunto de arestas; sendo que cada aresta detém um peso.
O resultado final é basicamente um somatório: w(s) = ∑_(w(u,v)∈S) w(u,v)
Existem alguns métodos para abordar esse problema (sendo um deles força bruta), mas os mais famosos são **Kruskal** e **Prim**

### Kruskal
- Algoritmo guloso
```txt
MST-Kruskal(G,*w*)
1   A = null
2   for each vertex *v* ∈ *G*.*V*
3       MAKE-SET(*v*)
4   sort edges of *G.E* into nondecreasing order by weight *w*
5   for each edge (*u,v*) ∈ *G.E*, taken in nondecreasing order by weitght
6       if FIND-SET(*u*) != FIND-SET(*v*)
7           A = A ∪ {(*u,v*)}
8           UNION(*u,v*)
9   return A
```
Sendo que aqui temos a separação dos dados nas linhas 1-4, percorrendo os conjuntos em 5-8, fazendo a escolha gulosa no if (melhor decisão local) e dentro do if atualizando o conjunto de soluções para implementar a escolha.
Veja que a implementação é feita baseado em uma comparação entre duas partes do algoritmo.

- menor caminho para chegar em todos os pontos (cidades, componentes, canais, etc)
- conexão de pontos
- é o problema do caixeiro viajante - algoritmo de Dijkistra?
- representação em grafos - descobrir a cobertura (de rede)
- grafos não-dirigidos
- cada aresta tem peso (a soma dos pesos é avaliada na distância)
- todos os pontos do grafo estão conectados (tem um caminho da origem até qql nodo)
- **Kruskal** e **Primm** resolvem esse problema
    - Kruskal é uma decisão gulosa porque escolhe o de menor custo e nunca se arrepende da escolha
    - a única restrição é não criar ciclo
    - o conjunto de nós e o peso fazem parte da resposta
    - partes disjuntas de um mesmo conjunto global - **conjuntos disjuntos**
- Pesquise sobre **union find**

## Caminho mais curto em um grafo entre dois dados pontos
Ao contrário de uma escolha mínima, aqui temos um grafo dirigido (não posso andas nas duas direções na mesma aresta).
O produto mais óbivo dessa dinâmica é o algoritmo de Dijkstra.

### Algoritmo de Dijkstra
Mentém um conjunto de vértices com os menos caminhos à partir de um vértice inicial s.
À cada vértice visitado, ele calcula a distância entre o visitado e o anterior e realiza o *relaxamento* - que consiste em verificar se a nova distância leva a outro vértice de maneira mais curta que os dados anteriores mostravam.
O algoritmo em si é bastante simples:
```txt
DIJKSTRA (G, w, s)
1   Initialize-Single-Source (G,s)
2   S = ∅
3   Q = G.V
4   while Q != ∅
5       u = Extract-Min(Q)
6       S = S ∪ {u}
7       for each vertex v ∈ G.Adj[u]
8           Relax(u,v,w)
```
A inserção de dados desse algoritmo precisa ser de pelo menos 3 (dado que com apenas 2 vértices não tem muito o que se calcular).
Existem alguns cálculos diferentes (para implementações diferentes) desse algoritmo. Entre as quais:
– array ordenado pelos vértices: O(V2 + A) → O(V2)
– binary min-heap: O((V + A)lg V) → O(A lg V)
– fibonacci heap: O(V lg V + A)

- os elementos se conectam
- pocotes na rede, via de rota pra veículo, etc
- grafos dirigidos
- existem pesos associados aos vértices
- **Dijkstra** - menor caminho entre dois pontos - *single-source shortest path*
- testa os menores custos das arestas para descobrir o menor custo para ir da origem à qualquer ponto
- complexidades variam conforme estruturas usadas


### Referências
- Aula 2024/2 Análise e Projeto de Algoritmos - Técnicas de Projeto de Algoritmos: Algoritmos Gulosos, Profa. Andriele Busatto do Carmo (Unisinos)
- Introduction to Algorithms (Cormen, et al.)
    - Capítulo 16 - Greedy Algorithms
    - Capítulo 23 - Minimun Spanning Trees
        - 23.2 - The Algorithms of Kruskal and Prim
    - Capítulo 24 - Single Source Shortest Paths
        - 24.3 - Dijkstra's algorithm
- Material desenvolvido com base nos originais do professor Sandro Rigo (Unisinos).