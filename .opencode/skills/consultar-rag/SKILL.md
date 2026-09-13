---
name: consultar-rag
description: Busca semântica local com chunking AST e LanceDB via archimedes-rag. Use quando o usuário pedir "buscar código", "achar função", "onde está implementado", "consultar rag" ou quando precisar de contexto cirúrgico de um projeto sem ler arquivos inteiros.
---

# 🔍 Skill: consultar-rag

## Memória Semântica Local com Chunking AST e LanceDB

O Archimedes utiliza o [`archimedes-rag`](https://github.com/brcesarms/archimedes-rag) para indexar repositórios de código via AST e executar buscas semânticas vetoriais ultra-rápidas, economizando até 95% de tokens em consultas.

## 📂 Localização do Motor

| Item | Caminho |
| :--- | :--- |
| CLI Global | `~/.local/bin/rag` ou `~/.local/bin/opencode-rag` |
| Indexador | `~/.local/bin/opencode-index` |
| Repositório | `~/projetos/archimedes-rag` |
| Cache Vetorial | `~/.cache/opencode_rag/projects/` |

## 📋 Como usar

1. **Consultar Contexto e Despachar Tarefa com RAG:**
   ```bash
   rag run "Como está implementado o backup do robocopy?"
   ```

2. **Listar Todos os Projetos Indexados:**
   ```bash
   rag list-projects
   ```

3. **Reindexar Manualmente um Projeto:**
   ```bash
   rag index --project-dir ~/projetos/archimedes-operator
   ```

4. **Verificar Status e Chunks do Projeto Atual:**
   ```bash
   rag info
   ```

## 🛡️ Diretrizes de Funcionamento
- 🧠 **AST Chunker:** Código Python é fatiado por classes e funções reais, mantendo integridade semântica.
- 🪝 **Zero-Overhead:** Os repositórios atualizam a base vetorial automaticamente via Git Hooks (`post-commit` e `post-merge`).
- ⚡ **Economia Extrema:** Injeta apenas os blocos relevantes (top-k) no prompt, evitando envio de arquivos inteiros.

---

## 🔗 Fontes

- [Repositório archimedes-rag](https://github.com/brcesarms/archimedes-rag)
- [Convenções de Projetos](../../convencoes/convencoes-projetos.md)
- [AGENTS.md](../../../AGENTS.md)
