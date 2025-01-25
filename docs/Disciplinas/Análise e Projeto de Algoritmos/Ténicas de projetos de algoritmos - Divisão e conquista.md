# Técnicas de projetos de algoritmos: Divisão e conquista
É uma técnica bastante simples de entender e bastante utilizada por diversos algoritmos, normalmente recursivos (tais como o mergesort); ela consiste em:
● Pegar um problema de entrada grande
● Quebrar a entrada em pedaços menores → divisão - *quebrar em subproblemas menores*
● Resolver cada pedaço separadamente → conquista - *resolver os problemas recursivamente*
● Combinar os resultados → combinação - *combinar as soluções todas e compor um resultado*

Provavelmente o maior exemplo de um algoritmo de divisão e conquista amplamente utilizado é o *mergesort*.
Confira abaixo um algoritmo recursivo de *mergesort*
MergeSort(int V[], int i, int f)
1. if i < f then
2.      m ← (i + f) / 2;
3.      Mergesort(V, i, m);
4.      Mergesort(V, i+1, f);
5.      Merge(V, i, m, f);
No qual MergeSort(vetor, 1, tamanho) e:
V[] -> vetor fonte
i -> índice inicial
m -> índice médio
f -> indice final

A grande moral dele é que usará um tempo constante quando n=1 (já que existe uma posição, a qual já é ordenada por padrão).
Utiliza duas chamadas recursivas nas linhas 3 e 4, ou seja, chama T(n) duas vezes; além disso, soma um tempo constante para a linha 2 a cada chamada e mais a chamada da linha 5 para o retorno.
Dessa forma, as equações recursivas ficam:
F(n) = | O(1),n=1           ou ainda F(n) = | 1,n=1
       |2T(n/2)+O(n),n>1                    |2T(n/2)+d,n>1
E, uma vez que a expanção da árvore se quebra em dois a cada recursão, tempo um log_2 (n) como sua altura; +1 para a recursão final.


- quebra o problema em partes menores para resolver - divisão
- ao resolver se conquista - conquista
- junta tudo no final - combinação
- dá pra repetir as mesmas iterações não importando o tamanho da instância
- decisão de divisão e tomada de ações precisa ser padrão para toda instãncia
- usa recursividade
- geralmente é com recursividade, mas depende
    - quando é necessário descer muitos níveis de recursão se evita utiliza pra n dar stackoverflow

### Referências
- CORMEN, Thomas H. et al. Introduction to Algorithms. 3. ed. Cambridge: MIT, 2009.
- SMaterial de aula. Prof. Jorge Abrantes de Figueiredo (UFCG).
- Material de aula. Prof. Sandro Rigo (Unisinos).
- Aula 2024/2 Análise e Projeto de Algoritmos - Árvores de Recorrência, Profa. Andriele Busatto do Carmo
