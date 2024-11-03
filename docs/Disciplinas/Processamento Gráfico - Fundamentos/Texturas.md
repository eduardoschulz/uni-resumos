# Texturas
As texturas surgiram para fazer uma "imitação" do que seria tal elemento com todos os polígonos presentes. Subtitui a necessidade de utilizar diversos polígonos enquanto ainda causa a ilusão de uma superfície.
Tudo que precisamos fazer é informar ao OpenGL os "cantos" do polígono, ou melhor, a região que tal textura precisa ficar que o **fragment shader** cuida da **interpolação** (preenche o resto).
Utilizando como coordenadas básicas de 0 a 1, um possível código para "placement" de uma textura poderia ser:

```C++
GLfloat texCoords[] = {
0.0f, 0.0f, // Inferior esquerdo
1.0f, 0.0f, // Inferior direito
1.0f, 1.0f, // Superior direito
0.0f, 1,0f // Superior esquerdo
};
```
## Texture Wrapping
Entre os pontos, o OpenGL pode fazer algumas coisas:
– GL_REPEAT: comportamento padrão, que repete a imagem de textura
– GL_MIRRORED_REPEAT: mesmo que GL_REPEAT mas espelha a imagem a cada repetição.
– GL_CLAMP_TO_EDGE: “prende”as coordenadas entre 0 e 1. Os valores mais altos ficam presos às arestas.
– GL_CLAMP_TO_BORDER: coordenadas for a do intervado recebem uma cor de borda.

Existem algumas maneiras de settar, mas as coordenadas s e t são necessárias; trate como x e y:
```C++
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_S, GL_MIRRORED_REPEAT);
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_T, GL_MIRRORED_REPEAT);
```

## Texture Filtering
Ou **Texture smoothing**. Esse processo serve para consertar problemas causados por compressão ou aumento muito grande de imagem (as texturas). Algumas técnicas podem ser usadas:

### Neares Neighbor Filtering
Se falta pixel pega a cor do vizinho mais próximo
```C++
glTexParameter(GL_TEXTURE_2D, GL_TEXTURE_MAG_FILTER, GL_NEAREST);
glTexParameter(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_NEAREST);
```
A imagem tem tendência de ficar pixelada e bastante forte.

### Linear Filtering
Faz uma média de todos os vizinhos; os pixels faltantes tem uma cor mediana.
Normalmente geram imagens mais *fuzzy* ou pouco nítidas.
```C++
glTexParameter(GL_TEXTURE_2D, GL_TEXTURE_MAG_FILTER, GL_LINEAR);
glTexParameter(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_LINEAR);
```

## Minimaps
O OpenGL pode gerar imagens menores de uma textura automaticamente.
A biblioteca faz divisões lineares (divisões por 2) diversas vezes e armazena versões *miniaturizadas* das mesmas imagens.
Existe um método padrão, mas é possível especificá-lo com:
– GL_NEAREST_MIPMAP_NEAREST: usa o mipmap mais próximo do tamanho do pixel e usa o método de interpolação do vizinho mais próximo para amostrar a textura
– GL_LINEAR_MIPMAP_NEAREST: usa o mipmap mais próximo do tamanho do pixel e usa o método de interpolação linear para amostrar a textura
– GL_NEAREST_MIPMAP_LINEAR: faz a interpolação linear dos dois mipmaps mais próximos ao tamanho do pixel e usa o método de interpolação do vizinho mais próximo para amostrar a textura
– GL_LINEAR_MIPMAP_LINEAR: faz a interpolação linear dos dois mipmaps mais próximos ao tamanho do pixel e usa o método de interpolação linear para amostrar a textura
 
```C++
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_LINEAR_MIPMAP_LINEAR);
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MAG_FILTER, GL_LINEAR);
```

## Mapeamento UV em modelos 3D
É um mapeamento do objeto 3D. Como se fosse uma planta baixa mesmo. Igual quando montávamos bonecos de papel os quais formavam cubos.
Tem algumas etapas, mas a principal delas é o **mapeamento de textura**. A mesma planta baixa, mas com as texturas aplicadas. É consideravelmente mais simples aplicar texturas em polígos simples que em poliedros.

## Inicialização de texturas
As texturas precisam ser obviamente inicializadas e colocadas dentro do projeto na hora do carregamento.
Cheque abaixo alguns dos métodos para inicializá-las.

- **Gere o ID da textura**
```C++
// Gera o identificador da textura na memória
glGenTextures(1, &texID);
glBindTexture(GL_TEXTURE_2D, texID);
```

- **Ajuste os parâmetros de *wrapping* e *filtering***
```C++
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_S, GL_REPEAT);
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_T, GL_REPEAT);

glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_LINEAR);
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MAG_FILTER, GL_LINEAR);
```

