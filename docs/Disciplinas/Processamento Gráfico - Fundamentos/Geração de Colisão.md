# Geração de colisão
Uma implementação de colisão simples é considerar os lados dos polígonos e identificar se eles estão sobrepostos.
Veja a implementação simples:
```C++
bool checkCollision(Sprite &one, Sprite &two)
{
  // collision x-axis?
  bool collisionX = one.getPMax().x >=
  two.getPMin().x &&
  two.getPMax().x >= one.getPMin().x;
  // collision y-axis?
  bool collisionY = one.getPMax().y >=
  two.getPMin().y &&
  two.getPMax().y >= one.getPMin().y;
  // collision only if on both axes
  return collisionX && collisionY;
}
```

### Referências
- Material de aula fornecido pela Profª Rossana Baptista Queiroz (Unisinos)