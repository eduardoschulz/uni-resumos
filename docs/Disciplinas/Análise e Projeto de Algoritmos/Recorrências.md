# Recorrências
Esse tipo de arranjo matemático e algoritmico é normalmente encontrado em problemas recursivos.
Nesses casos, se entende que exista um caso base e outro recursivo, por exemplo:
x^n = | 1,n=0
      |x.x^(n-1),n>0
Para esse cálculo, devemos:
– identificar qual é o “n” (tamanho do problema);
– identificar o caso base;
– identificar qual é o tempo do caso base;
– identificar o termo geral da recorrência.

No exemplo anterior, "x^(n-1)" seria a nossa equação recursiva sendo repetida "x" vezes.

- equações recorrentes
- é tipo uma recursão
- necessário um conhecimeto parcial sobre o resultado
- vai formar um sistema de equações
- sempre identifique n, o caso base, o tempo do caso base e o termo geral 
    - caso base e geral ficam juntos
- precisa validar a equação enconrada com o caso base
    - depois olha pro caso indutivo
    - joga o n lá dentro

Para a resolução de tais equações, utiliza-se o **Método da Substituição**

## Método da substituição
Dada uma relação de recorrência T(n):
– substitua n por diferentes valores, até que seja
identificado um padrão;
– escreva uma fórmula em termos de n e o número
de substituições i;
– escolha um i para ser o caso base;
– resolva a soma resultante.

Essa abordagem funciona para boa parte dos problemas, mas não todos, fique atento.
Para um caso hipotético, temos que:
T(n) = |    c,n=1
       |T(n-1)+d,n>1
Sendo que para todo n>1 T(n-1)+d; então nosso primeiro passo seria encontrar um n suficientemente grande:
T(n) = T(n - 1) + d
T(n - 1) = T(n - 2) + d
T(n - 2) = T(n - 3) + d
.
.
.
T(2) = T(1) + d
T(1) = c

À partir daí implementar quantas substituições forem necessárias na mesma fórmula até encontrarmos um padrão de alteração:
T(n) = T(n - 1) + d
     = (T(n – 2) + d) + d
     = T(n – 2) + 2d
     = (T(n – 3) + d) + 2d
     = T(n – 3) + 3d

Depois de algumas substituições (i), podemos encontrar um padrão baseado em repetições de i:
T(n) = T(n - i) + id

Agora, queremos que o T(n - i) torne-se T(1), de modo á cair no caso c,n=1 e podermos retirar o T(n - i) da jogada. Nesse caso, nosso i=n-1:
T(n) = T(1) + d(n - 1)
     = dn + c - d

### Provas
Isso feito, agora precisamos provar que a soluação está correta. Comece usando a nova fórmula para encontrar T(1):
T(1) = dn + c – d
     = d * 1 + c – d
     = d + c – d
     = c -> esse resultado precisa necessariamente ser igual ao caso base, aqui c,n=1.

Agora podemos induzir a nova fórmula para identificar seu comportamento com n+1:
T(n + 1) = dn + c – d
         = d(n + 1) + c – d
         = dn + d + c – d
         = dn + c

Depois podemos pegar nossa fórmula original (T(n-1)+d,n>1) e teambém induzí-la a n+1. Essa e a anterior precisam ter o mesmo resultado:
T(n + 1) = T(n - 1) + d
         = T(n + 1 - 1) + d
         = T(n) + d
         = dn + c - d + d
         = dn + c

### Referências
- Lecture Notes on Algorithm Analysis and Computational Complexity (Ian Parberry).
- Aula 2024/2 Análise e Projeto de Algoritmos - Recorrências, Profa. Andriele Busatto do Carmo