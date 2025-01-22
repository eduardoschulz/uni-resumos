# Programação Dinâmica
O core da programação dinâmica consiste em abordagem expansiva de dados. São casos em que uma decisão local boa não reflete em uma global aceitável.
Esse tipo de programação também é utilizada quando, em problemas recursivos, temos repetição de operações e necessitamos de boa eficiência (repetição de ações - quando não necessário - não é eficiente)
Essa prog sempre guarda os dados para usar mais tarde. Uma troca simples de espaço por tempo.
A ideia é dividir esse problema em diversas partes iguais para conquistá-las mais tarte, guardando os dados já calculados em outro local e pulando essas operações já realizadas.
Para um problema cair em programação dinâmica, ele deve, pelo menos, ter uma **subestrutura ótima** (facilmente divisível) e subproblemas **concientes** (muitos iguais, logo poucos cálculos são feitos de verdade).
-> Pesquise por *Sequência de Fibonacci com programação dinâmica*

Como princípio básico de resolução de problemas com programação dinâmica, lembre-se:
1. Descrever a solução ideal do problema
2. Definir recursivamente a solução ideal, em função de soluções ideais de subproblemas
3. Determinar as soluções de todos os subproblemas utilizando a abordagem top-down
4. Determinar as soluções de todos os subproblemas utilizando a abordagem bottom-up
5. Reconstituir a solução ideal com base nos cálculos realizados

-> Pesquise por *Problema da pirâmide dos números com programação dinâmica*

- guardar resultados para o caso de ser necessário refazer algum cálculo
- redução de tempo de execução abrindo mão do espaço
- precisa de computações repetitivas
- espaço de resolução de problemas não é muito grande (muita memória)
- substrutura ótima e problemas coincidentes 
- **memoização** -> versão recursiva de uma prog. dinâmica
- **tabulação** -> basicamente uma ideia parecida sem recursão (construindo da base pra cima)
- todas as instâncias tem uma solução ótima local
- no problema da piâmide de números pode exitir a possibilidade de ter retrabalho durante o algoritmo
    - em uma primeira versão o problema é recalculado várias vezes
- caracterize uma solução ótima
    - veja se força bruta n funciona
- divida o problema e veja se uma solução é aplicável em formas recursivas -> problemas podem se repetir
- aplique um *top-down*


### Referências
- Material do professor João Gluz (Unisinos)
- Aula 2024/2 Análise e Projeto de Algoritmos - Programação Dinâmica, Profa. Andriele Busatto do Carmo (Unisinos)