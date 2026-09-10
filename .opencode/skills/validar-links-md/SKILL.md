---
name: validar-links-md
description: Validação de links markdown em notas e arquivos do Archimedes Vault. Verifica se destinos de links relativos existem e detecta links quebrados.
---

# 🔗 Skill: validar-links-md

## Validação de Links em Markdown

Esta skill valida links markdown em arquivos do cofre.

## 📋 O que fazer

1. Buscar todos os links markdown `[Texto](caminho)` em um arquivo ou pasta
2. Verificar se o destino realmente existe
3. Listar links quebrados
4. Gerar relatório com status

## 📝 Resultado esperado

- Log de cada link com ✅ ou ❌
- Resumo final com quantidade de links quebrados
- Sugestão de ações se houver falhas

## 🔗 Fontes

- 📄 Processo definido em: [`AGENTS.md`](../../../AGENTS.md)
- 📁 Script original: `guia-ia-local/scripts/linux/validacoes/verificar-links-parado.sh`
