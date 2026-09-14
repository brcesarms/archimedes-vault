---
name: notas-atomicas
description: Criação e edição de notas no estilo do Archimedes. Use quando for criar, editar ou organizar notas markdown neste cofre — aplica notas atômicas, emojis, links markdown relativos e seção de fontes. Dispara ao ouvir "criar nota", "anotar", "resumo", "to-do notes" e nomes como "nota atômica".
compatibility: opencode
metadata:
  audience: ia-local
  workflow: notas
---

# 🗒️ Notas Atômicas do Archimedes

Este cofre segue regras de escrita de notas. Ao criar ou editar qualquer nota, siga sempre estas convenções.

## 📍 Onde salvar cada nota

- **Manutenção do sistema** (lições, manutenção, propostas, health report) → `guia-ia-local/notas/`
- **Estudos de TI** → `~/wikisidian/t.i/` (pasta pessoal, repo brcesarms/t.i)
- **Concursos** → `~/wikisidian/concurseiro/` (pasta pessoal, repo brcesarms/concurseiro)
- ⚠️ Sempre coloque a nota no lugar certo — sistema ≠ conteúdo

## ⚛️ Princípio da Nota Atômica

Cada nota trata de **um único assunto, conceito ou regra**, de forma focada e direta.

- ❌ Não misturar vários temas em uma nota
- ✅ Uma nota = um assunto

## 📌 Regras de Nomenclatura

| Elemento | Regra |
|----------|-------|
| Título (dentro do arquivo) | Objetivo e descritivo, com emoji no H1 |
| Nome do arquivo | Kebab-case, minúsculas, sem acentos, **sem emojis** |
| Conexões | Notas nunca ficam isoladas — conecte com correlatas ou índice |

Exemplo de nome de arquivo: `docker.md`

## 🔗 Formato de Links

- ❌ **Proibido**: Wikilinks do Obsidian `[[Nome da Nota]]`
- ✅ **Obrigatório**: Links markdown com caminhos relativos
   - Mesma pasta: `[Nome da Nota](./nome-da-nota.md)`
   - Pasta diferente: `[Nome da Nota](../diretorio/nome-da-nota.md)`

## 🎨 Uso de Emojis

- Títulos H1 sempre com emoji: `# 🐳 Docker Básico`
- Cabeçalhos H2/H3 com emoji: `## 📦 Instalação`, `## ⚠️ Cuidados`
- Listas com emojis: `- ✅ Feito`, `- ⏳ Pendente`, `- ❌ Erro`
- Tabelas com emoji na primeira coluna

## 📚 Seção de Fontes

Toda nota criada ou editada deve terminar com:

```markdown
---

## 🔗 Fontes
- [Documentação Oficial do Docker](https://docs.docker.com)
```

## ✅ Checklist antes de salvar

1. [ ] Nome do arquivo em kebab-case, minúsculas, sem acentos, sem emojis
2. [ ] H1 com emoji
3. [ ] Um único assunto
4. [ ] Links markdown relativos (sem wikilinks)
5. [ ] Seção `## 🔗 Fontes` no final
6. [ ] Conectado com notas correlatas ou índice
