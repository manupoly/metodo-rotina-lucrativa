# Filmou / Ganhou — Landing Page

Landing page estática do curso **Filmou / Ganhou**: um único `index.html` com HTML, CSS e JS inline, sem build e sem dependências além das fontes do Google.

## Cores

Dois tokens de verde, e a diferença entre eles não é estética:

| token | valor | uso |
| --- | --- | --- |
| `--acc` | `#0fd96b` | **preenchimento** — botão, barra, ponto. Nunca texto sobre papel: dá 1,70:1. |
| `--acc-txt` | `#0b7a44` | **texto** verde sobre papel (4,87:1). Vira `--acc` dentro de superfície escura. |
| `--acc-on` | `#141414` | texto **por cima** do verde (9,79:1). |

Toda superfície escura precisa estar no seletor que remapeia `--acc-txt` (logo abaixo do `:root`). Painel escuro que ficar de fora herda o verde de papel sobre preto e sai a 3,4:1.

## Ícone da aba

`favicon.svg` — nota de dólar verde acesa sobre pastilha escura. A pastilha não é decoração: sem ela o halo verde desaparece numa barra de abas clara. É SVG, então escala sem perder nitidez; navegadores muito antigos simplesmente não mostram ícone nenhum, sem quebrar nada.

Para mudar a cor, são dois valores no arquivo: `#0fd96b` no corpo da nota e `#0b7a44` nos traços.

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
- [ ] Depoimentos e prints marcados com `⬅️ TROCAR` (usar material **real**, com autorização)
- [ ] Dados legais no rodapé: `legal`, `supportUrl`, `termsUrl`, `privacyUrl`

## Rodar localmente

Basta abrir o `index.html` no navegador. Para servir por HTTP:

```bash
python -m http.server 8000
```

## Publicação

Hospedado via GitHub Pages a partir da branch `main`, raiz do repositório. O `.nojekyll` desativa o processamento Jekyll — sem ele o Pages ignora arquivos iniciados com `_`.
