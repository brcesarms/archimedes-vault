# 📦 Archimedes Backup — repositório único de backups

> Criação: 2026-09-12 · Status: 🟢 ativo · Repo: [brcesarms/archimedes-backup](https://github.com/brcesarms/archimedes-backup)

## 🎯 Objetivo

Unir **todo backup do ecossistema** em um único repositório, sem duplicar código:

| Plataforma | Motor | Técnica |
| :--- | :--- | :--- |
| 🪟 Windows | `robocopy` | Cópia por usuário (Desktop/Documents/Downloads/Pictures) → share SMB |
| 🐧 Linux | `rsync` | Cópia block-level (`-aHX --partial --delete`) → via SSH |

Arquitetura **controller + agent**: Python só no orquestrador; motores **nativos** no alvo
(PowerShell no Windows, rsync no Linux).

## 📁 Estrutura

```text
~/projetos/archimedes-backup/
├── orquestrador.py           <-- CLI: --perfil / --novo-perfil / --lista-perfis / --dry-run
├── comum/                    <-- perfis.py · conexao.py (paramiko) · relatorio.py · tests/
├── config/perfis/            <-- Perfis de máquina (.conf) — exemplo-linux, exemplo-windows...
├── linux/                    <-- motor-rsync.sh · setup-ssh.sh · README
├── windows/                  <-- backup-robocopy.ps1 (migrado) · README
├── docs/instrucoes.md        <-- Manual completo
├── manifests/                <-- Manifestos gerados (gitignored 🛡️)
└── logs/                     <-- Logs de execução (gitignored 🛡️)
```

## 🔀 Relação com o projeto-bancada

- O `backup-robocopy.ps1` **saiu** de `projeto-bancada/scripts/powershell/` (2026-09-12).
- O `orquestrador.py` da bancada referencia **caminho absoluto** `~/projetos/archimedes-backup/windows/backup-robocopy.ps1` — sem duplicar código.

## 🔑 Perfis (config/perfis/*.conf)

```ini
[geral]
nome = omarchy-paula
plataforma = linux

[origem]
ssh_origem = paula@10.0.0.218       # vazio = origem local
caminho = /run/media/paula/BRUNO/
excluir = *.tmp,*.part

[destino]
ssh_destino = backup@10.0.0.4
caminho = /srv/arquivos/backup/omarchy-paula/
```

> `--novo-perfil` gera o esqueleto; edite e rode `--perfil <nome>`.

## 🛡️ Política de segurança (bancada)

- Ambiente confiável: host keys automáticas + senha via prompt (nunca salva).
- **Nunca** commitar senha/token/chave privada (`manifests/` e `logs/` gitignored).
- Fora da bancada → adotar chave obrigatória + `known_hosts`.

## ⚠️ Próximo passo conhecido

- Testar perfil real `omarchy-paula` (**SSH do Omarchy `10.0.0.218` precisa estar ativo** — porta 22 atualmente fechada).

## 🔗 Fontes

- [Repositório archimedes-backup](https://github.com/brcesarms/archimedes-backup)
- [Robocopy — Microsoft Learn](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/robocopy)
- [rsync man page](https://linux.die.net/man/1/rsync)