# Camads de sprites e cenários 2D
Cada ciclo do *Game Loop* vai gerar um sprite diferente. Lembre-se de que o game loop sempre passa pelo renderer um update e um sync.
Os sprites estão presentes dentro de uma **Spritesheet**, como uma contendo os estágios de animação de um personagem.
Tal personagem pode possuir uma SpriteSheet com o loop de caminhada que se repete toda vez que ele caminha, dessa forma, o game loop também "caminha" pela spritesheet mostrando as fases.
O posicionamento das imagens é baseado em x, y e z.
Para que o sprite exista, ele precisa estar associado a um quadrilátero qualquer, para que o sprite sirva como uma "textura".
Todas as imagens vem pelo *shader*. Veja uma implementação simples:
```C++
glEnable(GL_DEPTH_TEST);
glDepthFunc(GL_ALWAYS);

glClear(GL_COLOR_BUFFER_BIT |
GL_DEPTH_BUFFER_BIT);

// Para existir transparência, use:
glEnable(GL_BLEND);
glBlendFunc(GL_SRC_ALPHA, GL_ONE_MINUS_SRC_ALPHA);
```
## Recorte de imagens - Spritesheet
A spritesheet funciona basicamente como uma matriz mesmo.
Divide-se o "papel" onde ela está em diferentes segmentos os quais correspondem a estágios da animação. Assim sendo, tudo que o programa faz é navegar pelos diferentes estágios dessa matriz que é a spritesheet.
Uma implementação de uma spritesheet deve levar em conta, agora, os frames de animação presentes. Para isso, uma implementação necessária é:
```C++
iFrame = (iFrame+1) % nFrames
```

Os **Offsets** serão basicamente coordenadas para puxar determinado sprite.
Tenha como exemplo:
```C++
// Na inicialização do sprite
dx = 1.0 / (float)nFrames;
dy = 1.0 / (float)nAnimations;
float vertices[] = {
// positions // colors // texture coords
0.5f, 0.5f, 0.0f, 1.0f, 0.0f, 0.0f, dx, dy, // top right
0.5f, -0.5f, 0.0f, 0.0f, 1.0f, 0.0f, dx, 0.0f, // bottom right
-0.5f, -0.5f, 0.0f, 0.0f, 0.0f, 1.0f, 0.0f, 0.0f, // bottom left
-0.5f, 0.5f, 0.0f, 1.0f, 1.0f, 0.0f, 0.0f, dy // top left
};

// Na atualização do sprite
GLint offsetLoc = glGetUniformLocation(shader->Program, "offset");
glUniform2f(offsetLoc, iFrame * dx, iAnimation * dy);
iFrame = (iFrame + 1) % nFrames;

// No shader
#version 450 core
in vec2 TexCoord;
out vec4 color;
// pixels da textura
uniform sampler2D tex1;
//Texture coords offsets for animation
uniform vec2 offset;
void main()
{
color = texture(tex1, TexCoord+offset);
}

// Dentro do gameloop, ainda é necessário implementar algum tipo de timer para coordenar os sprites
//GAME LOOP
while (!glfwWindowShouldClose(window))
{
timer.start();
//faz as chamadas de update e desenho...

// E ainda uma classe timer
#include <chrono>
#include <thread>
#include <ctime>
class Timer
{
public:
Timer();
void start() { begin = std::chrono::system_clock::now(); }
void finish() { end = std::chrono::system_clock::now(); }
double getElapsedTimeMs()
{
std::chrono::duration<double> elapsed_seconds = end - begin;
return elapsed_seconds.count() * 1000;
}
double getElapsedTime()
{
std::chrono::duration<double> elapsed_seconds = end - begin;
return elapsed_seconds.count();
}
double calcWaitingTime(int fps, double elapsedTime) {
double wt = 1000 / (double)fps - elapsedTime;
return wt;
}
protected:
// Using time point and system_clock
std::chrono::time_point<std::chrono::system_clock> begin,
end;
};
```

Ainda é necessário implementar um **waiting time**. Caso ele não exista, a animação funciona, mas ela fica descompassada e não-natural.
É bastante interessante usar um waiting time a fim de, por exemplo, colocar uma velocidade diferente do personagem correndo e andando (de animação no caso).
```C++
double calcWaitingTime(int fps, double elapsedTime) {
  double wt = 1000 / (double)fps - elapsedTime;
  return wt;
}

//GAME LOOP
while (!glfwWindowShouldClose(window))
{
  timer.start();
  glfwPollEvents();
  //...Chama métodos de atualização e desenho dos objetos da cena....
  //Sincronizando o FPS
  timer.finish();
  double waitingTime = timer.calcWaitingTime(60, timer.getElapsedTimeMs());
  if (waitingTime)
  {
  std::this_thread::sleep_for(std::chrono::milliseconds((int)waitingTime));
  }
  glfwSwapBuffers(window);
}
```

## Camadas e Parallax
O efeito de parallaxe não é exatamente simples de ser executado.
Na realidade, é necessário quebrar quebrar a imagem em algumas camadas (como árvores mais adentro separado de uma casa ao fundo) para ser possível *simular* a realidade.
Como na invenção de animação do Walt Disney (dê uma olhada https://www.youtube.com/watch?v=YdHTlUGN1zw), as camadas se movem e tem comportamento um tanto diferentes. A magia está no movimento.
Essa implementação de camadas são os **layers**
A viewport sendo uma câmera, se comporta tal qual a invenção e um offset é necessário:
```C++
layers[i]->setOffsets(offsetx,offsety);
```
Considerando que ainda são "texturas", precisamos definir coordenadas x e y, assim como definição de qual layer é.

Uma forma de implementação seria:
```C++
for all layers [0..n]
layers[i]->computeScrollRateX(mainLayer->getWidth());
layers[i]->computeScrollRateY(mainLayer->getHeight());

for all layers [0..n]
layers[i]->scroll(forward);

for all layers [0..n]
layers[i]->plot(viewport); // será alterado para animação

for all layers [0..n]
layers[i]->computeScrollRateX(mainLayer->getWidth());
layers[i]->computeScrollRateY(mainLayer->getHeight());

for all layers [0..n]
layers[i]->scroll(forward);
```

### Referências
- LearnOpenGL - Anton's OpenGL 4 Tutorials
- https://learnopengl.com/
- Material de aula fornecido pela Profª Rossana Baptista Queiroz (Unisinos)