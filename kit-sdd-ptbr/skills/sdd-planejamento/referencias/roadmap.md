# Criação de Roadmap

**Gatilho:** "Criar roadmap", "Planejar features", "Mapear fases do projeto"

## Processo

Com base no PROJECT.md, decompor a visão em:

- Marcos (incrementos entregáveis)
- Features (capacidades visíveis ao usuário)
- Rastreamento de status (planejado/em andamento/concluído)

## Saída: .specs/project/ROADMAP.md

**Estrutura:**

```markdown
# Roadmap

**Marco Atual:** [nome do marco]
**Status:** Planejando | Em Andamento | Concluído

---

## [Nome do Marco 1]

**Objetivo:** [O que torna este marco entregável]
**Meta:** [Data ou critérios de conclusão]

### Features

**[Nome da Feature]** - STATUS

- [Capacidade 1]
- [Capacidade 2]
- [Capacidade 3]

**[Nome da Feature]** - STATUS

- [Capacidade 1]
- [Capacidade 2]

---

## [Nome do Marco 2]

**Objetivo:** [O que este marco adiciona]

### Features

**[Nome da Feature]** - PLANEJADO
**[Nome da Feature]** - PLANEJADO

---

## Considerações Futuras

- [Potencial capacidade futura]
- [Potencial capacidade futura]
```

**Valores de status:**

- PLANEJADO: Não iniciado
- EM ANDAMENTO: Implementando atualmente
- CONCLUÍDO: Entregue e verificado

**Limite de tamanho:** 3.000 tokens (~1.800 palavras)

**Estratégia de atualização:**

- Marcar features PLANEJADO → EM ANDAMENTO ao iniciar
- Marcar EM ANDAMENTO → CONCLUÍDO após verificação
- Adicionar novos marcos conforme o projeto evolui

**Validação:**

- Cada marco tem resultado entregável claro?
- Features são capacidades visíveis ao usuário?
- Status reflete a realidade atual?
