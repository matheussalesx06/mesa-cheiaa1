# Mesa Cheia

Catálogo de jogos de tabuleiro para noites de jogatina. Atividade de Autoria Web (Semana 9, Flexbox).

**Público-alvo:** jovens e adultos que jogam em grupo e precisam escolher rápido o que jogar.

Estrutura: `index.html`, `style.css` e a pasta `capturas/` (coloque aqui as 3 imagens: `1280.png`, `768.png`, `360.png`).
Os cards usam blocos visuais com emoji (sem arquivos de imagem), então não há caminhos externos.

## Justificativa técnica

**1. Contêineres flex (seis ou mais, funções diferentes)**

| Seletor | Função | Eixo |
|---|---|---|
| `.header-inner` | cabeçalho | row |
| `.menu` | links do menu | row |
| `.hero-inner` | texto + bloco informativo | row + wrap |
| `.hero-info` | pilha de dados da apresentação | column |
| `.section-header` | título + contagem | row |
| `.cards` | coleção | row + wrap |
| `.card` / `.card-body` | conteúdo do card | column |
| `.card-visual` | centraliza o ícone | row |
| `.card-meta` | metadados | row |
| `.footer-inner` | rodapé | row + wrap |

- **Row:** em `.header-inner`, o eixo principal é horizontal. `justify-content: space-between` joga logo e menu para as pontas, e `align-items: center` os alinha na vertical.
- **Column:** em `.hero-info`, o eixo principal é vertical. `justify-content: center` centraliza o grupo na altura do bloco, e `align-items: center` centraliza cada item na horizontal.
- Outros valores usados: `justify-content: center` e `flex-end` (menu), `align-items: baseline`, `flex-start` e `stretch`.

**2. Gap, padding e ações na base dos cards**

- `gap`: `.cards` (20px entre cards), `.card` (14px), `.hero-inner`, `.menu`, `.footer-inner`.
- `padding`: `.card` (16px), `.container` (24px de cada lado), `.hero-info` (24px).
- Ações na base, sem altura fixa: `.cards` usa `align-items: stretch`, então os cards da linha têm a mesma altura. `.card` é uma coluna e `.card-body` tem `flex: 1 1 auto`, absorvendo a sobra de espaço e empurrando metadados e `.btn` para baixo.

**3. Cálculo em 1280 px**

- Largura interna do contêiner: 1100 − 2 × 24 = **1052 px**
- Gaps entre 3 cards: 2 × 20 = **40 px**
- Largura de cada card: (1052 − 40) / 3 ≈ **337,3 px**

A base de 300 px (`flex: 1 1 300px`) cabe 3 vezes em 1052 px (940 px), mas não 4 (1260 px). Em 768 px a área útil é 720 px: cabem 2 (620 px), não 3. Em 360 px é 312 px: cabe 1.

**4. Sétimo card**

> Preencha após o teste: ao duplicar um card, ele foi para a nova linha sozinho e, por causa de `flex-grow: 1`, ocupou toda a largura da linha (1052 px em 1280 px), ficando maior que os outros.

`justify-content: space-between` pode não alterar nada quando não sobra espaço livre na linha: por exemplo, quando os itens têm `flex-grow` e já preenchem toda a largura, ou quando a linha tem um único item.

## Testes (fazer no navegador)

1. **Três larguras:** use o modo responsivo do DevTools em 1280, 768 e 360 px e salve a captura da página inteira em `capturas/`.
2. **Conteúdo maior:** aumente um título e uma descrição e inclua uma palavra longa sem espaços; `overflow-wrap: anywhere` evita estouro e os botões seguem alinhados por linha.
3. **Sétimo card:** duplique um card, observe, anote acima e restaure os seis.
