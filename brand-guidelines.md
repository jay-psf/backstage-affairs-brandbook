# Backstage Affairs — Brand Guidelines
**Versão 3.1 · Abril 2026**

---

## 1. Sobre a Marca

**Backstage Affairs** é uma empresa de produção e gerenciamento de eventos ao vivo. O nome carrega a dualidade entre o que acontece nos bastidores (Backstage) e a condução estratégica dos assuntos (Affairs). Essa dualidade é o núcleo visual da identidade.

---

## 2. Regra de Ouro — Logo

> **BACKSTAGE** é intocável. **AFFAIRS** sempre recebe o tratamento de efeito.

Nunca separe as duas palavras com espaço ou hífen. `BACKSTAGE` é sempre uma palavra única.

| Elemento | Regra |
|---|---|
| BACKSTAGE | Sempre sólido, limpo, sem qualquer efeito |
| AFFAIRS | Sempre com efeito (blur para digital, striped para impresso) |
| Cor | Sempre monocromático — tudo branco ou tudo preto, nunca mistura |
| Separação | "back stage" ou "back-stage" é proibido em qualquer contexto |

---

## 3. Três Modos de Uso do Logo

### Modo 1 — Fog Animado ★ (Digital Primário)
- **Uso:** Websites, apps, HTML, vídeo-intro, apresentações interativas
- **Regra:** Sempre preferir este modo sobre os demais em contextos digitais com suporte a CSS animation
- **Técnica:** Cada letra de AFFAIRS anima individualmente com blur oscilante
- **Cor:** Branco em fundo preto (nunca mistura de cores)

```css
/* Animação fog — letra por letra */
@keyframes ba-fog {
  0%, 100% {
    filter: blur(0.05em);
    text-shadow: 0 0 0.5em rgba(255,255,255,.28), 0 0 1em rgba(255,255,255,.12);
  }
  50% {
    filter: blur(0.085em);
    text-shadow: 0 0 0.7em rgba(255,255,255,.44), 0 0 1.4em rgba(255,255,255,.2);
  }
}

/* Hero/destaque — blur fixo em px (não escala com fonte) */
@keyframes ba-fog-hero {
  0%, 100% { filter: blur(2px); }
  50%       { filter: blur(3.5px); }
}
```

**HTML para AFFAIRS animado:**
```html
<span class="ba-fog">
  <span class="ba-fog-l">A</span>
  <span class="ba-fog-l">F</span>
  <span class="ba-fog-l">F</span>
  <span class="ba-fog-l">A</span>
  <span class="ba-fog-l">I</span>
  <span class="ba-fog-l">R</span>
  <span class="ba-fog-l">S</span>
</span>
```

---

### Modo 2 — Blur Estático (Digital Secundário)
- **Uso:** PowerPoint, Google Slides, imagens estáticas para redes sociais, PDF digital
- **Regra:** Usar quando animação CSS não é possível
- **Técnica:** Gaussian blur de 20–30% aplicado somente em AFFAIRS
- **Cor:** Branco em fundo escuro, ou preto em fundo claro — sem mistura

```css
/* Blur estático em AFFAIRS */
.affairs-blur {
  filter: blur(1.2px);
  text-shadow: 0 0 8px rgba(255,255,255,0.3);
}
```

---

### Modo 3 — Striped (Impresso Apenas)
- **Uso:** Contratos, crachás, camisetas, sinalização física, papelaria impressa
- **Regra:** ⛔ NUNCA usar em telas — proibido em site, app, PPT, redes sociais, e-mail
- **Técnica:** Linhas horizontais finas cortando as letras de AFFAIRS (arquivo vetorial SVG/PDF)
- **Proporção das listras:** aprox. 75% sólido + 25% gap (3:1)

```css
/* Simulação CSS — apenas para mockups internos, NÃO para produção digital */
.affairs-striped {
  background: repeating-linear-gradient(
    0deg,
    currentColor 0,
    currentColor 3px,
    transparent 3px,
    transparent 4px
  );
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
}
```

---

## 4. Arquivos de Logo

### Formatos disponíveis

| Arquivo | Uso | Formato |
|---|---|---|
| `backstage_affairs_stacked_striped_white.svg` | Impresso, fundo escuro | SVG + PDF |
| `backstage_affairs_stacked_striped_black.svg` | Impresso, fundo claro | SVG + PDF |
| `backstage_affairs_horizontal_striped_white.svg` | Impresso horizontal, fundo escuro | SVG + PDF |
| `backstage_affairs_horizontal_striped_black.svg` | Impresso horizontal, fundo claro | SVG + PDF |

**Para arquivos digitais (blur/fog):** não existe arquivo exportado — o efeito é sempre gerado por CSS animation em HTML, ou aplicado manualmente em software (Photoshop, After Effects) para exportações estáticas.

### Formato para envio/colaboração
- **Para impressão/produção:** SVG ou PDF (vetorial)
- **Para compartilhar com IA ou em ferramentas digitais:** PNG em alta resolução (mín. 1600px de largura, fundo incluído)
- **Para HTML/web:** CSS animation (não usar imagem)

---

## 5. Layouts do Logo

### Stacked (Empilhado)
BACKSTAGE na linha superior, AFFAIRS na linha inferior. AFFAIRS aumenta de tamanho até que sua largura iguale exatamente a de BACKSTAGE. Ambas as palavras ficam alinhadas pelas bordas esquerda e direita.

```
BACKSTAGE    ← tamanho base
AFFAIRS      ← fonte ~29% maior que BACKSTAGE para igualar largura
```

