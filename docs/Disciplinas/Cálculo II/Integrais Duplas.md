# Integrais duplas
Lembre-se que anteriormente, com apenas uma variavel, víamos a área abaixo de uma função. Nesse caso, vemos o **volume** abaixo de uma função com duas variáveis - com mais variaveis, vemos mais dimensões.
A forma mais simples, assim como anteriormente, é quebrar o problema em diversas retângulos (nesse caso, prismas ou paralelepípedos) e somar todos os volumes - V_k = ΔA_kf(X*_k,Y*_k).
Esse cálculo é posto em um somatório, que entre em um limite, limite esse que é invertido por uma integral dupla
V = ∫∫_R f(x,y)dA -> esse é a nossa integral.

- É basicamente o volume de um sólido
- Ao invés de retângulos temos paralelepípedos
- Mas a moral é a mesma de cologar vários retângulos pro volume se aproximar do real
- a soma dos volumes seria o volume do que seria o sólido
- precisa saber o limite do somatório

## Integral dupla em regiões regulares
Um cálculo de integral dupla se dá pelo cálculo de duas integrais diferentes, uma baseada no x e outra no y (considerando que essas são as variáveis consideradas, a mesma coisa funciona com outras integrais).
Para qualquer região retangular, a ordem dos cálculos não altera o resultado da equação.

- tem uma integral dentro da outra
- em regiões retangulares a ordem das integrais não altera o resultado diretamente
- a-b -> integração em x
- c-d -> integração em y
- o resultado da integral de dentro vira a nova função da integral de fora
- o resultado também é uma área líquida
    - se o resultado é negativo a maior parte do sólido está abaixo do plano xy
- em quadrados a ordem de integração não importa
- os intervalos acabam sempre mostrando retângulos
- a amostragem da região de integração (retangular) é facilmente exposta em [a,b ]x[c,d ]

## Integral dupla em regiões não-retangulares
Por definição:
(a) Uma **região do tipo I** é limitada esquerda e direita por retas verticais x = a e x = b e é limitada abaixo e acima por curvas continuas y = g_1(x) e y = g_2(x), onde g_1(x) <= g_2(x) com a <= x <= b.
(b) Uma **região do tipo II** é limitada abaixo e acima por retas horizontais y = c e y = d e é limitada à direita e à esquerda por curvas continuas x = h_1(y) e x = h_2(y), que satisfazem h_1(y) <= h_2(y) com c <= y <=> d.
Ou seja, **se R for uma região do tipo I**, então primeiro calcule y e depois x.
**Se R for uma região do tipo II**, então primeiro calcule x e depois y.


- regiões não definidas
- pode ser do tipo 1 com limites em x
    - intervalo em y pelas funções
- ou tipo 2 com limites em y
    - intervalo em x pelas funções
- a ordem dos cálculos muda o resultado
- se for do tipo 1
    - intevalo definido em x e por funções em y
    - integra primeiro em y (funções)
    - depois integra em x
- se do tipo 2
    - intervalo definido em y e por funções em x
    - integra primeiro em x (funções)
    - depois integra em y


### Referências
- ANTON, Howard; BIVENS, Irl; DAVIS, Stephen. Cálculo. 10. ed. Porto Alegre: Bookman, 2014. v. 1
- Material de aula fornecido pela Profª Zeliane Santos de Arruda (Unisinos)