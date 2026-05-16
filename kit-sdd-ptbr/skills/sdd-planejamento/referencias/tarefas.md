# Tarefas

**Objetivo**: Quebrar em tarefas GRANULARES e ATÔMICAS. Dependências claras. Ferramentas certas. Plano de execução paralela.

**Pule esta fase quando:** Há ≤3 passos óbvios. Nesse caso, as tarefas são implícitas — vá direto para Executar e liste-as inline no plano de implementação.

## Por que Tarefas Granulares?

| Tarefa Vaga (RUIM) | Tarefas Granulares (BOM) |
| --- | --- |
| "Criar formulário" | T1: Criar componente de input de email |
| | T2: Adicionar função de validação de email |
| | T3: Criar botão de submit |
| | T4: Adicionar gerenciamento de estado do formulário |
| | T5: Conectar formulário à API |
| "Implementar auth" | T1: Criar formulário de login |
| | T2: Criar formulário de registro |
| | T3: Adicionar utilitário de armazenamento de token |
| | T4: Criar serviço de API de auth |
| | T5: Adicionar proteção de rotas |

**Benefícios do granular:**

- **Agentes não erram** — Foco único, sem ambiguidade
- **Fácil de testar** — Cada tarefa = um resultado verificável
- **Paralelizável** — Tarefas independentes rodam simultaneamente
- **Erros isolados** — Uma falha não bloqueia tudo

**Regra**: Uma tarefa = UMA dessas:

- Um componente
- Uma função
- Um endpoint de API
- Uma mudança de arquivo

---

## Processo

### 1. Revisar o Design

Leia `.specs/[feature]/design.md` antes de criar tarefas.

### 1.5. Carregar Matriz de Cobertura de Testes

Leia `.specs/codebase/TESTING.md` (se existir) antes de criar tarefas. A Matriz de Cobertura de Testes e a Avaliação de Paralelismo orientam duas decisões críticas:

**Testes co-localizados:** Cada tarefa que cria ou modifica uma camada de código com tipo de teste obrigatório DEVE incluir escrever/atualizar esses testes na mesma tarefa. Testes NÃO são tarefas separadas.

**Flags de paralelismo:** Cruce a Avaliação de Paralelismo ao marcar tarefas como `[P]`:

- Se o tipo de teste obrigatório de uma tarefa é "Paralelo-Safe: Não" → remova a flag `[P]`
- Se o tipo de teste obrigatório de uma tarefa é "Paralelo-Safe: Sim" → `[P]` é permitido

### 2. Quebrar em Tarefas Atômicas

**Tarefa = UM entregvel**. Exemplos:

- ✅ "Criar interface UserService" (um arquivo, um conceito)
- ❌ "Implementar gerenciamento de usuário" (vago demais, múltiplos arquivos)

### 3. Definir Dependências

O que DEVE ser feito antes que esta tarefa possa começar?

### 4. Criar Plano de Execução

Agrupe tarefas em fases. Identifique o que pode rodar em paralelo.

### 5. Validar Antes de Apresentar (OBRIGATÓRIO)

Antes de mostrar as tarefas ao usuário, rode TODAS as três verificações pré-aprovação. Não são opcionais.

**Verificação 1: Granularidade das Tarefas** — verifique que cada tarefa é atômica.

**Verificação 2: Cruzamento Diagrama-Definição** — verifique que o diagrama de execução corresponde ao campo `Depende de` de cada tarefa.

**Verificação 3: Validação de Co-localização de Testes** — verifique que o campo `Testes` de cada tarefa corresponde à matriz de cobertura do TESTING.md.

Apresente ambas as tabelas junto com as tarefas. Qualquer ❌ significa que DEVE reestruturar antes de apresentar.

### 6. PERGUNTAR sobre MCPs e Skills

**CRÍTICO**: Antes da execução, pergunte ao usuário:

> "Para cada tarefa, quais ferramentas devo usar?"
>
> **MCPs disponíveis**: [lista do projeto ou usuário]
> **Skills disponíveis**: [lista do projeto ou usuário]

---

## Template: `.specs/[feature]/tasks.md`

```markdown
# Tarefas: [Feature]

**Design**: `.specs/[feature]/design.md`
**Status**: Rascunho | Aprovado | Em Andamento | Concluído

---

## Plano de Execução

### Fase 1: Fundação (Sequencial)

Tarefas que devem ser feitas primeiro, em ordem.

T1 → T2 → T3

### Fase 2: Implementação Central (Paralelo OK)

Após a fundação, estas podem rodar em paralelo.

         ┌→ T4 ─┐
T3 ──┬→ T5 ─┬─→ T8
         └→ T6 ─┘
T7 ───────→

### Fase 3: Integração (Sequencial)

T8 → T9

---

## Detalhamento das Tarefas

### T1: [Criar Interface X]

**O quê**: [Uma frase: entregvel exato]
**Onde**: `src/caminho/para/arquivo.ts`
**Depende de**: Nenhuma
**Reutiliza**: `src/existente/BaseInterface.ts`
**Requisito**: [FEAT]-01

**Ferramentas**:

- MCP: `filesystem` (ou NENHUM)
- Skill: NENHUM

**Pronto quando**:

- [ ] Interface definida com todos os métodos do design
- [ ] Tipos exportados corretamente
- [ ] Sem erros de TypeScript

**Testes**: [unitário/e2e/integração/nenhum — da matriz de cobertura]
**Gate**: [quick/full/build — dos comandos de gate check]

---

### T2: [Implementar Serviço Y] [P]

**O quê**: [Entregvel exato]
**Onde**: `src/services/YService.ts`
**Depende de**: T1
**Reutiliza**: padrões de `src/services/BaseService.ts`

**Ferramentas**:

- MCP: `filesystem`, `context7`
- Skill: NENHUM

**Pronto quando**:

- [ ] Implementa a interface de T1
- [ ] Trata casos de erro do design
- [ ] Gate check passa: `[comando quick gate do TESTING.md]`
- [ ] Contagem de testes: [N] testes passam (sem deleções silenciosas)

**Testes**: unitário
**Gate**: quick

**Commit**: `feat([escopo]): [descrição]`
```

---

## Verificação de Granularidade das Tarefas

Antes de aprovar as tarefas, verifique se são granulares o suficiente:

| Tarefa | Escopo | Status |
| --- | --- | --- |
| T1: Criar input de email | 1 componente | ✅ Granular |
| T2: Adicionar função de validação | 1 função | ✅ Granular |
| T3: Criar formulário com todos os campos | 5+ componentes | ❌ Divida! |
| T4: Conectar à API | 1 função | ✅ Granular |

**Verificação de granularidade**:

- ✅ 1 componente / 1 função / 1 endpoint = Bom
- ⚠️ 2-3 coisas relacionadas no mesmo arquivo = OK se coeso
- ❌ Múltiplos componentes ou arquivos = DEVE dividir

---

## Dicas

- **[P] = Paralelo OK** — Marque tarefas que podem rodar simultaneamente
- **Reutiliza = Economizador de tokens** — Sempre referencie código existente
- **Ferramentas por tarefa** — MCPs e Skills evitam abordagens erradas
- **Dependências são gates** — Claro o que bloqueia o quê
- **Pronto quando = Testável** — Se não consegue verificar, reescreva
- **ID de Requisito = Rastreável** — Cada tarefa rastreia de volta a um requisito da spec
- **Um commit por tarefa** — Planeje o formato da mensagem de commit com antecedeência
