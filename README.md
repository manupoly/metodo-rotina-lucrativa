# Método Rotina Lucrativa — Landing Page

Landing page estática do curso **Método Rotina Lucrativa**: um único `index.html` com HTML, CSS e JS inline, sem build e sem dependências além das fontes do Google.

## O que a página vende

Seis módulos, na ordem em que aparecem no acordeão da seção 04:

| | módulo |
| --- | --- |
| 01 | Cadastro: entre na plataforma no primeiro dia |
| 02 | Como ajustar o kit de gravação |
| 03 | Grave dentro dos requisitos |
| 04 | O que a plataforma não permite gravar |
| 05 | Como funciona o app onde você grava |
| 06 | Do envio ao saque no Pix |

Se o conteúdo do curso mudar, esta lista, o acordeão e a lista de inclusos da oferta (`.inc`) mudam junto — a página não pode prometer módulo que não existe. Hoje a oferta ainda inclui **"Checklist de pré-envio"**, que era o entregável de um módulo que saiu: confirme se ele continua existindo como material de apoio ou tire da oferta.

A descrição do módulo 05 foi escrita por dedução sobre como um app desse tipo funciona, não a partir do app real — revise antes de rodar tráfego.

Duas coisas que o texto **não** pode voltar a dizer, porque são falsas sobre como a plataforma funciona:

- que existe escolher a tarefa certa, ou que umas tarefas pagam mais que outras — **toda tarefa da rotina pode virar hora paga**;
- qualquer promessa de valor mensal, e qualquer preço riscado que nunca foi cobrado.

O eixo do texto é **requisito de aprovação**, nunca reprovação. Palavras como "rejeitado", "recusado" e "reprovado" foram removidas de propósito.

## Cores

Dois tokens de verde, e a diferença entre eles não é estética:

| token | valor | uso |
| --- | --- | --- |
| `--acc` | `#0fd96b` | **preenchimento** — botão, barra, ponto. Nunca texto sobre papel: dá 1,70:1. |
| `--acc-txt` | `#0b7a44` | **texto** verde sobre papel (4,87:1). Vira `--acc` dentro de superfície escura. |
| `--acc-on` | `#141414` | texto **por cima** do verde (9,79:1). |

Toda superfície escura precisa estar no seletor que remapeia `--acc-txt` (logo abaixo do `:root`). Painel escuro que ficar de fora herda o verde de papel sobre preto e sai a 3,4:1.

## Marca

| arquivo | onde usar |
| --- | --- |
| `icone-rotina-lucrativa.svg` | figura em tinta escura — **fundo claro** |
| `icone-rotina-lucrativa-dark.svg` | figura clara — **fundo escuro** (cabeçalho e rodapé) |
| `rotina-lucrativa-lockup-dark.png` | lockup com fundo chapado — só para `og:image` |
| `favicon.svg` | o mesmo boneco sobre pastilha escura, com contraluz verde |
| `favicon-32.png` | o `favicon.svg` rasterizado — **fallback** de aba |

Trocar uma variante do ícone pela outra faz a marca sumir dentro do fundo. O `favicon.svg` repete as formas do `-dark`: se o logo mudar, é aquele bloco de formas que precisa ser atualizado junto.

O `favicon-32.png` existe porque SVG como favicon não funciona no Safari abaixo do 16 nem em navegadores antigos — sem ele, esse grupo pede `/favicon.ico`, não encontra e mostra ícone genérico. Ele é **derivado** do `favicon.svg`: mudou o logo, precisa regerar os dois. Não há rasterizador no projeto; o PNG foi gerado desenhando o SVG num `<canvas>` e exportando com `toDataURL`.

A pastilha escura do favicon não é decoração — a figura é clara, e sem ela o ícone desapareceria numa barra de abas branca.

## A seção "O mercado"

Substituiu a faixa rolante de cidades e tarefas. É montada pelo JS a partir de `CONFIG.mercado`, uma lista de cards:

```js
mercado: [
  { tipo:"video",   url:"dQw4w9WgXcQ",   titulo:"…", fonte:"Canal da empresa", data:"2026" },
  { tipo:"noticia", url:"https://…",     titulo:"…", fonte:"Reuters", data:"mar/2026", resumo:"…" },
],
```

`tipo:"video"` abre o player dentro do próprio card ao clicar — nada é carregado antes disso, então dez cards não custam dez players. A `url` aceita ID do YouTube, link do YouTube/Vimeo ou arquivo de vídeo, pelo mesmo parser que o vídeo do topo usa.

`tipo:"noticia"` transforma o card inteiro em link e abre em outra aba.

**Com a lista vazia, a seção se remove do DOM.** É proposital: moldura vazia converte pior que seção ausente — a mesma lição da seção 00. Só entre com reportagem de veículo identificável e com data; notícia sem fonte enfraquece em vez de provar.

## Como editar

Todo o conteúdo variável (link de checkout, vídeo, preço, rodapé legal) está centralizado no bloco `CONFIG`, no final do `index.html`. Procure por `⬅️ TROCAR` para achar o que ainda falta preencher:

```js
const CONFIG = {
  checkoutUrl: "",   // URL do checkout (Kiwify, Hotmart, Eduzz, Cakto, Kirvano, Stripe)
  videoEmbed:  "",   // ID ou link do YouTube/Vimeo, ou arquivo .mp4 local
  price:       "25", // só o número, sem "R$"
  legal:       "...",
  supportUrl:  "",
  termsUrl:    "",
  privacyUrl:  "",
};
```

Pendências antes de rodar tráfego pago:

- [ ] `checkoutUrl` — sem ele os botões de compra ficam inativos
- [ ] `videoEmbed` — vídeo do topo
- [ ] **Seção 00** — os seis depoimentos e os quatro prints ainda são de exemplo, e o aviso interno sobre isso **renderiza para o visitante**. Depoimento inventado é propaganda enganosa (CDC art. 37). Sem material real e autorizado, apague a seção inteira e deixe a página começar na 01.
- [ ] Dados legais no rodapé: `legal`, `supportUrl`, `termsUrl`, `privacyUrl` — hoje a página promete devolução em 7 dias ao lado de links vazios

## Rodar localmente

Basta abrir o `index.html` no navegador. Para servir por HTTP:

```bash
python -m http.server 8000
```

## Publicação

Hospedado via GitHub Pages a partir da branch `main`, raiz do repositório. O `.nojekyll` desativa o processamento Jekyll — sem ele o Pages ignora arquivos iniciados com `_`.
