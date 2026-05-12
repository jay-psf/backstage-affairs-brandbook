# Merge Pack — Backstage Affairs Brand Hub

Pacote para **mesclar** com o repositório existente `jay-psf/backstage-affairs-brandbook`. NÃO sobrescreve o `index.html` nem o `brand-guidelines.md` que já estão lá — apenas adiciona o que falta.

## O que tem neste pacote

```
brand-merge/
├── llms.txt                                # NOVO — endpoint pra IAs
├── vercel.json                             # SUBSTITUI o atual (versão melhorada com CORS)
├── PATCH-index-html.txt                    # Bloco HTML pra colar dentro do index.html existente
├── assets/
│   └── logos/
│       ├── horizontal/                     # 4 PNGs
│       ├── monogram/                       # 4 PNGs
│       └── stacked/                        # 4 PNGs
└── downloads/
    └── backstage-affairs-brand-kit.zip     # Pacote ZIP com os 12 logos
```

## Passo a passo do merge

### Etapa 1 — Subir os arquivos NOVOS (não conflitam)

No GitHub web, no repo `backstage-affairs-brandbook`:

1. Clica em **Add file** → **Upload files**
2. Arrasta de uma vez:
   - O arquivo `llms.txt`
   - A pasta `assets/` inteira (com as 3 subpastas)
   - A pasta `downloads/` inteira (com o ZIP)
3. No campo de commit: `add: PNG assets, llms.txt e downloads`
4. **Commit changes**

### Etapa 2 — Substituir o `vercel.json`

1. No repo, clica em `vercel.json` (o arquivo existente)
2. Clica no ícone de **lápis** (edit) no canto superior direito
3. **Apaga todo o conteúdo** atual
4. **Cola o conteúdo** do `vercel.json` deste pacote
5. Embaixo: commit message `update: vercel.json com CORS pros assets`
6. **Commit changes**

### Etapa 3 — Adicionar o patch no `index.html`

Esta é a etapa mais delicada. **Antes de mexer, faz uma cópia de segurança:**

1. Abre o `index.html` no repo
2. Clica em **Raw** (botão no topo direito do código)
3. **Salva o conteúdo todo** num arquivo `.html` no teu computador como backup (Ctrl+S no Chrome funciona)

Agora o merge:

1. Volta no `index.html` no GitHub e clica no **lápis** pra editar
2. Procura por uma dessas referências (Ctrl+F):
   - `<section class="section" id="arquivos">` — se existir essa seção, posiciona o cursor ANTES dela
   - Se não existir, procura por `<!-- VOZ` ou `<section class="section" id="voz"` — posiciona ANTES disso
   - Se ainda não achar, procura por `<footer` — posiciona ANTES
3. Abre o arquivo `PATCH-index-html.txt` deste pacote
4. **Copia tudo** entre os marcadores `<!-- INÍCIO DO PATCH -->` e `<!-- FIM DO PATCH -->`
5. **Cola** na posição que você marcou no index.html
6. Embaixo: commit message `add: seção 07 Arquivos e 08 Para IAs`
7. **Commit changes**

### Etapa 4 — Deploy na Vercel

Se você ainda não conectou o repo à Vercel:

1. Acessa **vercel.com/new**
2. Importa o repo `backstage-affairs-brandbook`
3. Na configuração:
   - **Framework Preset:** `Other`
   - **Root Directory:** deixa vazio
   - **Build Command:** deixa vazio
   - **Output Directory:** deixa vazio (raiz do repo)
4. **Deploy**

Se já estiver conectado: cada commit no GitHub redeploya automaticamente em ~30 segundos.

### Etapa 5 — Domínio `brand.backstageaffairs.com`

Vou repetir do passo anterior pra ter aqui consolidado:

1. No projeto Vercel → **Settings** → **Domains**
2. Adiciona `brand.backstageaffairs.com`
3. No GoDaddy → DNS do `backstageaffairs.com`:
   - Type: **CNAME**
   - Name: **brand**
   - Value: **cname.vercel-dns.com**
   - TTL: 1 hour
4. Aguarda propagação (5-30 min)

## Verificações pós-deploy

Abre cada URL no navegador e confirma que carrega:

- [ ] https://brand.backstageaffairs.com — site abre com hero animado
- [ ] https://brand.backstageaffairs.com/assets/logos/horizontal/blur-white.png — PNG aparece
- [ ] https://brand.backstageaffairs.com/downloads/backstage-affairs-brand-kit.zip — baixa o ZIP
- [ ] https://brand.backstageaffairs.com/llms.txt — abre como texto plano
- [ ] https://brand.backstageaffairs.com/brand-guidelines.md — abre o markdown
- [ ] As 12 imagens aparecem na seção "Arquivos" do site

## Importante sobre o repo existente

O `index.html` que tá no repo é **excelente** — sistema de 3 modos do logo, animação por letra, paleta LED, matriz de decisão. Tudo isso fica preservado. O patch só adiciona:

- **Seção 07 — Arquivos:** botões reais de download das 12 PNGs (porque o HTML atual só simula com CSS, não tinha como o usuário baixar um arquivo de verdade)
- **Seção 08 — Para IAs:** card destacando o `llms.txt` como endpoint pra LLMs

O `brand-guidelines.md` também fica intocado — é a documentação técnica completa e o `llms.txt` referencia ele.

## Em caso de dúvida

Se algo der errado no patch do `index.html`, é só restaurar o backup que você salvou. O GitHub também permite reverter qualquer commit pela aba **History**.
