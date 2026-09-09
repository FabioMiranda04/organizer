# Organizer

Kanban para anotar as tarefas dos meus projetos.

Estética Y2K: estrutura de página de 2003 — pills envidraçadas, barcode,
painéis com barra de título — com cromo, gradiente holográfico e sparkles por
cima.

**No ar:** https://fabiomiranda04.github.io/organizer/ — depois de ligar o
Pages uma vez (veja *Publicação*).

Um arquivo. Sem build, sem dependência, sem servidor: o `index.html` sozinho
já é o app — abre direto no navegador se você quiser.

## Feito para computador

Largura fixa de 1180px, sem layout responsivo — foi decisão sua, e por isso
não há nenhuma media query de tela pequena. Em celular a página não quebra,
só pede zoom/rolagem lateral.

## Como funciona

- **Projetos** são as pills da barra. `+ projeto` cria ali mesmo, digitando;
  o projeto ativo fica holográfico e vira o título da faixa, onde aparecem
  `renomear` e `excluir`.
- **Colunas**: Backlog → Fazendo → Feito. Os números `01/02/03` estão ali
  porque isso é mesmo uma sequência, não enfeite.
- **Progresso** no widget da direita: cada célula acesa mostra uma fatia
  diferente do espectro.
- **Nova tarefa**: digite no campo do fim da coluna e tecle Enter.
- **Mover**: arraste o cartão — ele se solta da coluna e vai balançando como
  pêndulo atrás do cursor, no espírito do menu do Wii. Uma linha azul mostra
  onde ele vai cair, e dá
  para reordenar dentro da própria coluna, não só trocar de coluna. Soltar no
  vazio da coluna joga para o fim. As setas `‹ ›` do cartão fazem o mesmo sem
  arrastar.
- **Editar**: duplo clique no cartão, ou o `✎` que aparece ao passar o mouse.
  O texto só fica editável nesse momento — se ficasse sempre, arrastar pelo
  texto selecionaria letras em vez de mover o cartão. Apagar o texto todo
  apaga a tarefa.
- **Apagar**: o `×` do cartão. Em *Feito* há um `limpar` que varre a coluna.
- **Todos**: mostra os projetos juntos, cada cartão com a etiqueta do seu.
- **A tira colorida do cartão é a cor do projeto** — vem de uma paleta fixa
  de oito cores, na ordem em que os projetos foram criados. Em *Feito* ela
  passa a verde, para a coluna se ler de longe.

## Onde os dados ficam

No `localStorage` **deste navegador**, na chave `organizer.kanban.v1`. Nada
sobe para servidor nenhum — ou seja: **não sincroniza entre aparelhos** e some
se você limpar os dados do site.

Por isso existem `exportar` e `importar` no banner: exportar baixa um `.json`
com tudo, importar substitui o que está salvo. É o backup.

## Publicação

GitHub Pages servindo a raiz da `main`. Ligar isso é um passo manual e único
— só o dono do repositório pode criar o site, nem o token do Actions
consegue:

> **Settings → Pages → Source: _Deploy from a branch_ → Branch: `main` /
> `(root)` → Save**

Depois disso todo push na `main` republica sozinho, sem build e sem workflow.
O `.nojekyll` está aí só para o Pages servir os arquivos como estão.

## Notas de design

- **Fontes**: `Archivo Black` no cromo do título, `Nunito Sans` no texto e
  `Silkscreen` (pixel) só nos rótulos fixos — pixel não tem acento, então
  nada que o usuário escreve passa por ela. Vêm do Google Fonts; se não
  carregarem, o app cai para as fontes do sistema e continua funcionando.
- **Cromo** é gradiente com faixa escura na linha do horizonte mais contorno
  fino, recortado no texto. **Holográfico** é um gradiente de seis paradas
  girando o matiz; nas tiras dos cartões ele vai em tamanho natural para o
  arco-íris aparecer inteiro, e nas células do medidor cada uma pega uma
  fatia distinta.
- **Liquid glass**: os painéis são translúcidos com `backdrop-filter`
  (desfoque + saturação), aresta especular de 1px no topo e brilho interno
  na base. Para o vidro ter o que distorcer existem manchas holográficas
  boiando atrás de tudo — sem elas, vidro sobre fundo liso não parece vidro.
  Os cartões ficam quase opacos de propósito: leitura vem antes do efeito.
- Fundo, blob, bolhas, wireframe, lens flare, barcode e sparkles são todos
  CSS/SVG — nenhuma imagem para baixar.
- **Arrasto não usa o drag-and-drop nativo**: nele o que segue o cursor é um
  bitmap congelado do elemento, impossível de animar. Em vez disso, pointer
  events com um clone real seguindo o mouse — é o que permite o balanço. O
  arrasto só começa depois de 5px de movimento, para clique continuar sendo
  clique.
- Animação respeita `prefers-reduced-motion` (o cartão arrastado fica
  inclinado e parado), e o foco de teclado tem anel visível.
