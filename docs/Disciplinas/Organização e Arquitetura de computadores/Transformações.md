# Transformações
Todas as transformações e rotações utilizam matrizes para os cálculos.
Além disso, precisam ainda transferir o objeto para a origem e depois ainda colocar na posição necessária.

▪ vec2: ponto 2D (x,y) ou coordenada de textura (s,t)
▪ vec3: ponto ou direção 3D (x,y,z)
▪ vec4: ponto 4D (x,y,z,1.0) ou direção 4D (x,y,z,0.0)
▪ Lembre-se que uma matriz 4x4 só pode ser transformada
por um vetor 4D e uma matriz 3x3 por um vetor 3D

- nos objetos
- precisar usar trigonometria pra fazer os giros (claramente já que é o espaço)

Uma vez que a trigonometria é bastante utilizada, sinta-se encorajado para dar uma olhada neste projeto iterativo sobre o mesmo: https://phet.colorado.edu/en/simulations/trig-tour -> prometo que o site é seguro

Outro recurso muitíssimo utilizado são as matrizes, uma vez que as imagens se dão em uma matriz (a tela do computador), nada mais justo que os cálculos serem matriciais.
Todas as operações com matrizes são utilizadas aqui, sinta-se a vontade para revisar operações com matrizes em https://pt.khanacademy.org/math/algebra-home/alg-matrices

Tenha em mente que as transformações ocorrem por meio dos cálculos angulares trigonométricos e matriciais, mas não se preocupe, o OpenGL (e outras bibliotecas gráficas) o fazem por você (o trabalho pesado pelo menos).

## Translação
É a movimentação de um objeto pelos eixos - todos os pontos do polígono são movidos
xt = x + Tx
yt = y + Ty

## Escala
Altera-se o "tamanho" do objeto, ou a sua escala. Pontos podem ficar maiores, arestas aumentam de tamanho, a área/volume do polígono se altera, etc
Existem escalas uniformes e não uniformes, conforme Ex = Ey e Ex != Ey
Para realizar esse cálculo multiplica-se um fator de escala:
xe = x * Ex
ye = y * Ey

## Rotação
A rotação é interessante uma vez que ela necessita trazer o objeto novamente para a origem, rotacioná-lo e aí sim devolvê-lo para a região de onde foi retirado - isso porquê, caso contrário, ele mudaria de posição ao invés de ângulo (já que é uma soma simples e as posições dos pontos também mudam).
É basicamente uma soma de ãngulos, de forma que os pontos formam um ângulo α em relação à origem. Quando aplicamos uma rotação, adicionamos um ângulo θ à α, e com isso precisamos recalcular a posição dos pontos conforme esse novo ângulo α+θ
xr = x.cos(θ) - y.sen(θ)
yr = y.cos(θ) + x.sen(θ)

Para evitar movimentações desnecessárias no plano:
x' = (x - xp).cos(θ) – (y – yp).sin(θ) + xp
y' = (x - xp).sin(θ) + (y – yp).cos(θ) + yp
-> esse é o chamado pivot da rotação.

## Outras transformações
Ainda existem algumas outras mais situacionais, como:

### Reflexão
Eixo X
x’ = x
y’ = -y

Origem
x’ = -x
y’ = -y

Eixo Y
x’ = -x
y’ = y

### Shearing (deslizamento)
xs = x + Sx
ys = y + Sy

Isso é uma manipulação de um dos lados de um polígono

## Homogeneização de matrizes e vetores
Isso vale tanto para objetos 2D quanto 3D.
Se rezume a completar o vetor um um 3° elemento para homogeneizá-lo. Já que os cálculos matriciais e vetoriais necessitam de operações *completas*, ou seja, uma matriz precisa *necessariamente* ser quadrática, essa homogeinização adiciona o valor **1** para completar.
Esse multiplicação e usabilidade é possível a partir do momento que o OpenGL ainda guarda as informações de matrizes vetorizadas e precisa calcular para matriciá-las e jogá-las na placa de vídeo.

### Referências
- https://learnopengl.com//#!Getting-started/Transformations
- Slides sobre CG dos professores: Christian Hofsetz, Cristiano Franco, Marcelo Walter, Soraia Musse, Leandro Tonietto e Rafael Hocevar
- Material de aula fornecido pela Profª Rossana Baptista Queiroz (Unisinos)