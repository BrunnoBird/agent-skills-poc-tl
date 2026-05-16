# Especificar: Discutir Áreas Cinzas

**Objetivo:** Capturar COMO o usuário imagina a feature quando a spec tem áreas ambíguas. Esta NÃO é uma fase separada — é ativada dentro de Especificar quando o agente detecta áreas cinzas que precisam de input do usuário.

**Gatilho:** Automaticamente quando áreas cinzas são detectadas durante a criação da spec, ou explicitamente via "discutir feature", "como isso deve funcionar?", "capturar contexto"

**Quando ativar (auto-detectar):** A spec contém comportamento voltado ao usuário que pode ir em várias direções E o usuário não expressou preferência. Se a spec é clara e inequívoca, pule completamente.

**Quando NÃO ativar:** Trabalho de infraestrutura, operações CRUD, contratos de API bem definidos, qualquer coisa onde o "como" é óbvio a partir do "o quê".

## Por que Esta Fase Existe

Especificações capturam O QUÊ construir. Design captura a arquitetura. Mas nenhum captura a visão do usuário para áreas ambíguas — preferências de layout, padrões de interação, estilo de tratamento de erros, tom de conteúdo. Sem isso, o agente adivinha. Com isso, o agente constrói o que o usuário realmente imaginou.

O output — `context.md` — alimenta diretamente Design e Tarefas:

- **Design lê** para saber quais decisões estão bloqueadas vs. flexíveis
- **Tarefas lê** para incluir comportamentos específicos nas definições de tarefa

## Processo

### 1. Analisar a Feature

Leia `.specs/features/[feature]/spec.md` e identifique o domínio:

| Domínio | Áreas cinzas para explorar |
| --- | --- |
| Algo que usuários **VÊEM** | Layout, densidade, interações, estados vazios, hierarquia visual |
| Algo que usuários **CHAMAM** (API) | Formato de resposta, erros, auth, versionamento, rate limiting |
| Algo que usuários **EXECUTAM** (CLI) | Formato de output, flags, modos, tratamento de erro, verbosidade |
| Algo que usuários **LEEM** | Estrutura, tom, profundidade, fluxo, navegação |
| Algo sendo **ORGANIZADO** | Critérios de agrupamento, nomenclatura, duplicatas, exceções |

Gere 3-4 áreas cinzas **específicas da feature**. Não categorias genéricas, mas decisões concretas para ESTA feature.

### 2. Apresentar Áreas Cinzas

Apresente a fronteira da feature (de spec.md) e as áreas cinzas ao usuário. Deixe-o escolher quais discutir.

### 3. Aprofundar Cada Área

Para cada área selecionada:

1. Faça 3-4 perguntas concretas com opções específicas (não categorias vagas)
2. Após as perguntas, verifique: "Mais sobre [area], ou seguimos?"
3. Se mais → faça 3-4 a mais, verifique novamente
4. Após todas as áreas → "Pronto para criar o contexto?"

**Design de perguntas:**

- Opções devem ser concretas ("Layout em card" não "Opção A")
- Cada resposta deve informar a próxima pergunta
- Inclua "Você decide" como opção quando razoável — captura a discrição do agente

### 4. Guarda-Chuva de Escopo (CRÍTICO)

A fronteira da feature de spec.md é **fixada**. A discussão esclarece COMO implementar, nunca SE adicionar novas capacidades.

**Permitido:** "Como os posts devem ser exibidos?" (esclarecendo ambiguidade)
**Não permitido:** "Devemos também adicionar comentários?" (nova capacidade)

Quando o usuário sugere scope creep: "Isso parece uma feature separada. Vou anotar nas Ideias Adiadas. De volta a [area atual]."

### 5. Escrever context.md

---

## Template: `.specs/features/[feature]/context.md`

```markdown
# Contexto: [Feature]

**Coletado:** [data]
**Spec:** `.specs/features/[feature]/spec.md`
**Status:** Pronto para design

---

## Fronteira da Feature

[Declaração clara do que esta feature entrega — a âncora de escopo de spec.md]

---

## Decisões de Implementação

### [Área 1 discutida]

- [Decisão específica tomada]
- [Outra decisão se aplicável]

### [Área 2 discutida]

- [Decisão específica tomada]

### Discrição do Agente

[Áreas onde o usuário disse explicitamente "você decide" — o agente tem flexibilidade aqui durante o design/implementação]

---

## Referências Específicas

[Momentos "quero como X", referências de produto, comportamentos específicos, padrões de interação mencionados durante a discussão]

[Se nenhum: "Sem requisitos específicos — aberto a abordagens padrão"]

---

## Ideias Adiadas

[Ideias que surgiram durante a discussão mas pertencem a outras features/fases. Capturadas aqui para não se perderem, mas explicitamente fora de escopo]

[Se nenhuma: "Nenhuma — discussão ficou dentro do escopo da feature"]
```

---

## Dicas

- **Decisões, não visão** — "Layout em cards com sombras sutis" é uma decisão. "Deve parecer moderno" não é.
- **Escopo é sagrado** — Ideias Adiadas captura scope creep sem perder as ideias
- **Usuário = visionario, Agente = construtor** — Pergunte sobre como imagina, não sobre implementação técnica
- **Não pergunte sobre:** Arquitetura técnica, performance, detalhes de implementação — isso é trabalho do Design
- **Confirme antes do Design** — O usuário aprova o context.md antes de avançar para a fase de design
