# Ana Paula Estética — link da bio

Página de links para o Instagram [@aanapaulaestetica](https://instagram.com/aanapaulaestetica).

**Produção:** https://bio.aanapaulaestetica.com.br
**Site institucional:** https://aanapaulaestetica.com.br

---

## Publicação

Hospedado na **Cloudflare Pages**, projeto `ana-paula-linkbio`.
Migrado do GitHub Pages em 22/08/2026.

O projeto usa **upload direto**, então `git push` não republica sozinho.
Para publicar uma alteração:

```bash
npx wrangler@4 pages deploy . \
  --project-name ana-paula-linkbio \
  --branch main --commit-dirty=true
```

> O arquivo `CNAME` na raiz é resquício do GitHub Pages e não tem mais efeito.
> O roteamento hoje é feito pelo registro `bio` na zona da Cloudflare, que
> aponta para o projeto do Pages com o proxy ligado.

---

## Rodar localmente

```bash
python -m http.server 8000
```

---

## Estrutura

```
index.html        página inteira: HTML, CSS e JS num arquivo só (45 KB)
assets/img/       imagens em WebP com fallback JPG
  og-capa.jpg     cartão 1200x630 da prévia de compartilhamento
logo-transparente.png
```

### Sobre o peso

As imagens estavam embutidas em base64 dentro do HTML, que pesava **2,02 MB**.
Foram extraídas para arquivos e o documento caiu para **45 KB**. As fotos de
antes e depois carregam sob demanda com `loading="lazy"`.

**Ao adicionar uma foto nova, não volte a embutir em base64.** Salve em
`assets/img/` como WebP (qualidade 80, largura máxima 1000px) com um `.jpg`
irmão de fallback, e referencie pelo caminho.

---

## Onde mexer no conteúdo

Contatos e links ficam centralizados num objeto `CONFIG` no início do
`<script>`, no fim do `index.html`:

```js
const CONFIG = {
  whatsapp: "5561993699986",
  whatsappMsg: "...",
  instagram: "https://instagram.com/aanapaulaestetica",
  site: "https://aanapaulaestetica.com.br",
  maps: "..."
};
```

### Dados que precisam bater com o site e com o Google

Nome, endereço e telefone são cruzados pelo Google entre todas as páginas.
Divergência derruba o ranqueamento local. Mantenha idêntico nos três lugares:

```
Ana Paula Estética
Quadra 2, Lote 2/6, Loja 4 · Setor Central, Gama - DF, 72405-020
(61) 99369-9986
Terça a sábado, com hora marcada
```
