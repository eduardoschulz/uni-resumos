# Sistemas de cores e Introdução ao Processamento de Imagens
Processamento gráfico trabalha com imagens puras e o processamento de imagens ainda segue as normas previamente vistas.
Grosso modo  uma *imagem* é, "nas ciências exatas, como a matemática, o termo "imagem" é entendido como representação de um objeto especializado, que exige técnicas e ferramentas especiais." - wikipédia
Como trabalhamos com matrizes de valores, uma imagem é isso mesmo, uma matriz de **pixels** - *picture elements*.
Cor, sendo uma percepção visual de luz e a luz, sendo uma onda/partícula, telas podem transmitir perfeitamente ilusões de luz.
Se quiser mais informações sobre cores, luz e etc., acesse https://pt.wikipedia.org/wiki/Cor

Existe o Diagrama de Cromaticidade CIE que é basicamente uma forma (X+Y+Z)=1 planificada em x e y, nesse caso, é uma forma meio bizarra onde as cores puras estão nas pontas.

A geração de imagens pelo computador depende de hardware, o qual pode ser por:
CRT (Cathode Ray Tube) - método de TV's de tubo
LCD (Liquid Cristal Display) - tem vários componentes de luz ligados em uma central - vários feixed de luz.

As dimensões da tela ainda usam os dimensionamentos padrão (640x480, 1280x1024) - o produto dessas dimensões identifica os **megapixels** - produto de largura pela altura

A quantidade de bits pode alterar a quantidade de cores representadas na tela. Por isso usualmente imagens e processamentos em gray scale são mais leves
O básico é que o *truecolor* surge a partir de 24 bits e é aí que o canal alfa (luminosidade) aparece para uso.
Caso queira mais informações sobre luminosidade, acesse https://pt.wikipedia.org/wiki/Profundidade_de_cor

Dessa forma, uma imagem é basicamente um conjuto de pixels, cada um com uma coordenada específica

Os modelos mais comuns de uso de cores são o RGB, CMY(K), HSV.
Cheque mais detalhes em https://pt.wikipedia.org/wiki/RGB, https://pt.wikipedia.org/wiki/CMYK e https://pt.wikipedia.org/wiki/HSV.
Inclusive, HSV é um dos modelos mais utilizados para editores de imagem.

### Referências
- Notas de Aula do professor Leandro Tonietto
- Notas de aula do professor Marcelo Walter (UFRGS)
- Notas de aula do professor Bruno Carvalho (UFRN)
- FOLEY, J.D. et al. Computer graphics: principles and practice. Reading: Addison-Wesley, 1990.
- TONIETTO, Leandro; WALTER, Marcelo. Análise de Algoritmos para Chroma-key. Unisinos, 2000.
- Material de aula fornecido pela Profª Rossana Baptista Queiroz (Unisinos)