- **Faça o carregamento da imagem**
-> Com a biblioteca stb_image (https://github.com/nothings/stb), esse processo é mais facilitado; considere dar um check.
```C++
int width, height, nrChannels;

unsigned char *data = stbi_load(filename.c_str(), &width, &height,
&nrChannels, 0);
```

- **Agora é só mandar os dados para a memória do OpenGL e trabalho feito**
```C++
if (data)
{
  if (nrChannels == 3) //jpg, bmp
  {
    glTexImage2D(GL_TEXTURE_2D, 0, GL_RGB, width, height, 0, GL_RGB, GL_UNSIGNED_BYTE, data);
  }
  else //png
  {
    glTexImage2D(GL_TEXTURE_2D, 0, GL_RGBA, width, height, 0, GL_RGBA, GL_UNSIGNED_BYTE, data);
  }
  glGenerateMipmap(GL_TEXTURE_2D);
  }
else
{
  std::cout << "Failed to load texture" << std::endl;
}
```

- **Algumas boas práticas interessantes**
```C++
// Considere sempre liberar o buffer de memória depois de usar (isso aqui ainda é baseado em C, ou seja, não existem muitas ferramentas de unassign de memória)
stbi_image_free(data);

glBindTexture(GL_TEXTURE_2D, 0);

// Precisa ativar o buffer de textura do OpenGL
glActiveTexture(GL_TEXTURE0);

// Sempre faça o bind das unidades de textura (as imagens mesmo) com os buffers os quais elas precisam estar relacionadas
glActiveTexture(GL_TEXTURE0);
glBindTexture(GL_TEXTURE_2D, textID1);
glActiveTexture(GL_TEXTURE1);
glBindTexture(GL_TEXTURE_2D, textID2);
glBindVertexArray(VAO);
glDrawElements(GL_TRIANGLES, 6, GL_UNSIGNED_INT, 0);
```

## Buffers
Agora os buffers do OpenGL possuem mais atributos e nossos leitores precisam espelhar tal fato.
Considere montar estruturas parecidas:
```C++
float vertices[] = {
// posicoes // cores // coordenadas de textura
0.5f, 0.5f, 0.0f, 1.0f, 0.0f, 0.0f, 1.0f, 1.0, // superior direito
0.5f, -0.5f, 0.0f, 0.0f, 1.0f, 0.0f, 1.0f, 0.0f, // inferior direito
-0.5f, -0.5f, 0.0f, 0.0f, 0.0f, 1.0f, 0.0f, 0.0f, // inferior esquerdo
-0.5f, 0.5f, 0.0f, 1.0f, 1.0f, 0.0f, 0.0f, 1.0 // superior esquerdo
};
unsigned int indices[] = {
0, 1, 3, // primeiro triangulo
1, 2, 3 // segundo triangulo
};

//-------------------------------------------------------------------------
glGenVertexArrays(1, &VAO); glGenBuffers(1, &VBO); glGenBuffers(1, &EBO);
glBindVertexArray(VAO);
glBindBuffer(GL_ARRAY_BUFFER, VBO);
glBufferData(GL_ARRAY_BUFFER, sizeof(vertices), vertices, GL_STATIC_DRAW);
glBindBuffer(GL_ELEMENT_ARRAY_BUFFER, EBO);
glBufferData(GL_ELEMENT_ARRAY_BUFFER, sizeof(indices), indices, GL_STATIC_DRAW);
// position attribute
glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, 8 * sizeof(float), (void*)0);
glEnableVertexAttribArray(0);
// color attribute
glVertexAttribPointer(1, 3, GL_FLOAT, GL_FALSE, 8 * sizeof(float), (void*)(3 * sizeof(float)));
glEnableVertexAttribArray(1);
// texture coord attribute
glVertexAttribPointer(2, 2, GL_FLOAT, GL_FALSE, 8 * sizeof(float), (void*)(6 * sizeof(float)));
glEnableVertexAttribArray(2);
```

**Não esqueça do vertex shader!**
```C++
#version 450 core
layout (location = 0) in vec3 position;
layout (location = 1) in vec3 color;
layout (location = 2) in vec2 tex_coord;
out vec4 vertexColor;
out vec2 texCoord;
uniform mat4 model;
uniform mat4 projection;
void main()
{
gl_Position = projection * model * vec4(position, 1.0f);
vertexColor = vec4(color,1.0);
texCoord = vec2(tex_coord.x, tex_coord.y);
}

//---------------------------------------------------------
#version 450 core
in vec3 vertexColor;
in vec2 texCoord;
out vec4 color;
// pixels da textura
uniform sampler2D tex_buffer;
void main()
{
color = texture(tex_buffer, texCoord);
}
```

## Finalizando
Alguns lembretes na hora de finalizar seus métodos para completar o programa:
```C++
//Não esquecer de chamar o método para carregar a imagem ☺
GLuint texID = loadTexture("./textures/mario.png");

// Não esquecer de especificar a variável uniform que vai conter os dados da textura no fragment shader
glUniform1i(glGetUniformLocation(shader.ID, "tex_buffer"), 0);

//Antes da drawcall:
glActiveTexture(GL_TEXTURE0);
glBindTexture(GL_TEXTURE_2D, texID);
glBindVertexArray(VAO);
glDrawElements(GL_TRIANGLES, 6, GL_UNSIGNED_INT, 0);
glBindVertexArray(0);
```

### Referêcias
- Slides sobre CG dos professores: Christian Hofsetz, Cristiano Franco, Marcelo Walter, Soraia Musse, Leandro Tonietto e Rafael Hocevar
- https://learnopengl.com/Getting-started/Textures
- Material de aula fornecido pela Profª Rossana Baptista Queiroz (Unisinos)