**Implementação CSS + JS:**
```javascript
// Sincroniza largura de AFFAIRS com BACKSTAGE em tempo real
function syncStackedLogo(backEl, affEl) {
  const targetW = backEl.offsetWidth;
  const base = parseFloat(getComputedStyle(backEl).fontSize) || 20;
  affEl.style.fontSize = base + 'px';
  const baseW = affEl.offsetWidth;
  if (baseW > 0) affEl.style.fontSize = (base * (targetW / baseW)) + 'px';
}
```

### Horizontal (Em Linha)
BACKSTAGE e AFFAIRS lado a lado, com espaço entre as palavras. Mesmo tamanho de fonte para ambas as palavras.

```
BACKSTAGE AFFAIRS    ← mesmo tamanho de fonte
```

---

## 6. Monograma BA

O monograma segue a mesma regra do logo completo:

| Letra | Regra |
|---|---|
| **B** | Sempre sólido, sem qualquer efeito |
| **A** | Sempre com efeito (blur animado para digital, striped para impresso) |

---

## 7. Sistema de Cores

| Token | Hex | Uso |
|---|---|---|
| `--black` | `#000000` | Fundo principal, máxima profundidade |
| `--white` | `#FFFFFF` | Texto principal, logo em fundo escuro |
| `--copper` | `#B87333` | Cor de destaque, acentos, links ativos |
| `--blue` | `#2B4A6F` | Cor secundária de destaque |
| `--gray-s` | `#999999` | Texto secundário |

**LED / Status:**

| Token | Hex | Uso |
|---|---|---|
| `--led-red` | `#FF3366` | Erros, proibições, alertas críticos |
| `--led-green` | `#00FF88` | Correto, aprovado |
| `--led-amber` | `#FFB800` | Atenção, cuidado |
| `--led-blue` | `#00AAFF` | Informação |

**Escala de cinza:**

| Token | Hex |
|---|---|
| `--g3` | `#1a1a1a` |
| `--g4` | `#2a2a2a` |
| `--g5` | `#3a3a3a` |
| `--g6` | `#666666` |
| `--g7` | `#888888` |

---

## 8. Tipografia

**Família:** Roboto Condensed (Google Fonts)

```html
<link href="https://fonts.googleapis.com/css2?family=Roboto+Condensed:wght@400;500;600;700&display=swap" rel="stylesheet">
```

| Peso | Valor | Uso |
|---|---|---|
| Regular | 400 | Corpo de texto, parágrafos |
| Medium | 500 | Labels, legendas, navegação |
| SemiBold | 600 | Subtítulos, destaques |
| Bold | 700 | Headings, logotipo, CTAs |

**Proibido:** pesos 300 (Light) e 900 (Black) — nunca usar.

**Hierarquia:**

| Nível | Tamanho | Peso | Uso |
|---|---|---|---|
| Hero | 72–120px | 700 | Logotipo hero |
| H1 | 40–56px | 700 | Títulos de seção |
| H2 | 28–36px | 700 | Subtítulos |
| H3 | 20–24px | 600 | Títulos de card |
| Body | 14–16px | 400 | Texto corrido |
| Caption | 10–12px | 500 | Labels, legendas |
| Overline | 9–11px | 700 | Categorias (letter-spacing: .12em) |

---

## 9. Espaço de Segurança (Clear Space)

O espaço mínimo ao redor do logo em todas as direções:
- **Digital:** 200px
- **Impresso:** 50mm

---

## 10. Tamanhos Mínimos

| Contexto | Tamanho mínimo |
|---|---|
| Digital | 120px de largura |
| Impresso | 30mm de largura |

---

## 11. Uso Proibido

- ❌ Separar "BACKSTAGE" como "back stage" ou "back-stage"
- ❌ Aplicar qualquer efeito em BACKSTAGE (blur, sombra, gradiente, distorção)
- ❌ Misturar cores no logo (ex: BACKSTAGE branco + AFFAIRS cobre)
- ❌ Usar o logo Striped em qualquer contexto digital (tela, PPT, redes sociais)
- ❌ Usar versões coloridas do logo (apenas preto ou branco)
- ❌ Rotacionar, inclinar ou deformar o logo
- ❌ Aplicar outline/contorno nas letras
- ❌ Usar fundos que não sejam preto ou branco para o logo

---

## 12. Matriz de Decisão — Qual modo usar?

| Contexto | Modo correto |
|---|---|
| Website / HTML / App | ★ Modo 1 — Fog Animado |
| Vídeo / Motion / Reels | ★ Modo 1 — Fog Animado |
| PPT / Google Slides | Modo 2 — Blur Estático |
| Social Media (imagem estática) | Modo 2 — Blur Estático |
| PDF Digital | Modo 2 — Blur Estático |
| Contrato / Proposta impressa | Modo 3 — Striped |
| Crachás / Camisetas / Merch | Modo 3 — Striped |
| Sinalização física / Banner | Modo 3 — Striped |

---

## 13. Voz e Tom da Marca

A Backstage Affairs comunica com precisão técnica e postura executiva. Nunca informal demais, nunca distante.

**Princípios de comunicação:**
- Clareza antes de estética — nunca sacrificar entendimento por elegância
- Autoridade sem arrogância — sabemos o que fazemos, mas não precisamos anunciar
- Bastidores visíveis — transparência sobre processo e metodologia é parte da marca
- Precisão nos números — dados e métricas sempre que possível

---

*Backstage Affairs Brand System · Versão 3.1 · Abril 2026*
