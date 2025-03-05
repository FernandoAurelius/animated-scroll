# Animated Scroll

Este projeto demonstra como implementar animações baseadas em scroll utilizando HTML, CSS e JavaScript.

## Conceitos Principais

### Animações com CSS
- **Estados dos Elementos:**  
  Os elementos iniciam com a classe `.hidden`, que define:  
  - `opacity: 0`: Elemento invisível.  
  - `filter: blur(5px)`: Aplica desfoque.  
  - `transform: translateX(-100%)`: Desloca o elemento para fora da tela.

- **Transições Suaves:**  
  Quando a classe `.show` é adicionada, os elementos mudam para:  
  - `opacity: 1`: Elemento visível.  
  - `filter: blur(0)`: Remove o desfoque.  
  - `transform: translateX(0)`: Posiciona o elemento na tela.  
  Essas mudanças são animadas suavemente devido à propriedade `transition: all 1s`.

- **Acessibilidade:**  
  Utiliza-se `@media(prefers-reduced-motion)` para desabilitar as animações caso o usuário prefira menos movimento.

### IntersectionObserver para Scroll
- **Detecção de Visibilidade:**  
  O `IntersectionObserver` é utilizado para monitorar quando os elementos com a classe `.hidden` entram ou saem da viewport.

- **Ativação das Animações:**  
  Ao detectar que um elemento está visível (`entry.isIntersecting`), o script adiciona a classe `.show`, iniciando a animação. Caso contrário, a classe é removida.

- **Delay Dinâmico:**  
  É atribuído um `transitionDelay` a cada elemento, calculado pelo seu índice na lista, criando um efeito de cascata na animação:
  ```js
  element.style.transitionDelay = i * 200 + "ms";
  ```

## Código JavaScript

O JavaScript utilizado no projeto é responsável por observar os elementos e adicionar ou remover classes com base na visibilidade dos elementos na viewport.

```js
// Seleciona todos os elementos com a classe "hidden"
const hiddenElements = document.querySelectorAll(".hidden");

// Cria um IntersectionObserver com uma função callback
const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
        if (entry.isIntersecting) {
            entry.target.classList.add("show");
        } else {
            entry.target.classList.remove("show");
        }
    });
});

// Observa cada elemento e adiciona um delay de transição
hiddenElements.forEach((element, i) => {
    element.style.transitionDelay = i * 200 + "ms";
    observer.observe(element);
});
```

## Estrutura do Projeto

- **HTML:**  
  Define a estrutura básica do conteúdo e inclui seções que serão animadas.

- **CSS:**  
  Define os estilos e as animações para os elementos, utilizando classes `.hidden` e `.show`.

- **JavaScript:**  
  Utiliza o `IntersectionObserver` para monitorar a visibilidade dos elementos e adicionar/remover classes para ativar/desativar animações.

## Referência

Baseado no vídeo "[Subtle, yet Beautiful Scroll Animations](https://www.youtube.com/watch?v=T33NN_pPeNI)" 