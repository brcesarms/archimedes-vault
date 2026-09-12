---
name: motor-remoto
description: Reuso do motor Python do projeto-bancada para operações remotas (SSH/SFTP/inventário/backup/manifesto) sem duplicar código. Use quando o usuário pedir "operar máquina remota", "inventário remoto", "backup remoto", "rodar banco no vault" ou quando uma tarefa do vault exigir executar scripts PowerShell em outra máquina via SSH/SFTP. Apenas REFERENCIA o orquestrador do projeto-bancada por caminho absoluto — nunca copie o código.
---

# 🔌 Skill: motor-remoto

## Reutilizar o motor Python do projeto-bancada (sem duplicar)

O Archimedes usa **um único motor** para operações remotas: o orquestrador do `projeto-bancada`. O vault **não** possui cópia — apenas referencia o caminho absoluto.

## 📂 Localização do motor

| Item | Caminho |
| :--- | :--- |
| Orquestrador | `~/projetos/projeto-bancada/scripts/python/orquestrador.py` |
| Scripts base (inventário) | `~/projetos/projeto-bancada/scripts/powershell/` |
| Backup (robocopy) | `~/projetos/archimedes-backup/windows/` |
| Pós-instalação + Desbloat | `~/projetos/archimedes-after-install-win11/windows/` |
| Venv | `~/projetos/projeto-bancada/.venv` |

## 📋 Como usar

1. **Ativar venv** (dependência `paramiko`):
   ```bash
   source ~/projetos/projeto-bancada/.venv/bin/activate
   ```

2. **Executar o orquestrador** com os parâmetros da máquina alvo:
   ```bash
   python3 ~/projetos/projeto-bancada/scripts/python/orquestrador.py \
       --host <IP> --usuario <usuario> --chave ~/.ssh/id_ed25519 \
       --cliente "<NOME_CLIENTE>" \
       --destino '<CAMINHO_UNC_OU_LOCAL>'
   ```

3. **Exemplo real** (VM Windows — confirmar dados na nota `proxmox-geekom-vm-windows.md`):
   ```bash
   python3 ~/projetos/projeto-bancada/scripts/python/orquestrador.py \
       --host 10.0.0.217 --usuario brces \
       --cliente "pricila braga" \
       --destino 'C:\Backups\Bancada\pricila braga'
   ```

## 🚫 Regras

- ❌ **NUNCA copiar** `orquestrador.py` ou `.ps1` para dentro do vault.
- ❌ **NUNCA** inventar novas flags — usar exatamente a interface do orquestrador (`--host`, `--usuario`, `--chave`, `--cliente`, `--destino`, `--saida`).
- ✅ Se faltar recurso no motor, **melhorar o projeto-bancada** (README, testes e docs lá) — depois atualizar esta skill.
- ✅ Configurações de máquinas conhecidas ficam nas notas do vault (ex: `guia-ia-local/notas/proxmox-geekom-vm-windows.md`).

## 🔗 Fontes

- [Projeto bancada no GitHub](https://github.com/brcesarms/projeto-bancada)
- [Nota: Decisão de Arquitetura Python/PowerShell](../../../guia-ia-local/notas/decisao-arquitetura-python-powershell-2026-09-11.md)
- [Nota: Arquitetura do Vault](../../../guia-ia-local/notas/arquitetura-vault.md)
- [Nota: Proxmox GEEKOM — VM Windows](../../../guia-ia-local/notas/proxmox-geekom-vm-windows.md)