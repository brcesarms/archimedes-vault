# 📊 benchmarks/ — Benchmarks do Projeto

> **Objetivo:** Métricas de desempenho de modelos LLM e scripts  
> **Responsável:** J.A.R.V.I.S.  
> **Última atualização:** 2026-09-08

---

## 📋 Estrutura

| Pasta | Conteúdo |
|-------|----------|
| `resultados/` | Arquivos JSON com métricas de benchmark |
| `HISTORICO.md` | Histórico de benchmarks ao longo do tempo |
| `BENCHMARKS.md` | Documentação dos benchmarks disponíveis |

---

## 🧪 Benchmarks Disponíveis

| Benchmark | Arquivo | Descrição |
|-----------|---------|-----------|
| Qwen3 Coder 30B | `qwen3-coder_30b.json` | Velocidade e memory usage |
| Qwen3.6 27B | `qwen3.6_27b.json` | Velocidade e memory usage |
| Qwen2.5 Coder 7B | `qwen2.5-coder_7b.json` | Velocidade e memory usage |

---

## 🚀 Como Rodar Benchmark

```bash
cd ~/archimedes-vault/guia-ia-local/scripts
./benchmark-moe.sh
```

Isso gera resultados em `guia-ia-local/benchmarks/resultados/`.

---

## 📊 Métricas Coletadas

| Métrica | Descrição |
|---------|-----------|
| **Warmup Time** | Tempo até o modelo estabilizar |
| **First Token Latency** | Tempo até o primeiro token |
| **Tokens/Second** | Velocidade de geração |
| **Memory Usage** | Uso de RAM em MB |
| **Disk Usage** | Uso de disco em MB |
| **Context Window** | Tamanho do contexto (tokens) |

---

## 📈 Como Analisar Resultados

### Via Terminal
```bash
cat guia-ia-local/benchmarks/resultados/qwen3-coder_30b.json | jq '.metrics'
```

### Via Markdown
```markdown
| Modelo | Tokens/Second | Memory (MB) |
|--------|---------------|-------------|
| Qwen3 Coder 30B | 24.5 | 14,200 |
| GPT-OSS 20B | 21.3 | 9,800 |
```

---

## 🔗 Fontes

- 📊 [guia-ia-local/benchmarks/HISTORICO.md](./HISTORICO.md)
- 📊 [guia-ia-local/benchmarks/BENCHMARKS.md](./BENCHMARKS.md)
- 🧪 [guia-ia-local/scripts/benchmark-moe.sh](../scripts/benchmark-moe.sh)

---

*Doc gerado por 🦾 J.A.R.V.I.S. em 2026-09-08*  
*Versão: 1.0.0 — Benchmarks*
