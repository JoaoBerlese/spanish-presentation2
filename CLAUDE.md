# CLAUDE.md — Regras para construir esta apresentação

> **Regras permanentes** para o agente (Claude Code). Evitam *drift* ao longo de
> muitas iterações. O *quê* está em `IDEA.md`; aqui vai o *como*.

## Idioma
- **Espanhol só no que é apresentação**: slides, presenter notes e `guion/guion.md`.
- **Português em todo o resto**: `README.md`, `IDEA.md`, este arquivo, `research/*`,
  comentários dos scripts em `bin/` e mensagens de commit.

## Voz (no conteúdo em espanhol)
- Registro **rioplatense**: voseo ("vos", "tenés", "¿te animás?"), natural e próximo.
- Nível acessível (~B1): frases curtas; presente, pretéritos e um ou outro
  condicional. Nada rebuscado.
- Tom **divertido e curioso**, nunca corporativo.
- Passada "humanizadora" em todo texto novo: tem que soar **falado**, não traduzido
  nem polido por IA.

## Regras dos slides
- **Máximo ~20 palavras por slide.** O resto se fala e vai no roteiro.
- Estética Presentation Zen: um título forte + um apoio visual (foto ou emoji).
- Cada slide é um bloco separado por `---` em `slides/la-paz.md`.
- Classes do tema (ver `themes/lapaz.css`): `title`, `curioso`, `center`, `ficha`,
  `foto-hero`, `obra-hero`, `dramatico`, `juega`, `cierre`.
- Presenter notes no fim de cada slide, em `<!-- ... -->`, começando com
  `Restan: ~MM:SS (Ds)` (tempo restante dos 5:00 + duração do slide). Bullets curtos:
  dicas de palco, não um segundo roteiro.

## Sincronização (regra de ouro do método)
Quando o conteúdo muda, mexem JUNTOS:
- `slides/la-paz.md` (o que se vê)
- `guion/guion.md` (o que se fala)
- as presenter notes do slide (sinais de palco e tempo)
Mexeu em um, revise os outros dois. Mudou a ordem/quantidade de slides → recalcular
todos os `Restan:`.

## Dados: nada de inventar
- Fatos (datas, números, nomes) saem de `research/fuentes.md`. Se não estiver lá,
  pesquisar e citar antes de colocar num slide.
- Números que variam entre fontes → arredondar com honestidade ("más de 3.600 m",
  "más de 30 km").
- Lendas são ditas como lenda ("dicen que…"): origem do bombín, chapéu reto = casada, Armstrong.
- La Paz é **sede de gobierno**; a capital constitucional é **Sucre**. Nunca escrever
  "capital más alta del mundo" sem esse contexto.

## Build e validação
- Pré-visualizar: `bin/serve` → servidor local com o deck.
- Exportar: `bin/build` → HTML, PDF e PPTX em `build/`.
- O PDF é mais rígido que o HTML: refazer o build e conferir depois de qualquer
  mudança de layout. Preferir flex a grid.
- Revisão visual: exportar PNG por slide
  (`npx @marp-team/marp-cli@4.5.1 slides/la-paz.md --images png --allow-local-files -o <tmp>/s.png </dev/null`)
  e olhar cada imagem (corte de texto, contraste, enquadramento).
- Node 24 + Marp CLI 4.5.1 (fixado nos scripts, via `npx`). Node 25 quebra o Marp.
- **Sempre** chamar o Marp com `</dev/null`: se o stdin não for um terminal (pipe,
  agente, CI), ele fica esperando Markdown pelo stdin e trava para sempre.
- O usuário abre o PDF no **Visualizador de Documentos (Evince/poppler)**, não só
  no Chrome. Conferir também com `pdftocairo -png build/la-paz.pdf <tmp>/c`.
- **Escurecimento sobre foto = PNG** (`assets/scrim-*.png`, gerados por
  `bin/scrims`). Nunca `linear-gradient` com `rgba` sobre foto: no PDF o Evince
  desenha isso rosa ou não desenha.

## Imagens
- Ficam em `assets/`, nome `lapaz-<descricao>.jpg` (minúsculas, sem acento, com
  hífen); `.png` só para logos/transparência.
- Nada de imagem remota no deck: quebra PDF/PPTX.
- Toda imagem tem linha em `research/catalogo-imagenes.md` (origem, autor, licença,
  slide). Os créditos ficam **só no catálogo**: o usuário pediu para tirar a
  linha de créditos do slide de encerramento.
- `assets/scrim-*.png` não são fotos: são as camadas de escurecimento do tema.

## Commits
- Mensagens em português, uma mudança por commit quando for ajuste visual
  (ex.: `Slide "teleférico": cabine maior e painel à esquerda`).
