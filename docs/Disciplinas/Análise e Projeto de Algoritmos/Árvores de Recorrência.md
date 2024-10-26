# àrvores de recorrência
Essas árvores são "geradores" ou representantes da recorrência de um algoritmo.
As mais simples posuem apenas uma "branch" e são relativamente lineares e bastante semelhantes ao pensamento costumeiro da recursão (adiciona as chamadas na pilha e vai retornando).
Uma observação interessante é que parte da montagem da *árvore* é dada pelo multiplicador da função recursiva. Pro exemplo, em T(n−1) a árvore é **linear** (segue um galho só, como se sempre estivesse na *main*); mas em 2*T(n−1) temos uma árvore **binária** (cada nodo tem 2 filhos).
Fique com o exemplo de "Hello World" das árvores de recorrência:
T (n)=| 1, n=0
      |2+T (n−1), n>0
**àrvore de recorrência**
T(n) = custo 2
T(n-1) = custo 2
T(n-2) = custo 2
T(n-3) = custo 2 -> n chamadas com custo 2 - **2n**
...
T(1) = custo 2
T(0) = custo 1 -> custo 1 quando n=0; ou seja T(n) = 2n + 1 -> **O(n)**


- representação de problema rescursivo
- no problema ele pega logaritmos
    - fatoração por logaritmo
    - log(n!) <= nlog(n)
- aqui precisa se dividir o problema em partes menores e montar uma árvore de recursão dos dados
- não necessariamente o limite está bem representado nos limites do algoritmo
    - limite justo é o theta
- com tantas chamadas de recursão se abre tantas branches na árvore
- o custo é cumulativo com a quantidade de brnaches
- sempre que houver aumento de expoente se usa logaritmo (aqui se usa log como log_2)

## Teorema mestre
Esse teorema pode resolver todos as recursões com uma fórmula **T(n) = aT(n/b) + f(n)**. Divide e conquista para resolver o problema com mais velocidade.
a >= 1 e b > 1, necessariamente.
Dessa forma, encontrar os limites assintóticos vira um trabalho de analisar uma tabela, veja:
● Se f(n) = O(n^(log(_b(a−ϵ)))) para uma constante ϵ > 0, então T(n) = Θ(n^(log_b a)).
● Se f(n) = Θ(n^(log_b a)), então T(n) = Θ(n^(log_b a lg n)). -> *Lembre-se que lg, em computação, equivale a log_2 (base 2)* 
● Se f(n) = Ω(n^(log_b(a+ϵ))) para uma constante ϵ > 0, e se af(n/b) <= cf(n) para uma constante c < 1 e todos os n suficientemente grandes, então T(n) = Θ(f(n)).

*A maioria dos resultados estão em theta, então ambos os limites estão incluídos.*
*Lembre-se de que os resultados são baseados nos limites da equação sozinha para o esquema recursivo.*

- é um formato de equação pra encontrar comportamento assintótico
- só funciona pra divisão e conquista
    - se identifica por divisões dentro das fórmulas
- se n der inteiro arredonda pra baixo ou pra cima
    - geralmente é pra cima
- essa equação mestre é só um arranjo da equação recursiva
- nesses casos se calcula theta, dessa forma, se chega em big O e ômega

### Referẽncias
- CORMEN, Thomas H. et al. Introduction to Algorithms. 3. ed. Cambridge: MIT, 2009.
- Solving Recurrences. https://web.stanford.edu/class/archive/cs/cs161/cs161.1168/lecture3.pdf
- Material de aula. Prof. Gilberto Irajá Müller (Unisinos).
- - Aula 2024/2 Análise e Projeto de Algoritmos - Árvores de Recorrência, Profa. Andriele Busatto do Carmo