# Organizer

Kanban para anotar as tarefas dos meus projetos.

> Retomando o projeto? Comece pelo `CLAUDE.md` (regras e armadilhas) e por
> `docs/ESTADO-DO-PROJETO.md` (o que está pronto e o que está aberto).

Estética Y2K: estrutura de página de 2003 — pills envidraçadas, barcode,
painéis com barra de título — com cromo, gradiente holográfico e sparkles por
cima.

**No ar:** https://fabiomiranda04.github.io/organizer/

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

## Quando uma tarefa chega em Feito

A tela inteira reage, de propósito exagerado: tremor, um flash, três ondas de
choque saindo de onde você soltou o cartão, raios, confete de estrelinhas,
CDs e respingos de spray, e um adesivo de rua entrando torto — `CLEAR!`,
`TAGGED`, `FRESH`, `S-RANK`, `JET SET`, `NEXT!`, `RIDE ON`.

**Não tem elogio, tem placar.** Em Jet Set Radio nada te parabeniza: te dá
rank. Então sai `+100`, e concluir de novo em até 7 segundos acumula
`2x COMBO`, `3x COMBO`… com os pontos multiplicando e o tom do som subindo
um semitom por passo, como contador de fliperama.

O som é sintetizado na hora pelo Web Audio — chiado de lata de spray, baque
grave e naipe de sopro. Nenhum arquivo de áudio no repositório.

O botão `🔊 som` no banner desliga só o áudio; a preferência fica salva junto
com as tarefas. Quem tem `prefers-reduced-motion` ligado no sistema recebe
só o som, sem a parte visual.

O flash é **um** e não uma sequência: piscar repetido em tela cheia é gatilho
de crise fotossensível.

## A tevê do canto

Uma CRT de plástico no canto inferior direito passando gatos aleatórios, e só
os gatos — sem legenda por cima. Clique na tela para trocar de canal; sozinha
ela troca a cada 15 segundos. Entre um gato e outro entra chuvisco de verdade
— ruído desenhado pixel a pixel num `<canvas>` de 96x72, com barra de
rolagem, esticado com `image-rendering: pixelated`.

**Ela busca as imagens do `cataas.com`** (Cat as a Service — grátis, sem
chave). É a única coisa no app que sai para a internet; se o serviço estiver
fora, a tela mostra `SEM SINAL` e o resto do app segue igual. O botão
`📺 tv` no banner desliga, e desligada ela não faz requisição nenhuma.

## O mascote

Um monitor de tubo de pernas curtas, com teclado de escudo e pá de espada.
Fica **sempre** no canto inferior esquerdo, pequeno, boiando de leve; de
tempos em tempos dá um rodopio completo. Clicar nele faz rodopiar na hora e
ele fala.

O que ele fala são **mensagens de sistema**, não recados para você:
`C:\> defrag backlog`, `640K é memória suficiente`, `não desligue o
computador`. Elogio e cutucão dão vergonha alheia — a piada está no
computador velho, não em você. O combo acima de 3 também o chama, com
`buffer overflow`. O botão `🖥️ mascote` no banner o aposenta.

**Sobre a arte** (`mascote.webp`): veio em 2000x2000 com quase metade de
margem vazia e **sem canal alfa** — fundo branco chapado. Foi recortada na
caixa do personagem, reduzida para 520x358 e **recebeu canal alfa de
verdade**: 42% dos pixels são totalmente transparentes. 47 KB, contra os 188
KB do original.

O recorte não podia ser "branco vira transparente", senão o corpo branco
dele viraria buraco. É um preenchimento a partir das quatro bordas, que só
alcança o fundo — o branco de dentro está cercado pelo contorno preto e
nunca é atingido. A sombra da arte, que o preenchimento alcança, virou um
azul-acinzentado translúcido em vez de sumir, para continuar sendo sombra em
qualquer cor de página. WebP com alfa em vez de PNG: mesma transparência,
arquivo bem menor.

## O ambiente é vivo

Atrás dos painéis flutuam bolhas subindo, faíscas piscando e mini-CDs
holográficos vagando e girando. Como os painéis são de vidro, o
`backdrop-filter` desfoca tudo que passa por trás deles de graça — o
movimento aparece borrado sob o vidro e nítido nas frestas. O blob do banner
respira mudando o próprio contorno, e o globo de arame gira devagar.

## Onde os dados ficam

