# Relatório do Projeto: Cena 3D

## Decisões de Modelagem

Para este projeto, implementei uma cena 3D com as seguintes decisões de modelagem:

### Biblioteca Escolhida
Escolhi a biblioteca **Three.js** por ser uma solução robusta e amplamente utilizada para desenvolvimento de aplicações 3D na web. Ela permite a criação de gráficos 3D no navegador sem a necessidade de plugins adicionais.

### Objetos 3D
1. **Cubo**: Implementado com uma textura de tabuleiro xadrez criada programaticamente utilizando Canvas. O padrão xadrez demonstra como aplicar texturas a objetos 3D.
2. **Esfera**: Criada com material laranja avermelhado, com propriedades metálicas médias e baixa rugosidade, dando aparência brilhante.
3. **Cilindro**: Implementado em verde lima com baixa propriedade metálica e alta rugosidade, criando um contraste visual com os outros objetos.

### Sistema de Iluminação
Implementei um sistema de iluminação que inclui:
- **Luz Ambiente**: Para iluminação básica global
- **Luz Direcional**: Simulando luz solar com capacidade de projetar sombras
- **Luz Pontual**: Para iluminação adicional de pontos específicos

### Interatividade
- **Controle de Câmera**: Implementado usando um controle orbital personalizado para permitir ao usuário explorar a cena livremente
- **Painel de Controle**: Interface intuitiva para seleção e manipulação individual dos objetos
- **Transformações**: 
  - Translação (posicionamento X, Y, Z)
  - Rotação em todos os eixos
  - Escala uniforme
- **Controle de Iluminação**: Ajuste da intensidade da luz direcional

### Elementos Adicionais
- Um plano de fundo para que as sombras possam ser visualizadas
- Interface responsiva que se adapta ao tamanho da janela
- Feedback visual sobre qual objeto está selecionado

## Implementação Técnica

### Renderização
A renderização é feita utilizando o WebGLRenderer do Three.js, que aproveita a aceleração de hardware através da GPU para renderizar gráficos 3D de forma eficiente no navegador.

```javascript
const renderer = new THREE.WebGLRenderer({ antialias: true });
renderer.setSize(window.innerWidth, window.innerHeight);
renderer.shadowMap.enabled = true;
document.body.appendChild(renderer.domElement);
```

### Materiais e Texturas
Para demonstrar diferentes tipos de materiais, utilizei o MeshStandardMaterial que permite controlar propriedades como metalicidade e rugosidade:

```javascript
const sphereMaterial = new THREE.MeshStandardMaterial({ 
    color: 0xff4500,  // Laranja avermelhado
    metalness: 0.5,
    roughness: 0.2
});
```

A textura do cubo foi criada programaticamente usando um Canvas para criar um padrão de tabuleiro:

```javascript
function createCheckerboardTexture() {
    const size = 512;
    const canvas = document.createElement('canvas');
    canvas.width = size;
    canvas.height = size;
    
    const context = canvas.getContext('2d');
    context.fillStyle = '#ffffff';
    context.fillRect(0, 0, size, size);
    
    const tileSize = size / 8;
    
    for (let i = 0; i < 8; i++) {
        for (let j = 0; j < 8; j++) {
            if ((i + j) % 2 === 0) {
                context.fillStyle = '#4169E1';
                context.fillRect(i * tileSize, j * tileSize, tileSize, tileSize);
            }
        }
    }
    
    const texture = new THREE.CanvasTexture(canvas);
    texture.needsUpdate = true;
    return texture;
}
```

### Controle de Câmera Personalizado
Devido a limitações de compatibilidade com o OrbitControls do Three.js, implementei um controle de câmera orbital personalizado que permite ao usuário rotacionar a câmera e fazer zoom:

```javascript
class SimpleOrbitControls {
    constructor(camera, domElement) {
        this.camera = camera;
        this.domElement = domElement;
        this.target = new THREE.Vector3(0, 0, 0);
        // ...
    }
    
    // Métodos para manipulação da câmera
    // ...
}
```

## Conclusão

A implementação atende todos os requisitos do projeto, incluindo os três objetos 3D, transformações, iluminação e controle de câmera. A adição de textura ao cubo demonstra técnicas avançadas de renderização 3D, e a interface de usuário intuitiva facilita a interação com a cena.

Um desafio enfrentado durante o desenvolvimento foi a implementação do controle de câmera, que exigiu a criação de uma solução personalizada para garantir compatibilidade entre diferentes ambientes de execução.

O resultado final é uma aplicação web 3D interativa que pode ser facilmente estendida para incluir objetos mais complexos, animações e interações adicionais no futuro.