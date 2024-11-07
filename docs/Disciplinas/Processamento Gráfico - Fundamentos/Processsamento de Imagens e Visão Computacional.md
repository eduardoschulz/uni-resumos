# Processamento de Imangens & Visão Computacional
Geração de imagens utiliza algumas técnicas interessantes para leitura de dados. Uma delas é streamlizar em matrizes, pixalizar e aplicar qualquer mudança cabível.

-> Processamento de imagens pega os valores numéricos, trabalha com eles e cuspe novos valores
  - bastante útil para reconhecimento de padrões e tratamento
-> Visçao computacional tenta emular a visão humana, puxando uma imagem e cuspindo uma interpretação

A manipulação de imagens tem algumas ideias interessantes.
Alterações de ruído e tirar *blur*, monitoramento, montagem de interfaces não usuais - treinamento de IA, automação industrial, etc.
Alguns desses tipos de automações retiram a necessidade de um humano ver o ambiente e analisá-lo mecanicamente.

**Imagem vetorisada** -> utiliza um vetor pre-existente para relacionar os valores de cores e geração de imagens. Dessa forma, a imagem vai evitar distorções durante um upscaling ou downscaling, ao contrário do bitmap. Mas o custo é bastante considerável.

## Representação e Mapa de bits (bitmap)
Os pixels todos são constituídos de bits, os quais seguram uma quantidade específica de informações.
As quantidades mais famoses de bit por pixel são 1, 2, 4, 8, 15, 16, 24 e 32
O pixel é uma estrutura e pode também ser enfileirado e usado como um "stack".
Os pixels da imagem toda são arrays unidimensionais e dessa forma tem alguns esquemas:
```python
# Processo para RGB
pixels[c + x*channels + y*width*channels]

– n = n / channels;
– x = n % width;
– y = n / width;
```

### Programando com imagens
Em quantidades maiores de bits o **canal alfa** serve como um medido de opacidade para as cores, uma forma de alterar a *transparência*.
Para RGB, por exemplo, 0 é transparente e 255 é opaco.
Cosiderando um objeto à frente do outro, uma transparência maior pode revelar uma sobreposição e uma soma das cores
```python
# mistura
C = c1*α + c2*(1-α)

# Canal B (blue) e alfa=0.5
C = 250*0.5 + 100*(1-0.5)
C = 250*0.5 + 100*0.5
c = 125 + 50 = 175

# Esses cálculos devem ser feitos para todos os canais dado que conforme o canal abordado, a avaliação de presença de cor se altera.
```

## Filtros de imagem
Uma manipulação dos pixels de uma imagem.
Basicamente uma brincadeira com as escalas e representações de cores.
Exemplos: brilho/contraste, correção gamma, sharpen, blur, sépia, etc.

Alguns exemplos tendem a ser:
```python
# gray-scale trivial
gray = r*0.333 + g*0.333 + b*0.333

# gray-scale seguindo a taxa de percepção do olho humano
# sim o olho percebe as cores de formas diferentes
gray = r*0.2125 + g*0.7154 + b*0.0721

# Colorização de imagem por cima de uma imagem rbg normal
newrgb = rbg | rgbModifier

# RGB negativo
canal ^ 255 # operação XOR
# Dá pra aplicar em um ou dois canais só para resultados diferentes
```
Outro ainda é a binarização de uma imagem. Ela precisa estar já em gray-scale, já que mede intensidade e não cor, mas ela diminui a quantidade de dados necessários para guardá-la, o que pode vir a ser bastante útil.

### Referências
- TONIETTO, Leandro; WALTER, Marcelo. Análise de Algoritmos para Chroma-key. Unisinos, 2000.
- GONZALEZ, Rafael C.; WOODS, Richard E. Digital image processing. 4nd ed. India: Person, c2018. 1019 p. ISBN 9789353062989
- Material de aula fornecido pela Profª Rossana Baptista Queiroz (Unisinos)