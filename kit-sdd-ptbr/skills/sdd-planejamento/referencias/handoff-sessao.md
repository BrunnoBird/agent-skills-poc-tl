# Handoff de Sessão

## Pausar Trabalho

**Gatilho:** "Pausar trabalho", "Encerrar sessão", "Criar handoff"

**Propósito:** Criar checkpoint do estado atual para retomada.

**Saída:** `.specs/HANDOFF.md` (sobrescreve o anterior)

**Meta de tamanho:** ~500 tokens

**Estrutura:**

```markdown
# Handoff

**Data:** [timestamp ISO]
**Feature:** [nome da feature]
**Tarefa:** [identificador da tarefa] - [status breve]

## Concluído ✓

- [Item de trabalho concluído]
- [Item de trabalho concluído]

## Em Andamento

- [Trabalho atual] ([porcentagem ou status])
- Localização específica: [arquivo:linha se aplicável]

## Pendente

- [Próximo passo imediato]
- [Passo seguinte]

## Bloqueadores

- [Descrição do bloqueador] - [impacto]

## Contexto

- Branch: [branch git se aplicável]
- Não commitado: [arquivos com mudanças]
- Decisões relacionadas: [referências ao STATE.md se aplicável]
```

**Instruções:**

- Focar em informações acionáveis para retomada
- Incluir referências específicas de arquivo/linha onde relevante
- Anotar mudanças não commitadas explicitamente
- Referenciar entradas relacionadas do STATE.md se aplicável

## Retomar Trabalho

**Gatilho:** "Retomar trabalho", "Continuar", "Carregar handoff"

**Processo:**

1. Carregar HANDOFF.md
2. Carregar STATE.md para contexto
3. Resumir posição atual
4. Propor próxima ação

**Padrão de resposta:**

- "Retomando [feature] em [tarefa]"
- "Concluído: [resumo]"
- "Próximo: [ação imediata]"
- "Continuar com [passo específico]?"
