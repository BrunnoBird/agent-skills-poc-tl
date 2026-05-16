# Gestão de Estado

**Propósito:** Memória persistente entre sessões — decisões, bloqueadores, aprendizados.

## Estrutura

**Saída:** `.specs/project/STATE.md`

```markdown
# Estado

**Última Atualização:** [timestamp ISO]
**Trabalho Atual:** [Nome da Feature] - [Identificador da Tarefa]

---

## Decisões Recentes (Últimos 60 dias)

### AD-[NNN]: [Título da decisão] ([data])

**Decisão:** [O que foi decidido]
**Razão:** [Por que essa escolha]
**Trade-off:** [O que foi sacrificado]
**Impacto:** [Como isso afeta a implementação]

### AD-[NNN]: [Título da decisão] ([data])

[Mesma estrutura]

---

## Bloqueadores Ativos

### B-[NNN]: [Descrição do bloqueador]

**Descoberto:** [Data]
**Impacto:** [Severidade e escopo]
**Contorno:** [Solução temporária se disponível]
**Resolução:** [Caminho para correção permanente]

---

## Lições Aprendidas

### L-[NNN]: [Descrição do aprendizado]

**Contexto:** [Situação que ocorreu]
**Problema:** [O que deu errado]
**Solução:** [Como foi resolvido]
**Prevém:** [O que este conhecimento previne no futuro]

---

## Tarefas Rápidas Concluídas

| #   | Descrição             | Data   | Commit | Status   |
| --- | ---------------------- | ------ | ------ | -------- |
| 001 | [Descrição da tarefa]  | [data] | [hash] | ✅ Feito |

---

## Ideias Adiadas

Ideias capturadas durante o trabalho que pertencem a features ou fases futuras. Evita desvio de escopo enquanto preserva boas ideias.

- [ ] [Descrição da ideia] — Capturada durante: [feature/fase]
- [ ] [Descrição da ideia] — Capturada durante: [feature/fase]

---

## Todos

Capture pensamentos em andamento e itens de ação que não cabem nas tarefas ativas.

- [ ] [TODO: item de ação]
- [ ] [TODO: item de ação]
```

## Quando Atualizar

| Evento                                  | Ação                                      |
| --------------------------------------- | ----------------------------------------- |
| Escolha arquitetural significativa      | Adicionar AD-[NNN]                        |
| Implementação bloqueada                 | Adicionar B-[NNN]                         |
| Descoberta/aprendizado importante       | Adicionar L-[NNN]                         |
| Tarefa rápida concluída                 | Adicionar linha na tabela Tarefas Rápidas |
| Desvio de escopo capturado              | Adicionar em Ideias Adiadas               |
| Pensamento em andamento                 | Adicionar em Todos                        |
| Fim de sessão                           | Atualizar "Última Atualização" + "Trabalho Atual" |

## Gestão de Tamanho (Estratégia Híbrida)

**Zonas:**

- 🟢 <7k tokens: Nenhuma ação
- 🟡 7-10k tokens: Nota no rodapé "STATE.md em [X]k. Limpeza recomendada."
- 🔴 >10k tokens: Prompt ativo "STATE.md crítico ([X]k). Limpar agora?"

**Processo de limpeza:**

- Mover decisões >60 dias para STATE-ARCHIVE.md
- Manter apenas bloqueadores ativos
- Preservar aprendizados recentes (<60 dias)

**Validação:**

- Decisões têm razão clara?
- Bloqueadores incluem caminho de resolução?
- Aprendizados são acionáveis?

---

## Preferências

Rastrear estado comportamental voltado ao usuário no STATE.md:

```markdown
## Preferências

**Dica de Modelo Exibida:** [data ISO ou "nunca"]
```

**Atualizar quando:**

| Evento                               | Ação                                    |
| ------------------------------------ | --------------------------------------- |
| Primeira dica de modelo fornecida    | Definir data                            |
| Usuário reconhece/descarta           | Manter data (não repetir)               |

Isso previne sugestões repetitivas enquanto mantém comportamento natural e útil.
