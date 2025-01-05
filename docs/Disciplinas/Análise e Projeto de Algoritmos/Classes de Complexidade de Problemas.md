# Classes de Complexidade de Problemas
Classes de complexidade são definições dadas a problemas dentro do contexto de **Teoria da Computação**, uma vez que ela se preocupa bastante em definir limitações e possibilidades para computadores. No fim das contas, essas classes são uma maneira de definir esses limites.
Todos os problemas podem ser definidos em:
Problemas -> Computáveis -> (Completamente) Solucionáveis
                         -> Parcialmente solucionáveis
          -> Não-computáveis = Não-solucionáveis
-> Complexidade vai trabalhar no ramo de Computáveis

Desses problemas que as classes abordam, eles podem ser:
- P
    - Resolvidos em tempo polinomial e tem soluções completas
- NP
    - *Nondeterministic polynomial-time*
    - Apenas sua solução pode ser determinada em tempo polinomial (verificação)
- NP-completos
    - O algorítimo que resolve isso aqui é o força-bruta
    - Não tem muito o que fazer e a solução não é verificada em tempo polinomial também
    - São tidos como problemas intratáveis
    - Tão complicados quanto os NP
- NP-difíceis
    - Esse é uma área meio cinza
    - São tão complexos quanto NP (solução verificável), mas podem também não ser NP, o que os torna tão complexos quanto NP-completos (só força-bruta)
    - De fato são difícieis
Em resumo, problemas NP englobam P e NP-difícil é outra parada, quando NP-difícil e NP se encontram, eles formam um problema NP-completo
-> Fun-fact: essas classes abordam **problemas de decisão**, que envolvem escolhs de lados, caminhos, if-else, etc. e por isso tem essa questões.

Agora, lembre-se do fato que problemas P estão englobados por problemas NP, isso significa que **P = NP**?
Essa pergunta, na verdade, é bastante famosa no mundo da computação e ainda não pode ser desmintida ou confirmada.
Há quem acredita que isso é uma falácia matemática e uma incongruência, mas outros contrapôe que não podemos nos dar por vencidos porque é virutalmente inpossível verificarmos todos os problemas do mundo (não temos uma contraprova eficaz).


### Referências
- The Algorithm Design Manual (Skiena) 
    - Capítulo 9 - Intractable Problems and Approximation Algorithms
- Material desenvolvido com base nos originais do professor Sandro Rigo (Unisinos)
- material da professora Andriele Busatto (Unisinos)