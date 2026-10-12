# Apresentação "La Paz" 🏔️ — *apresentação como código*

Projeto de apresentação de espanhol (Fisk, Módulo 3) sobre **La Paz, Bolívia**,
construído no estilo **"presentation as code"** (inspirado no repositório
[tropicalruby-2026](https://github.com/akitaonrails/tropicalruby-2026) do Fábio Akita),
usando [Marp](https://marp.app): você escreve **Markdown** e gera **HTML, PDF e PPTX**.

Irmão do projeto anterior, "El Pato" (`../spanish-presentation`), com a mesma estrutura.

## Como funciona (o método)

O segredo é **separar responsabilidades** em arquivos, cada um com um papel:

| Arquivo | Papel |
|---|---|
| `IDEA.md` | O **brief**: objetivo, público, restrições, arco de slides. Escrito ANTES dos slides. |
| `CLAUDE.md` | As **regras** para o agente (idioma, tom, limite de texto, workflow). |
| `slides/la-paz.md` | O **deck** em Marp (o que se vê), com presenter notes. |
| `guion/guion.md` | O **roteiro falado** em espanhol (o que se diz) + ajuda de pronúncia. |
| `research/fuentes.md` | **Fontes** e fatos verificados (pra não alucinar). |
| `research/catalogo-imagenes.md` | **Inventário de imagens**: origem, licença, crédito e slide. |
| `themes/lapaz.css` | O **tema** visual (paleta andina). |

**Regra de ouro:** slides ↔ guión ↔ presenter notes se movem **juntos**.

**Idioma:** espanhol só no que é apresentação (deck, notas, roteiro); o resto em português.

## Comandos

```bash
bin/serve    # pré-visualizar no navegador (http://localhost:8080), com recarga
bin/build    # exportar para HTML, PDF e PPTX em build/
```

> Requer Node (22 ou 24; o 25 quebra o Marp) + `npx` — usa `@marp-team/marp-cli@4.5.1`
> sob demanda, sem instalar nada global — e o Google Chrome para exportar PDF/PPTX.
> Ajuste `CHROME_PATH` se necessário.

## Trocar ou adicionar imagens

A base de imagens vem do Wikimedia Commons (licenças livres). Para trocar por uma
foto sua:

1. **Salve a imagem em `assets/`**. O jeito mais simples é **substituir o arquivo
   mantendo o mesmo nome** (ex.: `assets/lapaz-teleferico.jpg`) — o slide já aponta
   para ele. Veja em `research/catalogo-imagenes.md` qual arquivo está em qual slide.
2. Ou aponte o slide para um arquivo novo, logo depois do `<!-- _class: ... -->`:
   ```markdown
   ![bg right:42% cover](../assets/minha-foto.jpg)
   ```
   - `bg` = fundo · `right:42%` = ocupa 42% à direita (pode ser `left`, ou mudar o %).
   - `cover` = preenche recortando · `contain` = mostra a imagem inteira.
3. **Atualize o crédito** em `research/catalogo-imagenes.md` (o deck não tem mais
   linha de créditos no último slide; eles ficam só no catálogo).
4. Rode `bin/build` e **confira o PDF** (é mais rígido que o HTML).

## Para apresentar
- **Ensaiar** com `guion/guion.md`, cronometrando (alvo: 5:00).
- **Apresentar** abrindo `build/la-paz.html` (tecla `F` = tela cheia; setas navegam).
- Ou subir `build/la-paz.pptx` no Google Slides / PowerPoint.
