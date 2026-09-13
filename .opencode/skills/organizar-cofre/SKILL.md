---
name: organizar-cofre
description: Organização da estrutura de pastas e arquivos do Archimedes. Use quando o usuário pedir "organizar cofre", "arrumar pastas", "limpar estrutura", "mover notas", "reorganizar" ou quando as notas estiverem em pastas erradas. Mantém a estrutura padrão do cofre.
compatibility: opencode
metadata:
  audience: ia-local
  workflow: gestao
---

# 🗂️ Organizar o Archimedes Vault

Mantenha a estrutura do cofre organizada e padronizada.

## 📁 Estrutura padrão do cofre

```
archimedes-vault/              # repo: brcesarms/archimedes-vault
├── AGENTS.md                  # Regras e governança da IA (NÃO mover)
├── opencode.json              # Config da CLI (NÃO mover)
├── README.md                  # Documentação principal (NÃO mover)
├── setup.sh                   # Porta de entrada pós-formatação (NÃO mover)
├── .opencode/                 # Automações da CLI (skills, convencoes, agents)
├── guia-ia-local/             # 🧠 SISTEMA — inteligência, scripts e automações
│   ├── cerebrum/              #   Runbooks e rotinas do Cérebro
│   ├── scripts/               #   Scripts de infraestrutura (linux/windows)
│   ├── notas/                 #   Notas atômicas de manutenção do sistema
│   ├── perfis/                #   Perfis de hardware
│   └── dotfiles/              #   Configurações de shell e aliases
├── concurseiro/               # 📂 Submódulo Git pessoal (privado)
└── t.i/                       # 📂 Submódulo Git pessoal (público)
```

## 🔍 Como organizar

### 1. Auditar a estrutura

- Listar todas as pastas e arquivos do cofre
- Comparar com a estrutura padrão acima
- Identificar arquivos fora do lugar

### 2. Classificar cada arquivo

| 📂 Tipo de conteúdo | 🎯 Pasta correta |
|---------------------|------------------|
| Nota de manutenção do sistema | `guia-ia-local/notas/` |
| Script de manutenção do sistema | `guia-ia-local/scripts/linux/` ou `guia-ia-local/scripts/windows/` |
| Conteúdo de concurso | `concurseiro/` (submódulo) |
| Conteúdo de TI / estudos | `t.i/` (submódulo) |
| Utilitário/config do sistema | `guia-ia-local/utils/` |
| Guia, setup, perfil | `guia-ia-local/` |

### 3. Mover com segurança

- **Sempre confirmar o plano completo** antes de mover (regra de ouro)
- Mover um arquivo por vez
- Usar `mv` e verificar se o destino existe

### 4. Regras

- 🚫 **NUNCA** mover `AGENTS.md`, `opencode.json` ou a pasta `.opencode/skills/` para fora
- ✏️ Corrigir nomes de arquivos para kebab-case quando estiverem fora do padrão
- 🔗 Após mover, atualizar os links markdown que apontavam para o antigo caminho
- 📝 Nunca deixar a raiz com arquivos soltos (exceto `AGENTS.md` e `opencode.json`)

## ✅ Checklist ao finalizar

1. [ ] Estrutura segue o padrão
2. [ ] Raiz só tem `AGENTS.md`, `opencode.json` e pastas
3. [ ] Links atualizados após mover
4. [ ] Nenhum arquivo crítico movido

---

## 🔗 Fontes

- 📁 Estrutura padrão: [`AGENTS.md`](../../../AGENTS.md) (Estrutura do Vault)
