# 🏛️ Archimedes Vault (`archimedes-vault`)

> *"Dê-me um script e uma CLI e automatizarei o dia a dia."*

[![GitHub](https://img.shields.io/badge/GitHub-archimedes--vault-181717?style=flat-square&logo=github)](https://github.com)
[![Obsidian](https://img.shields.io/badge/Obsidian-100%25%20GFM%20Compatible-7C3AED?style=flat-square&logo=obsidian)](https://obsidian.md)
[![CLI](https://img.shields.io/badge/CLI-Antigravity%20%7C%20OpenCode-4B5563?style=flat-square)](https://antigravity.google)

---

## 📌 Sobre o Projeto

O **Archimedes Vault** é o ecossistema de **Segundo Cérebro e Automação de T.I.** de **Bruno César Medeiros Siqueira** (Analista de T.I. Pleno). 

Este repositório unifica a gestão de conhecimento no **Obsidian**, o versionamento no **GitHub** e a execução padronizada de scripts de infraestrutura (Linux/Windows) operados via **CLI** (`antigravity` e `opencode`).

---

## 🏛️ O Assistente: Archimedes

O **Archimedes** atua como o arquiteto e executor de automação do cofre, operando sob uma hierarquia de modelo duplo:

- 🧠 **CÉREBRO (Modelo Grande):** Planeja a estrutura, projeta Runbooks e desenha scripts mecânicos em `guia-ia-local/cerebrum/`.
- ⚡ **EXECUTOR (Modelo Local Rápido):** Executa os Runbooks com 100% de consistência, sem alucinações e respeitando os limites do sistema.

---

## 📐 Regras de Arquitetura & Boas Práticas

### 1. Padrão de Notas & Obsidian
- **Sintaxe:** 100% compatível com GitHub Flavored Markdown (GFM).
- **Links Relativos:** Uso exclusivo de links markdown padrão (`[Texto](./caminho/nota.md)`). **Proibido o uso de Wikilinks (`[[...]]`)**.
- **Nomenclatura:** Arquivos em `kebab-case` sem acentos ou caracteres especiais.
- **Formatação:** Título H1 com emoji, seções organizadas (H2/H3) e bloco final `## 🔗 Fontes`.

### 2. Regra do 2x (Criação de Skills)
Qualquer rotina ou tarefa executada mais de **2 vezes** deve ser abstraída e convertida em uma **Skill** reutilizável armazenada em `.opencode/skills/<nome-da-skill>/SKILL.md`.

### 3. Sincronização Automática do Mapa da Raiz
O **Archimedes** é instruído a manter o mapa da árvore de diretórios (`README.md` e `AGENTS.md`) **SEMPRE atualizado** na raiz do repositório a cada alteração de diretório, adição de novas pastas ou criação de skills.

### 4. Isolamento do Cofre
- ⚙️ **SISTEMA (`guia-ia-local/`):** Área restrita para automação, utilitários, scripts e logs.
- 📚 **ESTUDOS (`concurseiro/`, `t.i/`):** Diretórios de uso pessoal do usuário. O código de automação do sistema **nunca** modifica arquivos nestas pastas.

---

## 📂 Mapa da Estrutura de Diretórios (Sempre Atualizado na Raiz)

```text
archimedes-vault/                   <-- Raiz do seu repositório / cofre principal no Obsidian
├── .opencode/                      <-- Pasta de configurações e automações da CLI (Antigravity e OpenCode)
│   ├── agents/                     <-- Subagents especializados (estudante, resumidor, executor)
│   ├── convencoes/                 <-- Guias auxiliares (Git, SSH, Scripts, etc.)
│   └── skills/                     <-- AQUI ficam as suas skills (Regra do 2x)!
├── guia-ia-local/                  <-- 🧠 SISTEMA: Inteligência, scripts e automações locais
│   ├── benchmarks/                 <-- Benchmarks de modelos de IA local
│   ├── cerebrum/                   <-- Runbooks e rotinas Cérebro ↔ Executor
│   │   ├── logs/                   <-- Histórico de execuções de rotinas (.gitkeep)
│   │   ├── prompts/                <-- Prompts imperativos do executor
│   │   ├── rotinas/                <-- Runbooks atômicos (.md)
│   │   └── systemd/                <-- Units de automação (.service e .timer)
│   ├── docker/                     <-- Serviços containerizados (docker-compose)
│   ├── dotfiles/                   <-- Configurações de shell e aliases (.aliases, .bashrc, .prompt)
│   ├── notas/                      <-- Notas atômicas de manutenção do sistema
│   ├── perfis/                     <-- Perfis de hardware (alienware, geekom, acer-paula)
│   └── scripts/                    <-- Scripts operacionais de infraestrutura
│       ├── linux/                  <-- Scripts bash e suite de validação em validacoes/
│       ├── python/                 <-- Scripts Python p/ parsing pesado e orquestração (pytest em tests/)
│       └── windows/                <-- Scripts PowerShell
├── concurseiro/                    <-- 📚 ESTUDOS: Suas notas pessoais de estudo para concursos
├── t.i/                            <-- 📚 ESTUDOS: Suas notas pessoais de T.I. e certificações
├── .editorconfig                   <-- Padrão de formatação de arquivos
├── .gitignore                      <-- Regras de exclusão do Git
├── .gitmodules                     <-- Mapeamento de submódulos Git
├── AGENTS.md                       <-- Manual de regras, segurança e identidade do Archimedes 🏛️
├── opencode.json                   <-- Configuração de compatibilidade com a OpenCode CLI
└── README.md                       <-- Documentação principal do repositório no GitHub
```

---

## 🚀 Como Executar

### 1. Uso via Antigravity CLI (Principal)
Inicie a CLI na raiz do projeto e passe as instruções para o Archimedes:

```bash
cd ~/archimedes-vault
agy
```

No chat da CLI:
```markdown
Leia o arquivo AGENTS.md para iniciarmos.
```

### 2. Uso via OpenCode CLI (Compatibilidade)
```bash
opencode
```

---

## 🛡️ Segurança e Governança

- **Permissão de Leitura:** Livre em todo o repositório.
- **Permissão de Escrita:** Exige apresentação prévia do plano de alteração e aprovação do usuário.
- **Segredos:** É estritamente proibido realizar commit de senhas, tokens de API, chaves SSH ou credenciais no repositório.

---

<p align="center">
  <i>Desenvolvido por Bruno César Medeiros Siqueira & Archimedes 🏛️</i>
</p>
