# BIMQUADOO# Infográfico Interativo BIM — Quadoo

Infográfico interativo de página única que apresenta as 11 etapas do processo BIM da Quadoo. O menu inicial em forma de losango funciona como índice navegável: cada número abre a arte correspondente com uma animação de arraste, e o ícone da Quadoo presente em cada tela retorna ao menu.

## Arquivo

- **`quadoo_bim_infografico.html`** — aplicação completa, em um único arquivo.

Todas as imagens estão embutidas no próprio HTML (em base64). Não há dependências externas, nenhuma biblioteca e nenhuma conexão à internet: basta o arquivo `.html`.

## Como usar

Abra `quadoo_bim_infografico.html` em qualquer navegador moderno (Chrome, Edge, Firefox, Safari). Funciona com dois cliques no arquivo, hospedado em um site, ou embutido em outra página via `<iframe>`.

### Navegação

- **Números 01 a 11** — cada número do losango é um botão que abre a etapa correspondente. Ao passar o mouse, um destaque circular indica que é clicável.
- **Losango branco central ("o que é BIM?")** — abre a tela de vantagens do BIM.
- **Ícone da Quadoo** — presente no canto de cada tela de etapa; clicar nele retorna ao menu inicial.

## Mapa de navegação

| Botão | Etapa |
|-------|-------|
| 01 | Reforma |
| 02 | Programa de Necessidades |
| 03 | Projeto Conceitual |
| 04 | Desenvolvimento de Projeto |
| 05 | Análise |
| 06 | Documentação |
| 07 | Fabricação |
| 08 | Construção 4D 5D |
| 09 | Construção Logística |
| 10 | Operação e Manutenção |
| 11 | Demolição |
| centro | O que é BIM? (Vantagens) |

## Comportamento das animações

- **Etapas 01 a 05** — o menu sai arrastando para a **direita** e a arte entra pela esquerda.
- **Etapas 06 a 11** — o menu sai arrastando para a **esquerda** e a arte entra pela direita.
- **Retorno** — ao clicar no ícone da Quadoo, a arte sai pelo mesmo lado por onde entrou e o menu reaparece.

O fundo é preto em todas as telas. A legenda "Para retornar ao menu / clique no ícone da quadoo" aparece apenas no menu inicial, no canto inferior esquerdo, e some suavemente durante a navegação.

## Estrutura interna

O código está organizado em três blocos dentro do `<head>`/`<body>`:

1. **CSS** — define o fundo preto, o posicionamento do menu, os destaques dos botões (`.hot`), o botão central (`#bimHot`), as telas de etapa (`#slideWrap`), as zonas de retorno (`.retZone`) e a legenda (`#menuNote`).
2. **`const IMG`** — objeto JavaScript com todas as imagens em base64 (`menu`, `bim`, `s01`…`s11`).
3. **Lógica** — monta os botões a partir do array `HOTS`, liga cada número à sua arte pelo objeto `SLIDES`, e controla as animações (`openSlide`, `openBIM`, `showMenu`).

## Personalização

### Trocar uma arte

As imagens ficam dentro de `const IMG = { ... }`, identificadas por chave (`s01` a `s11`, `bim`, `menu`). Para substituir uma arte, gere o novo PNG em base64 (formato `data:image/png;base64,...`) e troque o valor da chave correspondente. O ideal é regerar o arquivo a partir dos PNGs originais, mantendo fundo transparente para combinar com o fundo preto.

### Ajustar a posição de um botão do menu

As coordenadas dos números ficam no array `HOTS`, em porcentagem relativa à imagem do menu:

```js
{n:'01', x:29.6, y:72.5}
```

`x` é a posição horizontal e `y` a vertical (ambas em %). Aumentar `x` move para a direita; aumentar `y` move para baixo.

### Ajustar a zona de retorno de uma etapa

No objeto `SLIDES`, cada etapa indica de que lado fica o ícone da Quadoo na arte (`side: 'right'` ou `side: 'left'`), o que define onde a área clicável de retorno é colocada.

### Cores e tempo de animação

No início do CSS, em `:root`:

- `--pink` e `--cyan` — cores da marca.
- `--dur` — duração da animação de arraste (padrão `.62s`).
- `--ease` — curva de aceleração da animação.

## Compatibilidade

Usa recursos modernos de CSS (`aspect-ratio`, `clip-path`, funções `max()`/`calc()`). Recomendado em versões atuais de Chrome, Edge, Firefox e Safari. Como tudo está embutido, não há requisitos de servidor.
