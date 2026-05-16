# CLAUDE.md

## Visão geral

Site institucional de página única (landing page) da **ZENIT — Agência & Hub de Marketing Digital**. Publicado via GitHub Pages em `agenciazenite.github.io`. Sem framework, sem build, sem dependências locais — tudo em um único arquivo `index.html`.

## Estrutura do projeto

```
agenciazenite.github.io/
├── index.html   ← único arquivo de código (HTML + CSS + JS inline)
└── CLAUDE.md
```

## Stack

- HTML5 semântico em português (`lang="pt-BR"`)
- CSS puro inline no `<style>` do `<head>` (sem Sass, Tailwind ou outra abstração)
- JavaScript vanilla inline no `<script>` no final do `<body>`
- Google Fonts (DM Serif Display, DM Sans, Questrial) via CDN

## Arquitetura do index.html

O arquivo é organizado em blocos comentados com `═══`:

| Bloco | ID/elemento | Descrição |
|---|---|---|
| NAV | `<nav>` | Barra fixa com logo SVG, links âncora e botão WhatsApp |
| HERO | `#hero` | Grid 2 colunas — copy + phone mockup animado |
| O QUE FAZEMOS | `#sobre` | Grid 2 colunas — texto + lista glassmorphism |
| SERVIÇOS | `#servicos` | Grid 3 colunas de cards de serviço |
| COMO FUNCIONA | `#jornada` | Grid 2 colunas de steps numerados |
| EQUIPE | `#equipe` | Grid 2 colunas — texto + placeholder de foto |
| CONTATO | `#contato` | Grid 2 colunas — info + formulário (sem backend) |
| FOOTER | `<footer>` | Logo, links âncora e redes sociais |
| WA FLOAT | `.wa-float` | Botão flutuante WhatsApp (fixo, canto inferior direito) |

## Design tokens (CSS custom properties em `:root`)

```css
--black:       #080B14   /* fundo principal */
--white:       #FFFFFF
--muted:       rgba(255,255,255,0.52)  /* texto secundário */
--card-bg:     rgba(255,255,255,0.04)
--card-border: rgba(255,255,255,0.09)
--accent:      #3B82F6   /* azul principal */
--accent-deep: #1D4ED8
--accent-light:#60A5FA
--accent-glow: rgba(59,130,246,0.22)
--grd:         linear-gradient(135deg, #3B82F6, #6366F1)  /* botões CTA */
--grd-text:    linear-gradient(135deg, #60A5FA, #818CF8)  /* texto destaque */
--serif:       'DM Serif Display', Georgia, serif
--sans:        'Questrial', 'DM Sans', system-ui, sans-serif
```

## Convenções de componentes

**Glassmorphism (`.glass`):** `background: var(--card-bg)` + `border: 1px solid var(--card-border)` + `backdrop-filter: blur(16px)` + `border-radius: 20px`.

**Blobs ambientais (`.blob`):** `<div>` com `position:absolute`, `border-radius:50%`, `filter:blur(90px)` e `pointer-events:none`. Não interferem no layout.

**Botões:** `.btn` é a base. Variantes: `.btn-orange` (gradiente CTA principal), `.btn-ghost` (transparente com borda), `.btn-wa-nav` (nav WhatsApp).

**Tipografia de destaque:** `.accent-orange` aplica `var(--grd-text)` com clip para criar texto gradiente.

**Logo:** SVG inline com `linearGradient` e id `rktGrd` (nav) / `rktGrd2` (footer). Não use o mesmo id em ambos ou haverá conflito de renderização.

## Responsividade

Um único breakpoint em `860px`. Abaixo dele:
- Grids 2-3 colunas viram 1 coluna
- `.hero-visual` (phone mockup) fica oculto
- `.nav-links` e `.footer-links` ficam ocultos

## JavaScript

Apenas um listener de scroll que destaca o link ativo na nav comparando `window.scrollY` com `offsetTop - 140` de cada `section[id]`.

## Formulário de contato

O `<form>` tem `onsubmit="return false;"` — sem backend conectado. Para ativar o envio, integrar com Netlify Forms, Formspree ou similar substituindo esse atributo.

## Informações de contato (placeholders)

Os dados abaixo são placeholders e devem ser substituídos pelos reais antes de ir para produção:
- WhatsApp: `5511999999999`
- E-mail: `contato@agenciazenit.com.br`
- Instagram: `@agenciazenit`

## Deploy

GitHub Pages publica automaticamente o branch `main`. Não há etapa de build. Para ver o resultado basta abrir `index.html` no browser ou fazer push para `main`.

## Fluxo de trabalho

1. Edite `index.html` diretamente
2. Abra no browser para validar visualmente (sem servidor necessário)
3. Verifique responsividade redimensionando para < 860px
4. Commit e push para `main` — o deploy é imediato via GitHub Pages
