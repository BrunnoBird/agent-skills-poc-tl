# Especificar

**Objetivo**: Capturar O QUÊ construir com requisitos testáveis e rastreáveis.

Se a feature tiver áreas cinzas ambíguas (múltiplas abordagens válidas para comportamento voltado ao usuário), o agente vai automaticamente acionar o processo de [discussão de áreas cinzas](discutir.md) dentro desta fase. Para features claras e bem definidas, vai direto para a próxima fase.

## Processo

### 1. Esclarecer Requisitos

Você é um parceiro de raciocínio, não um entrevistador. Comece aberto — deixe o usuário descarregar o modelo mental. Siga a energia: o que ele enfatizar, aprofunde nisso.

Pergunte de forma conversacional (não como checklist):

- "Qual problema você está resolvendo?"
- "Quem é o usuário e qual é a dor dele?"
- "Como é o sucesso?"

Se necessário:

- "Quais são as restrições (tempo, tecnologia, recursos)?"
- "O que está explicitamente fora de escopo?"

**Desafie a vagueza.** Nunca aceite respostas nebulosas. "Bom" quer dizer o quê? "Usuários" quer dizer quem? "Simples" quer dizer como? Torne o abstrato concreto: "Me mostre usando isso." "Como isso realmente parece?"

**Saiba quando parar.** Quando entender o que estão construindo, por quê, para quem e como é o feito — ofereça prosseguir.

### 2. Capturar Histórias de Usuário com Prioridades

**P1 = MVP** (precisa ser entregue), **P2** (deveria ter), **P3** (seria bom ter)

Cada história DEVE ser **independentemente testável** — você pode implementar e demonstrar apenas aquela história.

### 3. Escrever Critérios de Aceite

Use o formato **QUANDO/ENTÃO/DEVERÁ** — é preciso e testável:

- QUANDO [evento/ação] ENTÃO [sistema] DEVERÁ [resposta/comportamento]

---

## Template: `.specs/[feature]/spec.md`

```markdown
# Especificação: [Nome da Feature]

## Declaração do Problema

[Descreva o problema em 2-3 frases. Qual dor estamos resolvendo? Por quê agora?]

## Objetivos

- [ ] [Objetivo primário com resultado mensurável]
- [ ] [Objetivo secundário com resultado mensurável]

## Fora de Escopo

Explicitamente excluído. Documentado para evitar scope creep.

| Feature | Motivo |
| --- | --- |
| [Feature X] | [Por que foi excluída] |
| [Feature Y] | [Por que foi excluída] |

---

## Histórias de Usuário

### P1: [Título da História] ⭐ MVP

**História de Usuário**: Como [papel], quero [capacidade] para que [benefício].

**Por que P1**: [Por que isso é crítico para o MVP]

**Critérios de Aceite**:

1. QUANDO [ação/evento do usuário] ENTÃO o sistema DEVERÁ [comportamento esperado]
2. QUANDO [ação/evento do usuário] ENTÃO o sistema DEVERÁ [comportamento esperado]
3. QUANDO [caso extremo] ENTÃO o sistema DEVERÁ [tratamento gracioso]

**Teste Independente**: [Como verificar que esta história funciona sozinha]

---

### P2: [Título da História]

**História de Usuário**: Como [papel], quero [capacidade] para que [benefício].

**Por que P2**: [Por que não é MVP mas é importante]

**Critérios de Aceite**:

1. QUANDO [evento] ENTÃO o sistema DEVERÁ [comportamento]
2. QUANDO [evento] ENTÃO o sistema DEVERÁ [comportamento]

**Teste Independente**: [Como verificar]

---

### P3: [Título da História]

**História de Usuário**: Como [papel], quero [capacidade] para que [benefício].

**Por que P3**: [Por que é um nice-to-have]

**Critérios de Aceite**:

1. QUANDO [evento] ENTÃO o sistema DEVERÁ [comportamento]

---

## Casos Extremos

- QUANDO [condição de fronteira] ENTÃO o sistema DEVERÁ [comportamento]
- QUANDO [cenário de erro] ENTÃO o sistema DEVERÁ [tratamento gracioso]
- QUANDO [input inesperado] ENTÃO o sistema DEVERÁ [resposta de validação]

---

## Rastreabilidade de Requisitos

Cada requisito recebe um ID único para rastreamento em design, tarefas e validação.

| ID do Requisito | História | Fase | Status |
| --- | --- | --- | --- |
| [FEAT]-01 | P1: [História] | Design | Pendente |
| [FEAT]-02 | P1: [História] | Design | Pendente |
| [FEAT]-03 | P2: [História] | - | Pendente |

**Formato do ID:** `[CATEGORIA]-[NÚMERO]` (ex: `AUTH-01`, `CART-03`, `NOTIF-02`)

**Valores de Status:** Pendente → Em Design → Em Tarefas → Implementando → Verificado

---

## Critérios de Sucesso

Como sabemos que a feature foi bem-sucedida:

- [ ] [Resultado mensurável - ex: "Usuário consegue completar X em < 2 minutos"]
- [ ] [Resultado mensurável - ex: "Zero erros no cenário Y"]
```

---

## Dicas

- **P1 = Fatia Vertical** — Uma feature completa e demonstrável, não apenas backend ou frontend
- **QUANDO/ENTÃO é código** — Se não consegue escrever como teste, reescreva
- **IDs de Requisito são obrigatórios** — Cada história mapeia para IDs rastreáveis
- **Casos extremos importam** — O que quebra? O que fica vazio? O que é muito grande?
- **Fora de Escopo evita scope creep** — Se não está aqui, não será construído
- **Confirme antes de Discutir** — O usuário deve aprovar a spec antes de avançar
