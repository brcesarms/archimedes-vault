# 📂 Convenção: Estrutura de Projetos (`~/projetos/`)

> Carregue este arquivo quando for criar, mover ou organizar projetos/repositórios no sistema.

## 🎯 Regra Central

**Projetos de código, automação e infraestrutura ficam em `~/projetos/`** — NUNCA soltos na home.

```text
/home/brn/
├── archimedes-vault/       <-- 🏛️ Cofre Obsidian (histórico de conhecimento) — NÃO MEXER
├── projetos/               <-- 📂 PASTA CENTRAL DE PROJETOS
│   ├── projeto-bancada/    <-- ✅ Repo GitHub: brcesarms/projeto-bancada
│   ├── archimedes-backup/  <-- ✅ Repo GitHub: brcesarms/archimedes-backup (backup único: robocopy + rsync)
│   └── archimedes-after-install-win11/ <-- ✅ Repo GitHub: brcesarms/archimedes-after-install-win11 (pós-instalação + desbloat Win11)
└── ...pastas padrão...     <-- Documentos, Downloads, etc.
```

## 📋 Regras

| Regra | Detalhe |
| :--- | :--- |
| **Localização** | Todo novo projeto/repo clonado ou criado → `~/projetos/<nome>/` |
| **Nome da pasta** | `kebab-case`, minúsculo, sem acento (ex: `projeto-bancada`) |
| **Vault é sagrado** | `~/archimedes-vault` NÃO move — caminhos absolutos fixos (AGENTS.md, opencode, submódulos) |
| **Novo repo GitHub** | Criar pasta em `~/projetos/`, clonar/nascer lá, push direto |
| **Migrações** | Sempre solicitar aprovação antes de mover pastas existentes |
| **🔗 Interligação entre repos** | Repositórios **NUNCA são silos**: documentação que afete outro projeto DEVE ser referenciada cruzadamente (guia de preparação no `archimedes-backup` ↔ vault/skills ↔ projeto-bancada). Ao criar/editar doc, procure onde ela deveria ser linkada nos demais repos. |

## 🗺️ Mapa de Projetos Atuais

| Projeto | Caminho Local | Repo GitHub | Visibilidade |
| :--- | :--- | :--- | :--- |
| projeto-bancada | `~/projetos/projeto-bancada/` | `brcesarms/projeto-bancada` | 🌐 Público |
| archimedes-backup | `~/projetos/archimedes-backup/` | `brcesarms/archimedes-backup` | 🌐 Público |
| archimedes-after-install-win11 | `~/projetos/archimedes-after-install-win11/` | `brcesarms/archimedes-after-install-win11` | 🌐 Público |

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