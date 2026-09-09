# Changelog — Organizer

Entrada nova sempre no topo.

## 09/09/2026 — sessão 1 (do zero ao publicado)

O projeto inteiro nasceu nesta sessão, em cima do repositório vazio
`FabioMiranda04/organizer`.

**Base**
- Kanban num `index.html` único: projetos, três colunas, `localStorage`,
  exportar/importar. Sem build e sem dependência.
- Publicação por GitHub Pages na raiz da `main`. A tentativa de ligar o Pages
  por workflow falhou (`Resource not accessible by integration` — o
  `GITHUB_TOKEN` não cria o site), então o workflow foi removido e o Fábio
  ligou à mão.

**Visual, em três direções até acertar**
1. Frutiger Aero claro (aprovado, mas ele quis algo mais afiado);
2. aero-tech escuro (reprovado);
3. **Y2K**: estrutura de página de 2003 com cromo, holográfico, sparkles,
   barcode e painéis com barra de título. Esta ficou.
- Tipografia trocada por Archivo Black + Nunito Sans + Silkscreen (a dupla
  anterior era genérica demais), mais Bungee nos adesivos.
- Desktop apenas, a pedido: largura fixa, nenhuma media query.
- Tira do cartão passou de gradiente holográfico a **cor do projeto**, de uma
  paleta fixa de oito — o hash de id anterior jogava projetos vizinhos no
  mesmo verde.

**Interação**
- Arrasto reescrito: saiu o drag-and-drop nativo (bitmap congelado, não
  anima), entrou pointer events com clone real — o cartão **balança como
  pêndulo**, no espírito do menu do Wii. Passou a reordenar dentro da coluna.
- Edição só sob demanda (duplo clique ou `✎`): `contenteditable` sempre
  ligado sequestrava o arrasto.
- Esqueleto de 380 ms ao trocar de projeto, na quantidade real de tarefas.

**Enfeites**
- Comemoração exagerada ao concluir: tremor, flash único, ondas de choque,
  confete, adesivo de rua e placar com combo. Som sintetizado no Web Audio.
- Tevê de gato no canto, com chuvisco em `<canvas>` entre os canais.
  Legendas de meme foram removidas a pedido — ficaram só os gatos.
- Mascote: primeiro desenhado em SVG, depois substituído pela arte que o
  Fábio subiu. A arte veio 2000x2000 sem alfa; foi recortada, reduzida para
  520x358 e ganhou **canal alfa de verdade** por preenchimento a partir das
  bordas (branco chapado não servia: o corpo dele é branco).

**Desempenho**
- Primeira rodada: `backdrop-filter` saiu de cartões e pills (23 elementos →
  5), desfoque de 26px para 13px, animações de `background-position` e
  `border-radius` viraram `hue-rotate` e `transform`, `mirar()` do arrasto
  passou a rodar uma vez por quadro, aba escondida pausa o ambiente.
- Segunda rodada, depois do relato "pesado no Chrome, liso no Firefox":
  **`backdrop-filter` removido por completo** (5 → 0). No Chrome ele cria um
  *backdrop root* e obriga a re-desfocar quase a tela inteira a cada quadro,
  porque há 15 elementos se movendo atrás dos painéis. O borrão do vidro foi
  recuperado borrando as próprias bolhas com `filter` estático.

**Correções pelo caminho**
- Costura escura no topo da pill ativa (era o `backdrop-filter` com borda
  arredondada), isolada por bisseção.
- Bloco de JS do mascote tinha caído dentro do `<style>` por causa de
  marcador de comentário duplicado — quebrava o script inteiro.
- Etiqueta do projeto era riscada junto com o texto nos cartões concluídos.
- Wordmark cromado ilegível e faixa branca abaixo da dobra, na fase Frutiger.
