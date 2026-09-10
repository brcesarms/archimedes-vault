# 🔄 Learning Loop (Auto-Aprendizado)

> Carregue este arquivo ao final de sessões longas ou quando repetir padrões de tarefa.

## 🧠 Detecção de Padrão

- Observe se você está repetindo o mesmo tipo de tarefa
- Se executou **3+ vezes** o mesmo padrão, entre na fase **"distill"**
- Exemplos: criar notas no mesmo molde, mesmos comandos, mesmo fluxo de config

## 📝 Procedimento de Criação (Distill)

1. **Identifique** o padrão repetido e documente os passos
2. **Proponha ao Bruno**: "Bruno, estou repetindo [X]. Quer criar uma skill?"
3. **Se confirmado**, crie `.opencode/skills/<nome>/SKILL.md`
4. **Documente**: name, description, quando usar, procedimento, armadilhas, verificação
5. A skill fica **disponível imediatamente** nas próximas sessões

## 🔧 Auto-Melhoria de Skills

- Ao usar uma skill existente, observe se pode ser melhorada
- Se sim, **proponha a melhoria** ao Bruno
- Nunca altere sem confirmação explícita
- Regra: usado **5+ vezes** sem melhoria → está boa, não mexa

## 📊 Rastreamento de Padrões

Mantenha registro em `guia-ia-local/notas/padroes-detectados.md`:

| Padrão | Frequência | Skill Proposta? | Status |
|--------|-----------|-----------------|--------|
| Criar notas atômicas | 10x | ✅ `notas-atomicas` | Ativa |
| Auditar cofre | 3x | ✅ `auditar-cofre` | Ativa |

> **Dica:** Ao final de cada sessão longa, verifique se algum padrão se formou.

---

## 🔗 Fontes
- [Aprendizado contínuo de agentes LLM — arXiv](https://arxiv.org/abs/2406.10042)
