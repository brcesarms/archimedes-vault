---
name: bancada-execucao
description: Execução padronizada do fluxo de bancada via orquestrador Python. Use quando o usuário pedir "bancada", "executar bancada", "inventário de máquina", "backup forense", "preparar formatação", "rodar orquestrador bancada", "manifesto de cliente" ou quando precisar coletar inventário Windows, fazer backup robocopy ou gerar manifesto pré-formatação via SSH.
compatibility: opencode
metadata:
  audience: ia-local
  workflow: automacao
---

# 🏗️ Execução do Projeto Bancada

> **Objetivo:** padronizar a execução do fluxo de bancada (inventário técnico + backup robocopy + manifesto) via orquestrador Python em `~/projetos/projeto-bancada/`.
> **Testado em:** 2026-09-11 — estrutura implementada e testes internos (parse JSON + manifesto) ✅

## 📍 Localização do Projeto

```text
/home/brn/projetos/projeto-bancada/
├── scripts/python/orquestrador.py      <-- Orquestrador principal
├── scripts/powershell/inventario.ps1   <-- Inventário JSON (Etapa 1)
├── scripts/powershell/backup-robocopy.ps1 <-- Backup por usuário (Etapa 2)
├── templates/MANIFESTO_TEMPLATE.md     <-- Modelo do manifesto
└── manifests/                          <-- Manifestos gerados (gitignored 🛡️)
```

> 📖 Detalhes completos: `docs/instrucoes.md` dentro do projeto.

## 🚦 Pré-requisitos (verificar antes de começar)

1. **Pasta `~/projetos/projeto-bancada/` existe** — se não, clonar:
   ```bash
   git clone git@github.com:brcesarms/projeto-bancada.git ~/projetos/projeto-bancada
   ```
2. **Python + paramiko** instalados:
   ```bash
   python3 -c "import paramiko" || pip install paramiko
   ```
3. **Chave SSH** configurada na máquina alvo Windows (OpenSSH Server ativo).
4. **Máquina alvo documentada/confirmada** pelo usuário (nunca conectar host desconhecido).

## 🧾 Dados necessários do usuário

| Dado | Flag | Obrigatório |
| :--- | :--- | :--- |
| IP/hostname da máquina | `--host` | ✅ |
| Usuário Windows | `--usuario` | ✅ |
| Nome do cliente | `--cliente` | ✅ |
| Storage central (UNC) | `--destino` | ⚠️ se omitir, pula backup |
| Caminho da chave | `--chave` | opt (padrão `~/.ssh/id_ed25519`) |

> Se faltar algum dado obrigatório → **PEDIR ao usuário** antes de executar (não inventar host).

## 📋 Fluxo de Execução (passos mecânicos)

### Passo 1 — Confirmar ambiente local

```bash
ls ~/projetos/projeto-bancada/scripts/python/orquestrador.py
python3 -c "import paramiko" && echo OK
```

### Passo 2 — Rodar o orquestrador

```bash
python3 ~/projetos/projeto-bancada/scripts/python/orquestrador.py \
  --host <IP> \
  --usuario <USUARIO> \
  --cliente <CLIENTE> \
  --destino '\\storage-central\Bancada\<CLIENTE>' \
  --chave ~/.ssh/id_ed25519
```

> ⚠️ **Caminho UNC:** usar aspas simples ou escape duplo (`\\\\`) — o shell interpreta contrabarras.
> ⚠️ Executar a partir de `~/projetos/projeto-bancada/` (o script resolve caminhos relativos ao projeto).

### Passo 3 — Verificar saída (não confiar só no relatório!)

- ✅ Inventário: `✔ Inventário coletado: <HOSTNAME> ...`
- ✅ Backup: `✔ Backup concluído: X pastas ok, Y com falha`
- ✅ Manifesto: `✔ Manifesto gerado: .../manifests/MANIFESTO_<CLIENTE>_<DATA>.md`

**Verificação independente (obrigatória):**
```bash
ls -la ~/projetos/projeto-bancada/manifests/MANIFESTO_<CLIENTE>_*.md
wc -l ~/projetos/projeto-bancada/manifests/MANIFESTO_<CLIENTE>_*.md
```

### Passo 4 — Reportar ao usuário

Resumo em pt-BR com emojis: hostname, nº de usuários, nº de softwares, pastas copiadas, falhas (se houver), caminho do manifesto.

## ⚠️ Armadilhas conhecidas

| ⚠️ Armadilha | ❌ Errado | ✅ Certo |
|--------------|----------|----------|
| Host não confirmado | Conectar a IP adivinhado | Pedir IP/host ao usuário |
| Caminho UNC no bash | `--destino '\\nas\Bancada\X'` com aspas erradas | Aspas simples OU `\\\\` no Python |
| Inventário vazio | Assumir que parseou | Verificar saída; reportar `#falha` se JSON vazio |
| Exit code robocopy >= 8 | Reportar sucesso | Marcar falha de cópia no manifesto |
| Manifesto com dados reais | Commitar em repo público | `manifests/` é gitignored — manter lá |
| `--destino` ausente | Esperar backup | OK — orquestrador pula backup (comportamento documentado) |

## 📌 Regras

- 🔒 **Segurança:** nunca conectar host não documentado; nunca expor chave OEM/credenciais no chat
- 🛡️ **Manifestos reais:** ficam apenas em `manifests/` local (gitignored) — NUNCA commit/push
- ✅ **Verificação independente:** conferir manifesto com `ls`/`wc` — relatório de saída não é evidência
- 🏷️ **Falha:** inventário vazio, backup com exit >= 8 sem registro → tag `#falha` + parar
- 📄 **Logs:** podem conter hostnames — não commitar (`logs/` gitignored)

---

## 🔗 Fontes

- 📖 Projeto Bancada (fora do vault): `~/projetos/projeto-bancada/docs/instrucoes.md`
- [Convenção SSH](../../convencoes/convencoes-ssh.md)
- [Convenção de Projetos](../../convencoes/convencoes-projetos.md)