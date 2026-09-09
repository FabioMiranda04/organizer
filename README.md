# Organizer

Kanban simples para anotar as tarefas dos meus projetos.

Um arquivo. Sem build, sem dependência, sem servidor: abra o `index.html`
no navegador e está funcionando.

## Como funciona

- **Projetos** ficam nos chips do topo. `+ projeto` cria, e quando um está
  selecionado aparecem `renomear` / `excluir`.
- **Colunas**: Backlog → Fazendo → Feito.
- **Nova tarefa**: digite no campo do fim da coluna e tecle Enter.
- **Mover**: arraste o cartão, ou use as setas `‹ ›` dele (é o que funciona
  no celular).
- **Editar**: clique no texto do cartão e escreva. Apagar tudo apaga a tarefa.
- **Apagar**: o `×` do cartão. Em *Feito* há um `limpar` que varre a coluna.
- **Todos**: mostra os projetos juntos, cada cartão com a etiqueta do seu.

## Onde os dados ficam

No `localStorage` deste navegador, na chave `organizer.kanban.v1`. Não sobe
para lugar nenhum — o que significa que **não sincroniza entre aparelhos** e
some se você limpar os dados do site.

Por isso existem `exportar` e `importar` no canto do cabeçalho: exportar
baixa um `.json` com tudo, importar substitui o que está salvo. É o backup.

## Publicar

É um site estático. Serve qualquer host: arraste a pasta na Vercel/Netlify,
ou ligue o GitHub Pages nas configurações do repositório (branch `main`,
pasta raiz). Nada para configurar.
