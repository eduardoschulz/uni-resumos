# Integrais impróprias
Na definição geral, temos que uma integral tem um espaço de aplicação contínuo e finito, como em ∫^b_a f(x)dx.
Todavia, quando o caso é uma integral com um dos limites infinitos, a coisa muda um pouco de figura. Como não podemos provar que não exitem infinitas descontinuidades em um espaço infinito dado, precisaremos utilizar limites para completarmos o cálculo.
Para calcular uma integral imprópria, podemos trocar o limite infinito por um dado finito (b se superior e a se inferior), calcular a integral, e colocar o resultado dentro de um limite de b->∞ ou a->-∞ e aplicar o limite

**Definição**
1. Se f é contínua no intervalo [a, ∞), então
∫^∞_a f(x)dx = lim_(b->∞)∫^b_a f(x)dx

2. Se f é contínua no intervalo (-∞, b], então
∫^b_-∞ f(x)dx = lim_(a->-∞)∫^b_a f(x)dx

3. Se f é contínua no intervalo (-∞, ∞), então
∫^∞_-∞ f(x)dx = ∫^c_-∞ f(x)dx + ∫^∞_c f(x)dx em que c é qualquer número real (normalmente utiliza-se 1 - é considerado a "metade dos infinitos" - é meio arbitrário mesmo).
Observe que: "Em cada caso, se o limite existir, a integral imprópria converge; caso contrário, a integral diverge. No terceiro caso, a integral à esquerda do sinal de igualdade diverge se uma das integrais impróprias à direita diverge."

Também existo o caso para que caso exista alguma descontinuidade infinita (daquele ponto ao infinito, positivo ou negativo) temos algumas regras, que funcionam basicamente como as anteriores:
**Definição 2**
1. Se f é contínua no intervalo [a, b) e tem uma descontinuidade infinita em b, então
∫^b_a f(x)dx = lim_(c->b^-)∫^c_a f(x)dx

2. Se f é contínua no intervalo (a, b], e tem uma descontinuidade infinita em a, então
∫^b_a f(x)dx = lim_(c->-a^+)∫^b_c f(x)dx

3. Se f é contínua no intervalo [a, b], exceto em c pertencente a (a, b), onde f tem uma descontinuidade infinita , então
∫^b_a f(x)dx = ∫^c_a f(x)dx + ∫^b_c f(x)dx

Observe que: "Em cada caso, se o limite existe, a integral imprópria converge; caso contrário, a integral diverge. No terceiro caso, a integral imprópria à esquerda do sinal de igualdade diverge se uma das integrais impróprias à direita diverge."

- não dá pra usar o teorema fundamental do cálculo
- quando tem limites infinitos ou descotinuidade da função
    - nesse momento não se utiliza as com descontinuidade
- [1 ]
- o resultado de uma integral com infinito é o limite do resultado dela 
- alguns resultados podem ser indeterminados (indeterminação matemática)
    - integral diverge (divergente)
- se o resultado é um número real ela converge (convergente)
- [2 ]

<img src="imgs/2024-10-02_Exercicios.png">
<img src="imgs/2024-10-02_Exercicios_2.png">
<img src="imgs/2024-10-02_Exercicios_3.png">

### Referências
- ANTON, Howard; BIVENS, Irl; DAVIS, Stephen. Cálculo. 10. ed. Porto Alegre: Bookman, 2014. v. 1 
- Material de aula fornecido pela Profª Zeliane Santos de Arruda (Unisinos)