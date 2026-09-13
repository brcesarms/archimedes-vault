# 📂 Convenção: Estrutura de Projetos (`~/projetos/`)

> Carregue este arquivo quando for criar, mover ou organizar projetos/repositórios no sistema.

## 🎯 Regra Central

**Projetos de código, automação e infraestrutura ficam em `~/projetos/`** — NUNCA soltos na home.

```text
/home/brn/
├── archimedes-vault/       <-- 🏛️ Cofre Obsidian (histórico de conhecimento) — NÃO MEXER
├── projetos/               <-- 📂 PASTA CENTRAL DE PROJETOS
│   ├── archimedes-operator/    <-- ✅ Repo GitHub: brcesarms/archimedes-operator
│   ├── archimedes-backup/  <-- ✅ Repo GitHub: brcesarms/archimedes-backup (backup único: robocopy + rsync)
│   ├── archimedes-win11-setup/ <-- ✅ Repo GitHub: brcesarms/archimedes-win11-setup (pós-instalação + desbloat Win11)
│   ├── usb-bootavel-tui/    <-- ✅ Repo GitHub: brcesarms/usb-bootavel-tui (criador de pendrive bootável TUI)
│   ├── archimedes-rag/      <-- ✅ Repo GitHub: brcesarms/archimedes-rag (RAG local com AST e LanceDB para OpenCode CLI)
│   └── archimedes-doctor/   <-- ✅ Repo GitHub: brcesarms/archimedes-doctor (Gerador de testes com Self-Healing loop)
└── ...pastas padrão...     <-- Documentos, Downloads, etc.
```

## 📋 Regras

| Regra | Detalhe |
| :--- | :--- |
| **Localização** | Todo novo projeto/repo clonado ou criado → `~/projetos/<nome>/` |
| **Nome da pasta** | `kebab-case`, minúsculo, sem acento (ex: `archimedes-operator`) |
| **Vault é sagrado** | `~/archimedes-vault` NÃO move — caminhos absolutos fixos (AGENTS.md, opencode, submódulos) |
| **Novo repo GitHub** | Criar pasta em `~/projetos/`, clonar/nascer lá, push direto |
| **Migrações** | Sempre solicitar aprovação antes de mover pastas existentes |
| **🔗 Interligação entre repos** | Repositórios **NUNCA são silos**: documentação que afete outro projeto DEVE ser referenciada cruzadamente (guia de preparação no `archimedes-backup` ↔ vault/skills ↔ archimedes-operator). Ao criar/editar doc, procure onde ela deveria ser linkada nos demais repos. |

## 🗺️ Mapa de Projetos Atuais

| Projeto | Caminho Local | Repo GitHub | Visibilidade |
| :--- | :--- | :--- | :--- |
| archimedes-operator | `~/projetos/archimedes-operator/` | `brcesarms/archimedes-operator` | 🌐 Público |
| archimedes-backup | `~/projetos/archimedes-backup/` | `brcesarms/archimedes-backup` | 🌐 Público |
| archimedes-win11-setup | `~/projetos/archimedes-win11-setup/` | `brcesarms/archimedes-win11-setup` | 🌐 Público |
| usb-bootavel-tui | `~/projetos/usb-bootavel-tui/` | `brcesarms/usb-bootavel-tui` | 🌐 Público |
| archimedes-rag | `~/projetos/archimedes-rag/` | `brcesarms/archimedes-rag` | 🌐 Público |
| archimedes-doctor | `~/projetos/archimedes-doctor/` | `brcesarms/archimedes-doctor` | 🌐 Público |

## ⚙️ Fluxo para Novo Projeto

```bash
# 1. Criar/clonar na pasta central
mkdir -p ~/projetos && cd ~/projetos
git clone git@github.com:brcesarms/<novo-projeto>.git

# 2. Trabalhar dentro de ~/projetos/<novo-projeto>/
# 3. Commits seguem as convenções git (convencoes-git.md)
```

## ⚠️ Exceções

- `~/archimedes-vault` → **NUNCA** mover (muitas referências absolutas).
- `~/obsidian-cofre-v1` → cofre legado; movido para `~/projetos/` apenas se o usuário solicitar explicitamente.
- Ferramentas pessoais (`.opencode`, `.config`, `.local`) → NUNCA em projetos.

---

## 🔗 Fontes

- [Filesystem Hierarchy Standard](https://refspecs.linuxfoundation.org/FHS_3.0/fhs/index.html)