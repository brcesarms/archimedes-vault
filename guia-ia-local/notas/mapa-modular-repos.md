# 🗺️ Mapa Modular do Ecossistema Archimedes — repos conectados sem duplicação

> Criação: 2026-09-12 · Status: 🟢 ativo · Assunto: arquitetura modular dos repositórios de operação

## 🎯 Objetivo

Registrar o **mapa de conectividade** entre os repositórios externos do ecossistema Archimedes:
cada módulo tem **um dono e uma função única**, e as interseções acontecem **por referência de
caminho absoluto** — nunca por cópia de código.

## 🧩 Módulos e responsabilidades

| Repo | Papel | Motor principal | Dono de |
| :--- | :--- | :--- | :--- |
| 🏗️ [`archimedes-operator`](https://github.com/brcesarms/archimedes-operator) | Fluxo completo de bancada (inventário → backup → manifesto → pos/debloat) | Python + PowerShell | `orquestrador.py` · `inventario.ps1` · `setup-ssh-pri.ps1` · `menu.py` · template manifesto |
| 💾 [`archimedes-backup`](https://github.com/brcesarms/archimedes-backup) | Backup dedicado (standalone Linux+Windows) | Python + rsync + robocopy | `backup-robocopy.ps1` · `backup-navegador.ps1` · motores rsync · perfis |
| 🪟 [`archimedes-win11-setup`](https://github.com/brcesarms/archimedes-win11-setup) | Pós-instalação + desbloat do Windows 11 | PowerShell | `pos-instalacao.ps1` · `Win11Debloat.*` |

## 🔗 Conexões (referência por caminho absoluto — zero duplicação)

```text
┌─────────────────────────┐
│ 🏗️ archimedes-operator      │  ← único motor do FLUXO da bancada
│   orquestrador.py        │
└──────────┬──────────────┘
           │ referencia, NUNCA copia
           ▼
┌─────────────────────────┐    ┌──────────────────────────────┐
│ 💾 archimedes-backup     │    │ 🪟 archimedes-win11-setup     │
│   backup-robocopy.ps1    │    │    pos-instalacao.ps1         │
│   backup-navegador.ps1   │    │    Win11Debloat.*             │
│   linux/motor-rsync.sh   │    │                              │
└─────────────────────────┘    └──────────────────────────────┘
```

| Referência (dentro do `orquestrador.py` da bancada) | Caminho absoluto |
| :--- | :--- |
| 🔌 Backup — `backup-robocopy.ps1` | `~/projetos/archimedes-backup/windows/` |
| 🧩 Pós-instalação — `pos-instalacao.ps1` | `~/projetos/archimedes-win11-setup/windows/` |
| 🧹 Desbloat — `Win11Debloat.zip` | `~/projetos/archimedes-win11-setup/windows/` |

> 🧠 **O mesmo `backup-robocopy.ps1` é consumido por 2 orquestradores** — e isso é o padrão
> correto: um único script dono, múltiplos consumidores via caminho absoluto.

## 📌 Regras anti-duplicação (manutenção)

1. ❌ **Nunca copiar** scripts entre módulos — sempre referenciar por caminho absoluto.
2. ❌ **Nunca duplicar** funções que já existem em módulos donos (`comum/`, motores, etc.).
3. 🔄 Se faltar recurso → **melhorar o módulo dono**, depois atualizar skills/notas do vault.
4. 🔍 Verificar duplicações por hash (`md5sum`) após qualquer migração de arquivos.
5. 🗺️ **Sincronizar** esta nota/skills sempre que um módulo mudar de escopo.

## ✅ Verificação 2026-09-12

- ✔ Varredura MD5: **0 arquivos `.ps1` duplicados** e **0 `.sh` duplicados** entre os repos.
- ✔ Cada módulo possui **um único orquestrador** com escopo próprio.
- ✔ Referências absolutas conferidas no código da bancada (sem caminhos antigos).

## 🔗 Fontes

- [Nota: Archimedes Backup](./archimedes-backup.md)
- [Nota: Archimedes Win11-Setup](./archimedes-win11-setup.md)
- [Nota: Decisão de Arquitetura Python/PowerShell](./decisao-arquitetura-python-powershell-2026-09-11.md)
- [Nota: Arquitetura do Vault](./arquitetura-vault.md)
- [Nota: Servidor de Arquivos Proxmox](./servidor-arquivos-proxmox.md)
- [Nota: Proxmox GEEKOM — VM Windows](./proxmox-geekom-vm-windows.md)
- [Convenção de Projetos](../../.opencode/convencoes/convencoes-projetos.md)