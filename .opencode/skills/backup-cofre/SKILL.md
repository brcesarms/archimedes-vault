---
name: backup-cofre
description: Backup e restauração do Archimedes Vault. Use quando o usuário pedir "fazer backup", "backup do cofre", "snapshot", "salvar cópia", "restaurar cofre" ou "recuperar backup". Cria snapshots datados com verificação de integridade e restaura o cofre a partir deles.
compatibility: opencode
metadata:
  audience: ia-local
  workflow: gestao
---

# 🔄 Backup e Restauração do Archimedes Vault

O cofre é o segundo cérebro — proteja-o com backups regulares e restauração segura.

## 💾 Backup

### 1. Fluxo Git (primário)

O GitHub + submódulos **já é o backup lógico** do cofre. Antes de criar snapshots, garantir que o conteúdo esteja versionado:

```bash
git status --short          # mudanças não commitadas?
git -C ~/wikisidian/t.i status --short   # estudos pessoais também
```

> Se houver mudanças, commitar e publicar seguindo [`convencoes-git.md`](../../convencoes/convencoes-git.md). O snapshot abaixo é o backup offline **complementar**.

### 2. Snapshot automático (script)

Para rodar sem depender do agente (cron/systemd), use o script pronto:

```bash
~/archimedes-vault/guia-ia-local/scripts/linux/backup-cofre.sh
```

Cria snapshot datado, verifica integridade e aplica rotação (mantém 7 cópias).

### 3. Snapshot manual datado

Criar um arquivo tar.gz compactado com a data no nome. **O destino é FORA do cofre** (`$HOME/backups/`) para evitar backup aninhado:

> ⚠️ **PEGADINHA (não caia!):** se o backup for salvo DENTRO do cofre (ex: `utils/backups/`), cada backup aninha os anteriores → infla exponencialmente (105K → 11M → 31M...). **SEMPRE excluir backups aninhados e preferir destino fora do cofre.**

```bash
BACKUP_BASE="$HOME/backups/archimedes-vault"
mkdir -p "$BACKUP_BASE"
STAMP="$(date +%Y-%m-%d_%H%M%S)"
tar -czf "$BACKUP_BASE/archimedes-vault_$STAMP.tar.gz" \
    --exclude='archimedes-vault/guia-ia-local/utils/backups/*.tar.gz' \
    --exclude='archimedes-vault/.opencode/node_modules' \
    --exclude='archimedes-vault/.git' \
    -C "$HOME" archimedes-vault
```

> 💡 Também exclui `node_modules` (62M de dependência npm recuperável) — nunca deve pesar no backup do conteúdo.

### 4. Verificar integridade

Sempre conferir se o backup está íntegro antes de dar como concluído:

```bash
tar -tzf "$BACKUP_BASE/archimedes-vault_$STAMP.tar.gz" > /dev/null && echo "✅ Backup íntegro"
ls -lh "$BACKUP_BASE/archimedes-vault_$STAMP.tar.gz"
```

> ✅ Confirmação extra de que nada foi aninhado:
> ```bash
> [ "$(tar -tzf "$BACKUP_BASE/archimedes-vault_$STAMP.tar.gz" | grep -c 'backups/.*tar.gz')" -eq 0 ] && echo "✅ Sem backups aninhados"
> ```

### 5. Rotação (opcional)

- Manter backups recentes e remover os antigos, se o usuário quiser
- Perguntar antes de apagar backups antigos (nunca apagar sem confirmação)

## ♻️ Restauração

### 1. Localizar o backup

```bash
ls -lh "$HOME/backups/archimedes-vault/"*.tar.gz
```

### 2. Restaurar

⚠️ **Sempre confirmar com o usuário** antes de sobrescrever o cofre atual.

```bash
# Restaurar a partir de um backup específico
tar -xzf "$HOME/backups/archimedes-vault/archimedes-vault_<DATA>.tar.gz" -C "$HOME"
```

### 3. Verificar

- Confirmar que `AGENTS.md`, `opencode.json`, `setup.sh`, `ME.md` e `MY-SETUP.md` existem
- Confirmar que `.opencode/skills/` está presente (skills nunca se perdem)

## 📌 Regras

- 🔬 **Nunca** apagar backups sem perguntar
- 📁 Backups ficam em `$HOME/backups/archimedes-vault/` (FORA do cofre)
- 🏷️ Nome sempre com data/hora (`archimedes-vault_YYYY-MM-DD_HHMMSS.tar.gz`)
- ✅ Verificar integridade do backup após criar e após restaurar

---

## 🔗 Fontes

- 🖥️ Estrutura do cofre: [`AGENTS.md`](../../../AGENTS.md) (Estrutura do Vault)
