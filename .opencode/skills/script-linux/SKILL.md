---
name: script-linux
description: Criação de scripts bash para Linux no estilo das convenções do J.A.R.V.I.S.. Use ao criar, editar ou revisar qualquer script .sh — aplica shebang, set flags, comentários descritivos, emojis nos logs, chmod +x e verificação de exit code. Dispara ao ouvir "criar script", "script bash", "automação", ".sh".
compatibility: opencode
metadata:
  audience: ia-local
  workflow: scripts
---

# 🐧 Scripts Linux do J.A.R.V.I.S.

Ao criar ou editar scripts bash para este cofre, siga sempre as convenções abaixo.

## 📍 Onde salvar os scripts

- **Manutenção do sistema** (backup, sync, deploy, automação do cofre) → `guia-ia-local/scripts/linux/`
- **Windows** → `guia-ia-local/scripts/windows/`
- **Templates** → `guia-ia-local/scripts/templates/`
- ⚠️ Scripts de **estudo/conteúdo** NÃO vão aqui — vão em `t.i/` ou `concurseiro/` (submódulos)

## 📜 Estrutura obrigatória

Todo script deve começar com:

```bash
#!/bin/bash
set -euo pipefail
```

## 💬 Comentários descritivos

- Incluir **comentários descritivos no início** explicando o que o script faz
- Usar comentários em português (pt-BR)
- Sempre que possível, seguir as convenções do AGENTS.md (não adicionar comentários desnecessários em código trivial)

## 🎨 Emojis nos logs de saída

Use emojis para dar feedback visual no terminal:

```bash
echo "✅ Sucesso! Modelo alterado."
echo "⚠️ Atenção: diretório não encontrado."
echo "❌ Erro: Ollama não está respondendo."
echo "🔍 Verificando..."
echo "📋 Listando arquivos..."
echo "🎯 Arquivo criado em: /caminho/arquivo.md"
```

## 🛡️ Verificação de exit code

Sempre verificar se os comandos tiveram sucesso:

```bash
if [ $? -ne 0 ]; then
    echo "✖ Operação falhou. Erro: $?"
    exit 1
fi
```

## ⚙️ Checklist antes de entregar

1. [ ] Shebang `#!/bin/bash`
2. [ ] `set -euo pipefail`
3. [ ] Comentários descritivos no início
4. [ ] Emojis nos logs (✅ ⚠️ ❌ 🔍 📋 🎯)
5. [ ] Verificação de exit code
6. [ ] `chmod +x` para tornar executável
7. [ ] Testado (rodar uma vez antes de confirmar sucesso)
8. [ ] `bash -n` passou (sintaxe)
9. [ ] `shellcheck` limpo (se instalado)

## 🚨 Erros comuns a evitar (já encontrados no cofre!)

> ⚡ **Antes de entregar um script, confira cada item** — esses erros já quebraram scripts reais:

| # | Erro | Correção |
|---|------|----------|
| 1 | `omarchy` agrupado com Ubuntu/apt | Omarchy é **Arch-based** — usar grupo `arch\|manjaro\|omarchy` com `pacman` |
| 2 | Aspas duplas aninhadas (`echo "a "b" c"`) | Escapar `\"` ou usar aspas simples |
| 3 | Argumento inválido aceito em silêncio | Validar com `case` + `--help` + exit ≠ 0 |
| 4 | Escrever no `.bashrc` sem checar duplicata | `grep -qF` antes de `>>` (idempotência) |
| 5 | `grep -q "$item"` colidindo com prefixos | Match exato: `awk '{print $1}' \| grep -qxF` |
| 6 | `sleep 2` esperando serviço subir | Loop de healthcheck com timeout (ex: `curl /api/tags`) |
| 7 | Citar arquivos que não existem nas mensagens | Conferir com `ls`/`glob` os nomes reais |
| 8 | Instalar docker-compose v1 p/ config v2 | Verificar versão do compose vs uso (`docker compose` = plugin v2) |

## 🐚 Verificação com ShellCheck (recomendado)

```bash
command -v shellcheck >/dev/null 2>&1 && shellcheck script.sh || echo "ℹ️ Instale: sudo pacman -S shellcheck"
```

> Se shellcheck **não estiver instalado**, avise o usuário — é a melhor rede de segurança para scripts bash.

### 📚 Tratamento de achados (regra de ouro)

> **NUNCA ignore um aviso — ou corrija, ou documente com `# shellcheck disable=`**

| Código | Significado | Tratamento |
|--------|-------------|------------|
| `SC2034` | Variável morta (declarada, nunca usada) | 🔧 Corrigir: remover ou usar |
| `SC2016` | `$VAR` em aspas simples que parece não expandir | 🧾 Suprimir se intencional, com comentário |
| `SC1091` | `. arquivo-externo` (ex: `/etc/os-release`) | 🧾 Suprimir — é padrão válido |

**Exemplo correto de supressão com documentação:**
```bash
# shellcheck disable=SC2016 # intencional: $HOME expande quando .bashrc rodar
echo 'export PATH="$HOME/.opencode/bin:$PATH"' >> "$HOME/.bashrc"
```

---

## 🔗 Fontes

- 📄 Convenções definidas em: [`AGENTS.md`](../../../AGENTS.md)
- 🩺 Varredura completa de erros: [`revisar-scripts`](../revisar-scripts/SKILL.md)
- 🐚 Documentação oficial: [ShellCheck](https://www.shellcheck.net/)
