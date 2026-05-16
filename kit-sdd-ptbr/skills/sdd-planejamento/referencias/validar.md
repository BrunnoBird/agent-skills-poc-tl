# Executar: Validar e Verificar

**Objetivo**: Verificar que a implementação atende à spec E aos princípios de codificação. Esta NÃO é uma fase separada — a verificação faz parte da conclusão de cada tarefa dentro do Executar.

**Dois níveis de verificação:**

1. **Verificação por tarefa (sempre):** Após implementar cada tarefa, verifique seus critérios "Pronto quando" antes do commit. Obrigatório e automático.

2. **Validação de feature (ao concluir ou sob demanda):** Após todas as tarefas de uma feature estarem concluídas, rode uma validação abrangente. Inclui verificação de critérios de aceite, revisão de qualidade de código e opcionalmente UAT interativo.

**UAT interativo é ativado quando:** A feature tem comportamento complexo voltado ao usuário onde o julgamento humano importa (fluxos de UI, padrões de interação, design visual). Para trabalho só de backend ou infraestrutura, verificações automatizadas são suficientes.

**Gatilho para validação explícita:** "Validar", "verificar trabalho", "UAT", "teste comigo", "mostre-me"

---

## Processo

### 1. Verificar Tarefas Concluídas

Passe pelo tasks.md:

- [ ] Todas as tarefas marcadas como concluídas?
- [ ] Alguma bloqueada ou parcial?

### 2. Verificar Critérios de Aceite

Para cada história de usuário em spec.md:

```markdown
### P1: [Título da História]

**Critérios de Aceite**:

1. QUANDO [X] ENTÃO [Y] → [PASSOU/FALHOU]
2. QUANDO [X] ENTÃO [Y] → [PASSOU/FALHOU]
```

### 3. Verificar Casos Extremos

Dos casos extremos de spec.md:

- [ ] [Caso extremo 1] tratado corretamente
- [ ] [Caso extremo 2] tratado corretamente

### 4. Rodar Gate Check de Nível Build (OBRIGATÓRIO)

Rode o gate check de nível Build do TESTING.md. NÃO é opcional.

1. Rode: `[comando build gate do TESTING.md]`
2. Código de saída diferente de zero = PARE. Não prossiga para Verificação de Qualidade de Código.
3. Registre resultados:
   - Total de testes: [N]
   - Passaram: [N]
   - Falharam: [lista]
   - Pulados: [lista — cada pulo deve ser justificado]

**Verificação de Integridade de Testes:**

- Compare a contagem atual de testes com a contagem antes desta feature ser implementada
- Se a contagem de testes DIMINUIU: investigue o motivo. Testes só devem ser deletados com justificativa explícita.

### 5. Verificação de Qualidade de Código (OBRIGATÓRIA)

Para cada arquivo alterado, verifique contra [principios-codigo.md](principios-codigo.md):

| Verificação | Passou? |
| --- | --- |
| Sem features além do que foi pedido | |
| Sem abstrações para código de uso único | |
| Sem "flexibilidade" desnecessária adicionada | |
| Só tocou arquivos necessários para a tarefa | |
| Não "melhorou" código não relacionado | |
| Corresponde aos padrões/estilo existentes | |
| Engenheiro sênior aprovaria? | |

❌ Qualquer "Não"? → Corrija antes de marcar como completo.

### 6. UAT Interativo (se feature voltada ao usuário)

Para cada entregvel testável, apresente um teste de cada vez:

```
Teste [N]: [Nome do Teste]

Esperado: [O que deve acontecer — específico e observável]

→ Isso funciona? Descreva o que você vê.
```

Aguarde a resposta do usuário:

| O usuário diz | Interpretar como |
| --- | --- |
| "sim", "passou", "funciona", "próximo" | ✅ Passou |
| "pular", "não consigo testar", "n/a" | ⏭️ Pulado |
| Qualquer outra coisa | ❌ Problema — registre literalmente |

**Inferência de severidade (nunca pergunte ao usuário a severidade):**

| Descrição do usuário contém | Severidade inferida |
| --- | --- |
| crash, erro, exceção, falha, quebrado | Bloqueador |
| não funciona, errado, faltando, não consigo | Maior |
| lento, estranho, fora do lugar, minor, pequeno | Menor |
| cor, fonte, espaçamento, alinhamento, visual | Cosmético |
| (pouco claro) | Maior (padrão) |

### 7. Gerar Planos de Correção (se problemas encontrados)

Para cada problema encontrado durante o UAT:

1. **Diagnosticar** — Analise o codebase para encontrar a causa raiz
2. **Criar tarefa de correção** — Escreva uma definição de tarefa com:
   - O quê: O fix específico
   - Onde: Caminhos de arquivo
   - Verificar: Como provar que o fix funciona
   - Pronto quando: Critérios de aceite para o fix
3. **Apresentar plano de fix** — Mostre todas as tarefas de fix ao usuário para aprovação

**Guarda-chuva:** Máximo de 3 iterações de diagnóstico por problema. Se a causa raiz não for encontrada após 3 tentativas, sinalize para investigação humana.

---

## Template de Relatório de Validação

```markdown
# Validação: [Feature]

**Data**: [AAAA-MM-DD]
**Spec**: `.specs/features/[feature]/spec.md`

---

## Conclusão das Tarefas

| Tarefa | Status | Notas |
| --- | --- | --- |
| T1 | ✅ Concluído | - |
| T2 | ✅ Concluído | - |
| T3 | ⚠️ Parcial | [Problema] |

---

## Validação das Histórias de Usuário

### P1: [Título da História] ⭐ MVP

| Critério | Resultado |
| --- | --- |
| QUANDO X ENTÃO Y | ✅ PASSOU |
| QUANDO A ENTÃO B | ✅ PASSOU |

**Status**: ✅ P1 Completo

---

## Testes

- **Comando gate**: [comando completo]
- **Resultado**: [X] passaram, [Y] falharam, [Z] pulados
- **Contagem de testes antes da feature**: [N]
- **Contagem de testes depois da feature**: [M]
- **Delta**: [+(M - N) novos testes]

---

## Atualização de Rastreabilidade de Requisitos

| Requisito | Status Anterior | Novo Status |
| --- | --- | --- |
| [FEAT]-01 | Implementando | ✅ Verificado |
| [FEAT]-02 | Implementando | ❌ Precisa de Correção |

---

## Sumário

**Geral**: ✅ Pronto | ⚠️ Problemas | ❌ Não Pronto

**O que funciona**: [Lista]

**Problemas encontrados**: [Problema 1: Como corrigir]

**Próximos passos**: [Ação]
```

---

## Dicas

- **P1 primeiro** — MVP deve funcionar antes de P2/P3
- **QUANDO/ENTÃO = Teste** — Cada critério é um caso de teste
- **Seja específico** — "Não funciona" não é útil
- **Recomende fixes** — Não só reporte problemas, crie tarefas de correção
- **Verificação de qualidade é obrigatória** — Não é opcional
- **Infira severidade** — Nunca pergunte ao usuário "quão grave é isso?"
- **Máximo 3 iterações de diagnóstico** — Evita loops de investigação infinitos
- **Atualize rastreabilidade** — Cada requisito verificado atualiza o status em spec.md
