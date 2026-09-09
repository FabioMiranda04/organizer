# CLAUDE.md — Organizer

## 1. O app

Kanban pessoal para o backlog dos projetos do Fábio. **Uso pessoal, uma
pessoa só.** Estética Y2K: estrutura de página de 2003 com cromo,
holográfico e sparkles por cima.

No ar: <https://fabiomiranda04.github.io/organizer/>
Repositório: `FabioMiranda04/organizer`. Branch de trabalho:
`claude/kanban-project-tasks-i49bl5`. **`main` é produção** — o GitHub Pages
serve a raiz da `main` e republica sozinho a cada push.

## 2. Arquitetura

| Arquivo | O que é |
|---|---|
| `index.html` | **o app inteiro** — markup, CSS e JS num arquivo só |
| `mascote.webp` | arte do mascote, 520x358, com canal alfa |
| `.nojekyll` | faz o Pages servir os arquivos como estão |
| `README.md` | **a documentação de verdade** — o que cada coisa faz e por quê. Leia antes de mexer |
| `docs/` | estado atual e histórico |

**Não existe** (e não presuma que exista): `package.json`, bundler, passo de
build, dependência, teste automatizado, backend, framework, CSS externo.
Fonte vem do Google Fonts por `<link>`, e o app funciona sem ela.

## 3. Comandos

Nenhum. Abrir `index.html` no navegador. Publicar = `git push origin HEAD:main`.

## 4. Regras

**R1 — Um arquivo.** Tudo em `index.html`. Se algo parecer exigir um segundo
arquivo de código, provavelmente não exige.

**R2 — Zero dependência.** Sem framework, sem biblioteca, sem CDN de script.
Ícone é emoji ou SVG inline. A única coisa que sai para a rede é a tevê,
puxando gato do `cataas.com`, e ela degrada para `SEM SINAL` sem quebrar nada.

**R3 — Português do Brasil** na UI, no commit, no comentário e no nome de
variável e função. O código já está todo assim (`desenharQuadro`, `festejar`,
`chamarMascote`, `esqueleto`).

**R4 — Desktop apenas**, a pedido do usuário. Largura fixa de 1180px,
`min-width: 1220px` no body, `viewport` travado em 1220 e **nenhuma media
query de tela**. Não reintroduza responsivo sem ele pedir.

**R5 — Dado só em `localStorage`**, chave `organizer.kanban.v1`. Nada de
servidor. O objeto salvo é `{projetos, tarefas, filtro, som, tv, mascote}` —
as preferências viajam junto no exportar/importar.

**R6 — `prefers-reduced-motion` é respeitado** em tudo que anima. Toda
animação nova precisa entrar na lista do `@media` lá embaixo do CSS.

**R7 — Nada de `backdrop-filter`.** Já custou uma sessão inteira (§5).

**R8 — Nada de elogio ao usuário.** O que a interface fala é placar de
arcade (`CLEAR!`, `+200`, `2x COMBO`) ou mensagem de sistema (`C:\> defrag
backlog`). "Mandou bem", "parabéns" e cutucão do tipo "você tá adiando isso"
foram rejeitados explicitamente — dão vergonha alheia.

**R9 — Estrutura que informa.** Numeração, etiqueta e cor precisam
significar algo: `01/02/03` porque Backlog→Fazendo→Feito é sequência de
verdade; a tira do cartão é a cor do projeto; a quantidade de esqueletos é a
quantidade real de tarefas que vem.

**R10 — Fim de sessão:** atualize `docs/CHANGELOG.md` (entrada nova no topo)
e `docs/ESTADO-DO-PROJETO.md`, depois `npm`-nada, commit e push na `main`.

## 5. Armadilhas já pagas — não repita

1. **`backdrop-filter` trava o Chrome.** Ele cria um *backdrop root*: tudo
   atrás perde composição independente e é rasterizado e desfocado de novo a
   cada mudança. Com painéis cobrindo a tela e bolhas se movendo atrás, a
   tela inteira era re-desfocada por quadro. Firefox não sofria — foi assim
   que o sintoma apareceu. **Para "vidro", use fundo translúcido + aresta
   especular, e borre os próprios elementos do fundo com `filter` estático.**
2. **`contenteditable` sempre ligado sequestra o arrasto.** Puxar pelo texto
   selecionava letras em vez de mover o cartão. O texto só vira editável no
   duplo clique ou no botão `✎`.
3. **Drag-and-drop nativo não anima.** O que segue o cursor é um bitmap
   congelado. O arrasto é por pointer events com um clone real, e é isso que
   permite o balanço do cartão.
4. **`hue-rotate` num elemento com texto tinge o texto junto.** Na pill ativa
   o holográfico vive num `::before` atrás do rótulo.
5. **Filtro animado + `transform` no mesmo elemento** tira o transform do
   compositor no Chrome. Separe.
6. **Marcadores de comentário duplicados.** `/* ---------- x ---------- */`
   aparece no CSS e no JS. Substituição por texto pega a **primeira**
   ocorrência e já jogou um bloco de JS inteiro dentro do `<style>`. Edite
   por linha ou ancore no contexto.
7. **Animar `background-position`** repinta a cada quadro. Use `transform`
   ou `hue-rotate`.
8. **Só um flash na comemoração**, nunca sequência: piscar repetido em tela
   cheia é gatilho de crise fotossensível.

## 6. Como verificar mudança (contêiner remoto)

Não há teste automatizado; a verificação é renderizar de verdade. O Chromium
do contêiner está em `/opt/pw-browsers/chromium-1194/chrome-linux/chrome`.

```bash
# servir uma cópia com dados de exemplo
cd /tmp/x && python3 -m http.server 8899 --bind 127.0.0.1 &

# captura
chrome --headless --no-sandbox --disable-gpu --window-size=1260,760 \
       --screenshot=/tmp/x.png --virtual-time-budget=2500 http://127.0.0.1:8899/

# teste de comportamento: injete um <script> que dispara eventos e escreve o
# resultado num <pre id="diag">, depois leia só ele
chrome --headless ... --dump-dom http://127.0.0.1:8899/t.html | sed -n '/<pre id="diag"/,/<\/pre>/p'
```

Três limites do contêiner que confundem:

- **o headless não desce de 500px de largura** — para ver 375px, ponha o app
  num `<iframe width="375">`;
- **o Chrome não confia na CA do proxy**: Google Fonts e `cataas.com` falham
  nas capturas (fonte cai no fallback, tevê mostra `SEM SINAL`). **`curl`
  funciona** — use ele para baixar coisa da internet;
- **`ffmpeg` não decodifica webp.** Para recortar/reencodar imagem, use o
  próprio Chromium via `<canvas>` + `toDataURL`, e canalize o base64 direto
  para `base64 -d` sem imprimir.

Sempre valide JS antes de subir:
`python3` extrai o bloco do `<script>` → `node --check`.

## 7. Onde está o resto

| Preciso de… | Arquivo |
|---|---|
| o que cada recurso faz e por quê | `README.md` |
| estado atual, o que está aberto | `docs/ESTADO-DO-PROJETO.md` |
| histórico | `docs/CHANGELOG.md` |
