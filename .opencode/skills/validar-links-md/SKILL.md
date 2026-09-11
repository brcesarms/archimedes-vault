---
name: validar-links-md
description: Validação de links markdown em notas e arquivos do Archimedes Vault. Verifica se destinos de links relativos existem e detecta links quebrados.
---

# 🔗 Skill: validar-links-md

## Validação de Links em Markdown

Esta skill valida links markdown em arquivos do cofre usando o **script Python** com testes.

## 📋 O que fazer

1. **Ativar venv** (primeira vez: `python3 -m venv .venv && pip install -r requirements.txt`):
   ```bash
   cd ~/archimedes-vault/guia-ia-local/scripts/python
   source .venv/bin/activate
   ```

2. **Rodar o validador** (arquivo ou pasta, raiz padrão = cwd):
   ```bash
   python3 validar_links.py <arquivo_ou_pasta> [--raiz <dir_base>]
   ```

   Exemplos:
   ```bash
   # Validar uma pasta inteira
   python3 validar_links.py ~/archimedes-vault/guia-ia-local/notas
   # Validar todo o cofre
   python3 validar_links.py ~/archimedes-vault --raiz ~/archimedes-vault
   ```

3. **Interpretar o relatório**:
   - ✅ links que resolvem para destinos existentes
   - ❌ links quebrados (destino não existe) → listados com arquivo, linha e link
   - Ignorados: URLs externas (`http/https/ftp/mailto/www`), âncoras (`#...`), blocos de código e código inline

4. **Rodar os testes** (após alterar o script):
   ```bash
   python3 -m pytest tests/ -v
   ```

## 📝 Resultado esperado

- Log de cada link com ✅ ou ❌
- Resumo final com quantidade de links quebrados
- Exit code: `0` sem quebrados, `1` com quebrados, `2` caminho inválido

> 🧪 **Testes obrigatórios:** todo script Python novo em `scripts/python/` deve ter testes em `tests/` (ver skill `revisar-scripts` e nota `arquitetura-vault.md`).

## 🧠 Lições Aprendidas (auditoria 2026-09-11)

1. **Subagentes erram a profundidade de links relativos** — notas geradas por IA usavam padrões errados: `../AGENTS.md` (deveria ser `../../AGENTS.md` por estar em `notas/`), `./guia-ia-local/README.md` (deveria ser `../README.md`), `reestruturação` com cedilha (arquivo real é sem acento). **Sempre revalidar após gerar notas em lote.**
2. **Acentos/cedilhas quebram links silenciosamente** — o cofre usa `kebab-case` SEM acento; link com `ç` não resolve. Se o arquivo existe mas o validador aponta quebrado, confira acentuação do nome.
3. **Falso-positivos automáticos** — `node_modules`, curingas `*`/`?`, URLs externas, âncoras e code blocks são ignorados pelo script. **Não** corrigir esses links.
4. **Erros sistemáticos → correção em lote**: quando o MESMO padrão repete em vários arquivos (ex: `guia-ia-local/guia-ia-local`, `../.opencode/`), usar `git grep` para mapear e edições com `replaceAll` por arquivo — depois revalidar até 0.

## 🔗 Fontes

- 📄 Processo definido em: [`AGENTS.md`](../../../AGENTS.md)
- 🐍 Script: `guia-ia-local/scripts/python/validar_links.py` (módulo em `snake_case` por ser importável — PEP 8)
- 🧪 Testes: `guia-ia-local/scripts/python/tests/test_validar_links.py`
- 🗺️ Arquitetura: `guia-ia-local/notas/arquitetura-vault.md`
