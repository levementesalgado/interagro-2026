# InterAgro 2026 — Site Estático

Site de divulgação e navegação no dia do evento **InterAgro 2026** ("Inteligência no
Campo"), realizado pela **FATEC Capão Bonito** (Centro Paula Souza), 21 a 23 de setembro
de 2026.

O site é **100% estático** (ou quase) — sem backend, sem banco de dados (ou quase), sem coleta de dados pessoais
(decisão da coordenação). HTML/CSS puro, sem framework, sem Tailwind.


## Identidade visual (segue `Grupo do Zap`)

Paleta de tokens (CSS em `assets/css/base.css`):

| Token | Cor | Uso |
|---|---|---|
| `--verde-agro` | `#2E7D32` | Primária: títulos, botões, destaque |
| `--verde-claro` | `#A5D6A7` | Fundos de seção, tag "PALESTRA" |
| `--terra` | `#8D6E63` | Secundária: detalhes, separadores |
| `--amarelo-sol` | `#F9A825` | CTA de ação (inscrição/vagas/contato) |
| `--quase-preto` | `#1B2A1B` | Texto principal |
| `--branco` | `#FFFFFF` | Fundo base |
| `--cinza-grama` | `#F1F5F1` | Fundo alternado de seções |
| `--perigo` | `#C62828` | Avisos urgentes |

- **Tipografia:** títulos em serifada (Georgia), corpo em sans system stack.
- **Logos obrigatórios:** FATEC, CPS e brasão aparecem na **tarja do rodapé** (footer) de
  toda página e na **tarja de patrocinadores** (`patrocinadores.html`). Arquivos em
  `assets/img/patrocinadores/instituicao-fatec.jpg`, `instituicao-cps.jpg`,
  `instituicao-brasao.jpg`.
- **Tags:** `PALESTRA` (verde-claro) e `OFICINA` (amarelo-sol).
- **Créditos/colaboradores:** a equipe de organização é listada no **rodapé** (ver
  `01_dados/equipe_organizacao.csv`): Adriano Daniel (Coordenação), Maria Renata
  (Conteúdo), Diego Guevara (Arte), Edil Queiroz (Design).

## Arquitetura e páginas (segue `Grupo do Zap` claro)

Sitemap multi-página estática (sem SPA, sem formulários):

| Página | Conteúdo |
|---|---|
| `index.html` | hero (nome + data + local + CTA), sobre, prévia da grade, destaques |
| `programacao.html` | grade por dia, com avisos de conflito (⚠) |
| `palestrantes.html` | 9 palestrantes (cards) |
| `oficinas.html` | 6 oficinas (cards) |
| `submeta-trabalho.html` | "Submeta seu Trabalho" / apresentação de trabalhos |
| `patrocinadores.html` | tarja com logos (instituições, patrocinadores, apoio) |
| `contato.html` | link de inscrição, Instagram, local |

Navegação global no header; rodapé com logos FATEC/CPS/brasão + créditos. Sem rotas
de admin e sem coleta de dados (restrição ambientaç (do coordenador;p)).

## Como montar cada parte

O conteúdo é **embutido direto no HTML** (sem `fetch`), então as páginas abrem em
`file://` e em qualquer hospedagem estática.

1. Edite as estruturas de dados no topo de `scripts/build_site.py`:
   - `SPEAKERS` — palestrantes/oficinas (nome, título, instituição, bio, dia, horário)
   - `PROGRAMA` — grade por dia (conflitos marcados com `flag`)
   - `PATROCINADORES` — logos por grupo (arquivos em `assets/img/patrocinadores/`)
2. Rode `python3 scripts/build_site.py` — gera os 7 HTML na raiz.
3. Ajuste a identidade em `assets/css/base.css` (tokens acima).
4. Imagens: `assets/img/patrocinadores/*.jpg` (logos) e `assets/img/palestrantes/`
   (coloque `P01.jpg`…`P15.jpg` para as fotos — os cards já referenciam esses nomes).

Alternativamente, a origem dos dados são os CSVs em `01_dados/` (palestrantes,
programação, equipe, requisitos) — revisados a partir do export completo do WhatsApp.

## Arquivos do repositório

```
interagro-2026/
├── index.html, programacao.html, palestrantes.html, oficinas.html,
│   submeta-trabalho.html, patrocinadores.html, contato.html
├── assets/
│   ├── css/base.css            # design system (tokens)
│   └── img/patrocinadores/     # logos FATEC/CPS/brasão + patrocinadores/apoio
├── 01_dados/                   # CSVs (fonte)
├── 02_descricoes/              # markdown de planejamento
├── 03_uml/                     # diagramas PlantUML
├── 04_ux_ui/                   # objetivos, sitemap, wireframes, design system
│
└── .nojekyll                  # GitHub Pages serve estático (sem Jekyll)
```

## Pendências (dependem da organização)

1. **Conflitos de horário** (⚠ na grade): 22/09 19h30 sobrepõe; 23/09 09h30 tem 4
   sessões simultâneas; 23/09 14h tem 3.
2. **Logos de patrocinadores**: nomes genéricos — confirmar qual é qual.
3. **Fotos dos palestrantes**: ainda não incluídas (todas) (`nome**.jpg`…`nome**.jpg`).
4. **Regras de submissão** (prazos, template) — a confirmar pela coordenação.
