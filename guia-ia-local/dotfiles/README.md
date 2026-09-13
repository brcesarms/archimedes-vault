# 🐚 Dotfiles do Archimedes

> Configurações de shell e ambiente versionadas para **sobreviver a formatação**. Copiadas para `~` pelo `bootstrap.sh` ou manualmente.

## 📄 O que mora aqui

| Arquivo | Para que serve | Contém segredo? |
| :--- | :--- | :---: |
| `ssh-config` | Template de `~/.ssh/config` (aliases dos hosts) | ❌ Não |
| `.bashrc` *(opcional)* | Aliases e PATH extras (ex: opencode) | ❌ Não |
| `config.fish` *(opcional)* | Mesma ideia para Fish shell (Omarchy) | ❌ Não |

> ⚠️ **Nunca** coloque chaves privadas, tokens ou senhas nesta pasta — vão para o repositório!
> Restaure segredos pelo Bitwarden ou gere novos na máquina.

## 🚀 Como usar

```bash
# Automático (recomendado)
cd ~/archimedes-vault && ./bootstrap.sh

# Manual — copiar o SSH config
cp guia-ia-local/dotfiles/ssh-config ~/.ssh/config
chmod 600 ~/.ssh/config
```

## 🔒 Atualizar um host (ex: IP mudou)

1. Edite `ssh-config`
2. Commit + push (segue convenções git)
3. Rode `./bootstrap.sh` na(s) máquina(s) afetada(s)

---

## 🔗 Fontes

- 🔌 Convenção SSH: [`convencoes-ssh.md`](../../.opencode/convencoes/convencoes-ssh.md)
- 🏛️ Bootstrap: [`bootstrap.sh`](../../bootstrap.sh)