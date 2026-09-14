---
title: "Estrutura do Cofre — Sistema Cérebro & Executor"
date_created: 2026-09-08
date_updated: 2026-09-08
tags:
  - cerebro
  - estrutura
  - organizacao
status: ativo
---

# 🗂️ Estrutura do Archimedes Vault (Sistema Cérebro & Executor)

> Árvore lógica para o sistema. O sistema de automação e inteligência reside em `guia-ia-local/` e `.opencode/`, mantendo a raiz limpa. Os estudos pessoais (`t.i/`, `concurseiro/`) ficam **fora do repositório**, em `~/wikisidian/`.

## 🌳 Árvore de Diretórios

```
archimedes-vault/
├── AGENTS.md                    # 🏛️ Manual de governança, regras e identidade
├── opencode.json                # ⚙️ Configurações da CLI
├── README.md                    # 📖 Documentação principal
├── setup.sh                     # 🚀 Script de setup pós-formatação
├── .opencode/                   # 🤖 Automações da CLI (skills, agents, convencoes)
├── guia-ia-local/               # 🧠 SISTEMA (scripts, notas, perfis, cerebrum)
│   ├── cerebrum/                # 🧠 Sistema Cérebro ↔ Executor
│   │   ├── master-plan.md       # 📋 Plano diretor em fases (Cérebro lê)
│   │   ├── estrutura-cofre.md   # 🗂️ Este documento (Cérebro lê)
│   │   ├── template-runbook.md  # 📝 Template padrão de Runbook (Cérebro usa)
│   │   ├── rotinas/             # 📋 RUNBOOKS prontos — 📖 única leitura do Executor
│   │   ├── prompts/             # 💬 Prompts atômicos para o Executor
│   │   ├── systemd/             # ⏱️ Units de automação systemd
│   │   └── logs/                # 🪵 Logs de execução (Executor escreve aqui)
│   ├── scripts/                 # 🐚 Scripts (o Executor executa, nunca edita)
│   │   ├── linux/
│   │   └── windows/
│   ├── notas/                   # 🗒️ Notas atômicas de manutenção do sistema
│   ├── perfis/                  # 🖥️ Perfis por máquina
│   └── dotfiles/                # 🐚 Configurações de terminal
└── README.md                    # 📖 Documentação principal

# Fora do repositório (privado)
~/wikisidian/
├── t.i/                         # 📂 ESTUDOS: T.I., redes e certificações
└── concurseiro/                 # 📂 ESTUDOS: Concursos públicos
```

## 🎭 Quem Lê o Quê

| Ator | Lê | Escreve/Executa |
|------|----|-----------------|
| 🧠 **Cérebro** (modelo grande) | `AGENTS.md`, `master-plan.md`, `template-runbook.md`, `logs/estado-falhas.md` (ao iniciar sessão) | Gera/atualiza Runbooks e scripts; decide ações a partir dos alertas |
| ⚡ **Executor** (modelo local rápido) | **SOMENTE** `cerebrum/rotinas/*.md` | Roda os comandos exatos do Runbook; escreve em `cerebrum/logs/`; marca `#falha` |

## 📏 Regras de Ouro

- 🚫 Executor **nunca** lê `AGENTS.md`, `template-runbook.md` nem `master-plan.md`
- ⚙️ Executor **nunca** edita scripts — apenas copia/cola o comando do Runbook
- 🪵 Toda execução gera log em `cerebrum/logs/`
- 🏷️ Falha → tag `#falha` no Runbook + PARE (nunca improvisar)

---

## 🔗 Fontes

- 🧠 Nota raiz: [`AGENTS.md`](../../AGENTS.md)
- 🗺️ Plano: [`master-plan.md`](./master-plan.md)
- 📄 Estrutura padrão do cofre: [`AGENTS.md`](../../AGENTS.md)