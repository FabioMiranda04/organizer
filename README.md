# Organizer

Kanban para anotar as tarefas dos meus projetos.
Visual Frutiger Aero: céu, vidro, bolhas e botões brilhantes.

**No ar:** https://fabiomiranda04.github.io/organizer/ — depois de ligar o
Pages uma vez (veja *Publicação*).

Um arquivo. Sem build, sem dependência, sem servidor: o `index.html` sozinho
já é o app — abre direto no navegador se você quiser.

## Como funciona

- **Projetos** são os chips do topo. `+ projeto` cria ali mesmo, digitando no
  chip; com um selecionado aparecem `renomear` e `excluir`.
- **Colunas**: Backlog → Fazendo → Feito. A barra do cabeçalho mostra quanto
  do que está à vista já foi feito.
- **Nova tarefa**: digite no campo do fim da coluna e tecle Enter.
- **Mover**: arraste o cartão, ou use as setas `‹ ›` dele — é o que funciona
  no celular, onde arrastar não vai.
- **Editar**: clique no texto do cartão e escreva. Apagar o texto todo apaga
  a tarefa.
- **Apagar**: o `×` do cartão. Em *Feito* há um `limpar` que varre a coluna.
- **Todos**: mostra os projetos juntos, cada cartão com a etiqueta do seu.

No celular vira uma coluna só. Dá para adicionar à tela de início pelo
Safari/Chrome e ele abre em tela cheia, como app.

## Onde os dados ficam

No `localStorage` **deste navegador**, na chave `organizer.kanban.v1`. Nada
sobe para servidor nenhum — ou seja: **não sincroniza entre aparelhos** e some
se você limpar os dados do site.

Por isso existem `exportar` e `importar` no cabeçalho: exportar baixa um
`.json` com tudo, importar substitui o que está salvo. É o backup, e é
também como levar as tarefas do computador para o celular.

## Publicação

GitHub Pages servindo a raiz da `main`. Ligar isso é um passo manual e único
— só o dono do repositório pode criar o site, nem o token do Actions
consegue:

> **Settings → Pages → Source: _Deploy from a branch_ → Branch: `main` /
> `(root)` → Save**

Depois disso todo push na `main` republica sozinho, sem build e sem workflow.
O `.nojekyll` está aí só para o Pages servir os arquivos como estão.

## Sobre a fonte

A tipografia é a **Titillium Web**, vinda do Google Fonts. Se ela não
carregar (sem internet, rede bloqueada), o app cai para a fonte do sistema e
continua funcionando igual — só muda o desenho das letras.
