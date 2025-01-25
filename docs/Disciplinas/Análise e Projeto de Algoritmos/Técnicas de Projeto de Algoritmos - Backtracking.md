# Técnicas de Projeto de Algoritmos: Backtracking
Esse tipo de algoritmo é um força bruta melhorado. Isso porque o funcionamento de ir testando as respostas funciona da exata mesma forma; todavia, o algoritmo precisa verificar toda hora se alguma das regras previamente impostas pelo problema foi quebrada, se sim, o algoritmo não continua por aquele caminho volta um nodo, e segue para o próximo (sim, também é montado em um esquema de árvore).
Esse funcionamento é bastante parecido com um algoritmo básico de atravessar um labirinto.

- força bruta melhorado
- pega todas as soluções e vai tirando
- pega um ramo e desce até n funcionar mais - beco sem saída
    - volta até o nó que permite chegar em uma solução possível
- um exemplo é um labirinto
    - precisa definí-lo como um grid pro exemplo
- precisa guardar os nós já visitados

## N-Queens
- Pesquise: **N-queens Problem**
- N rainhas no tabuleiro sem nenhum ser ameaçada
- cada rainha em uma linha e cada uma em uma coluna diferente
- uma das abordagens é entregar uma terceira diretriz pra elas não ficarem na diagonal (bounding function)
    - qualquer solução que jogar uma rainha na diagonal da outra nem começa a ver o ramo

### Referências
- Material do professor Abdul Bari. Disponível em:
    [Algoritmos e Programação](https://www.youtube.com/channel/UCZCFT11CWBi3MHNlGf019nw)
- material da professora Andriele Busatto (Unisinos)
- The Algorithm Design Manual (Skiena) 
    - Capítulo 7 - Combinatorial Search and Heuristic Methods
