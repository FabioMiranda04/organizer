# Estado do projeto — Organizer

_Atualizado em 09/09/2026._

## Em uma linha

App **pronto e no ar**, funcionando. Nada quebrado, nada pela metade.

## O que existe

**Kanban** — três colunas (Backlog → Fazendo → Feito), projetos como pills,
tarefa com texto único. Arrastar move e reordena, com linha azul marcando
onde cai; as setas `‹ ›` fazem o mesmo sem arrastar. Editar é duplo clique
ou o `✎`. Apagar o texto todo apaga a tarefa.

**Dados** — `localStorage`, chave `organizer.kanban.v1`. `exportar` baixa
um JSON com tudo (inclusive as preferências de som/tv/mascote), `importar`
substitui.

**Enfeites, todos desligáveis pelo banner:**

| | botão | o que faz |
|---|---|---|
| Som da comemoração | `🔊 som` | Web Audio sintetizado, sem arquivo |
| Tevê de gato | `📺 tv` | CRT no canto com gatos do `cataas.com` e chuvisco entre canais |
| Mascote | `🖥️ mascote` | sempre à vista no canto inferior esquerdo, boiando, rodopiando |

**Comemoração ao concluir** — tremor, um flash, três ondas de choque,
confete, adesivo de rua sorteado (`CLEAR!`, `TAGGED`, `S-RANK`…), `+100` e
combo por conclusões em até 7s.

**Trocar de projeto** — esqueleto por 380 ms na quantidade real de tarefas
que vem, depois os cartões entram escalonados.

## Publicação

GitHub Pages **já ligado**, servindo a raiz da `main`. Todo push republica
sozinho. Confirmado no ar: HTTP 200, `mascote.webp` servindo os 47.682 bytes
da versão com alfa.

## Decisões que não devem ser revisitadas sem o Fábio pedir

- **Desktop apenas.** Foi decisão explícita dele. Não há media query de tela.
- **Nada de elogio ao usuário.** Duas rodadas foram rejeitadas por isso
  ("mandou bem" e as legendas de meme na tevê). O registro certo é placar de
  arcade e mensagem de sistema.
- **Um arquivo, zero dependência.** Nunca pediu build e não deve ganhar um.
- **Sem `backdrop-filter`.** Ver `CLAUDE.md` §5.1.

## Aberto / ideias não pedidas

Nada pendente. Se ele voltar querendo mais, o que faz sentido e ainda não
existe:

- **Prazo ou data na tarefa** — hoje a tarefa é só texto.
- **Ordenar ou filtrar dentro da coluna** — hoje a ordem é manual.
- **Arquivar projeto** em vez de excluir — hoje excluir leva as tarefas junto.
- **Sincronizar entre aparelhos** — exigiria backend, o que contraria a R2.
  O caminho barato seria exportar/importar por arquivo, que já existe.
- **Domínio próprio** no lugar de `github.io`.

## Riscos conhecidos

- **`localStorage` é o único armazenamento.** Limpar dados do site apaga
  tudo. O `exportar` é o backup, e isso está dito no README e na UI.
- **A tevê depende de um serviço de terceiros** (`cataas.com`). Se sumir de
  vez, o app segue funcionando com `SEM SINAL`; trocar de fonte é mexer numa
  linha em `trocarCanal()`.
