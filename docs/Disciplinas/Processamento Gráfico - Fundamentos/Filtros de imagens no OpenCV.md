# Filtros de Imagens no OpenCV
Esse tipo de filtros que estamos falando aqui abordam principalmente a utilização do kernel do openCV (com np.array, do python).
O funcionamento aqui é utilizar o np.array pra criação de uma matriz que será posta sobre a imagem original. Essas matrizes podem variar de tamanho, indo de 3x3, 5x5 a 19x19 e assim por diante. Elas não necessariamente precisam ser quadráticas, permitindo organizações em 3x5 e etc.

## Filtro de Correlação
A aplicação do kernel é feita diretamente em cima da imagem; o sistema basicamente coloca o kernel em cima dela e faz uma multiplicação matricial da imagem pela máscara (kernel); resultando em uma correlação. Dessa forma, diferentes tamanhos de kernel resultam em diferentes resultados (mais "fortes" ou "fracos").
Nesse sentido, a função **filter2D** utiliza a correlação para fazer aplicação no kernel.
```python
correlated_image = cv.filter2D(img, -1, kernel)
```

## Filtro de Convolução
Os filtros desse tipo tem o kernel rotacionado em 180° antes de aplicar em cima da imagem.
Tem aplicações interessantes em detecção de bordas e realces.
Existem alguns desse tipo, os mais conhecidos sendo:
```python
#Filtro Sobel – bordas horizontais
sobel_horizontal = cv.Sobel(img, cv.CV_64F, 1, 0, ksize=3)

#Filtro Laplaciano – bordas em todas as direções
laplacian_image = cv.Laplacian(img, cv.CV_64F)
```

## Passa baixa - suavização
Removedores de ruído e suavizadores de imagens (os blurs entram nessa categoria)
```python
#Filtro de média (blur)
smoothed_image = cv.blur(img,(5,5))

#Filtro Gaussiano
blurred_image = cv.GaussianBlur(img, (5,5), 1.5)
```

## Passa alta - nitidez
Mantém componentes com frequência alta (principalmente bordas e texturas)
```python
# Filtro Laplaciano
laplacian_image = cv.Laplacian(img, cv.CV_64F)

# Filtro de Realce (sharpening)
kernel = np.array([[0, -1, 0],
                   [-1, 5, -1],
                   [0, -1, 0]])
sharpened_image = cv.filter2D(img, -1, kernel)
```

## Estáticos
Operações estatísticas em pixels vizinhos, como o suavizados de bordas e média de cores.
```python
#Filtro de mediana (útil para reduzir ruído)
median_filtered_image = cv.medianBlur(img, 5)

#Filtros de realce de áreas claras e escuras

# Carregar a imagem em escala de cinza
img = cv.imread('baboon.png', cv.IMREAD_GRAYSCALE)

# Definir o kernel (vizinhança)
kernel = np.ones((3, 3), np.uint8)

# Aplicar filtro de Máximo (Dilatação - aumentar as áreas brilhantes)
filtro_maximo = cv.dilate(img, kernel)

# Aplicar filtro de Mínimo (Erosão - aumentar as áreas escuras)
filtro_minimo = cv.erode(img, kernel)
```


### Referências
- Material de aula fornecido pela Profª Rossana Baptista Queiroz (Unisinos)