No `localStorage` **deste navegador**, na chave `organizer.kanban.v1`. Nada
sobe para servidor nenhum — ou seja: **não sincroniza entre aparelhos** e some
se você limpar os dados do site.

Por isso existem `exportar` e `importar` no banner: exportar baixa um `.json`
com tudo, importar substitui o que está salvo. É o backup.

## Publicação

GitHub Pages **já ligado**, servindo a raiz da `main`: todo push republica
sozinho, sem build e sem workflow. O `.nojekyll` está aí só para o Pages
servir os arquivos como estão.

(Se um dia precisar religar: **Settings → Pages → Source: _Deploy from a
branch_ → Branch: `main` / `(root)` → Save**. É passo manual porque só o dono
do repositório pode criar o site — nem o token do Actions consegue.)

## Trocar de painel

Clicar em outro projeto não troca o conteúdo de estalo: as colunas mostram
**esqueletos** por 380 ms — blocos no formato do cartão com uma faixa de
brilho atravessando — e então os cartões reais entram escalonados, 45 ms um
atrás do outro.

A quantidade de esqueletos por coluna é a quantidade real de tarefas do
projeto que você escolheu (limitada a 4), então a transição já tem a forma
do que vem. A faixa de brilho anda por `transform`, não por
`background-position`: uma é composta pela GPU, a outra repintaria a cada
quadro. Com `prefers-reduced-motion` a troca é imediata, sem esqueleto.

## Desempenho das animações

### Por que estava pesado no Chrome e leve no Firefox

Sintoma real: travava no Chrome, rodava liso no Firefox. A causa era o
`backdrop-filter`.

No Chrome, um elemento com `backdrop-filter` cria um *backdrop root*: tudo
que está atrás dele **perde a composição independente** e precisa ser
rasterizado e desfocado de novo sempre que muda. Havia 5 painéis de vidro
cobrindo quase a tela inteira e 15 bolhas, faíscas e discos se movendo o
tempo todo atrás deles — ou seja, a tela quase inteira era re-desfocada a
cada quadro. O Firefox implementa o mesmo efeito pelo WebRender de um jeito
que não cai nesse padrão, e por isso ia bem.

**O `backdrop-filter` saiu por completo.** O que ele fazia visualmente era
desfocar um degradê já suave — quase nada. E o que ele fazia de fato era
desfocar as bolhas que passavam atrás do vidro; isso foi recuperado
borrando **as próprias bolhas** com um `filter` estático. Filtro fixo em
elemento que só anima `transform` vira textura em cache, movida pelo
compositor: sai de graça, e vale em qualquer navegador.

Junto disso: o blob do banner deixou de animar `filter` e `transform` ao
mesmo tempo (filtro animado tira o transform do compositor no Chrome), e o
raio de desfoque das manchas de fundo caiu de 70px para 48px.

### Antes disso

Medido no próprio app, contando elementos com `backdrop-filter` e com
animação ativa:

| | antes | depois |
|---|---|---|
| elementos com `backdrop-filter` | 23 | 5 → **0** |
| elementos animados | 36 | **28** |

O que estava caro e o que mudou:

- **Vidro em coisa pequena.** Cartões, pills e o widget tinham
  `backdrop-filter` e já eram ~94% opacos: o desfoque não aparecia e cada um
  virava uma camada que a GPU recompõe. Saiu de todos; ficou só nos cinco
  painéis grandes, onde o efeito de fato se vê.
- **Raio do desfoque.** 26px → 13px nos painéis. O custo cresce com o raio.
- **Animação que repinta.** O holográfico animava `background-position`, o
  que repinta o elemento a cada quadro; virou `hue-rotate`, que a GPU resolve
  no compositor. Na pill ativa ele foi para uma camada atrás do texto, senão
  o filtro tingiria o rótulo junto.
- **O blob** deformava `border-radius` (repinta) e agora deforma por
  `transform` (compositor).
- **Menos coisas boiando** atrás do vidro: cada uma invalida o desfoque dos
  painéis. 10 bolhas → 6, 9 faíscas → 6, 4 discos → 3.
- **Arrastar** chamava `elementFromPoint` e `getBoundingClientRect` a cada
  `pointermove`, forçando layout no meio do gesto. Agora no máximo uma vez
  por quadro, via `requestAnimationFrame`.
- **Chuvisco** alocava um `ImageData` novo por quadro; agora reaproveita o
  mesmo.
- **Aba escondida** pausa bolhas, faíscas, discos, blob e mascote.

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
