---
name: sdd-planejamento
description: Planejamento de projetos e features com 4 fases adaptativas — Especificar, Design, Tarefas, Executar. Dimensiona a profundidade pela complexidade automaticamente. Cria tarefas atômicas com critérios de verificação, commits atômicos, rastreabilidade de requisitos e memória persistente entre sessões. Agnóstico de stack. Use quando (1) Iniciar novos projetos, (2) Trabalhar em codebases existentes, (3) Planejar features, (4) Implementar com verificação e commits atômicos, (5) Tarefas ad-hoc rápidas, (6) Registrar decisões/blockers/ideias entre sessões, (7) Pausar/retomar trabalho. Ativado por: "inicializar projeto", "mapear codebase", "especificar feature", "discutir feature", "design", "tarefas", "implementar", "validar", "verificar trabalho", "UAT", "correção rápida", "tarefa rápida", "pausar trabalho", "retomar trabalho". NÃO use para análise de decomposição arquitetural ou documentos de design técnico.
license: CC-BY-4.0
metadata:
  author: Felipe Rodrigues - github.com/felipfr
  version: 2.0.0
  translated-to: pt-BR
---

# Desenvolvimento Orientado a Especificação

Planeje e implemente projetos com precisão. Tarefas granulares. Dependências claras. Ferramentas certas. Zero cerimônia desnecessária.

```
┌─────────────┐   ┌────────┐   ┌─────────┐   ┌─────────┐
│  ESPECIFICAR │ → │ DESIGN │ → │ TAREFAS │ → │ EXECUTAR│
└─────────────┘   └────────┘   └─────────┘   └─────────┘
   obrigatório     opcional*    opcional*     obrigatório

* O agente pula automaticamente quando o escopo não justifica
```

## Dimensionamento Automático: O Princípio Central

**A complexidade determina a profundidade, não uma pipeline fixa.** Antes de iniciar qualquer feature, avalie o escopo e aplique apenas o necessário:

| Escopo | O quê | Especificar | Design | Tarefas | Executar |
| --- | --- | --- | --- | --- | --- |
| **Pequeno** | ≤3 arquivos, uma frase | **Modo rápido** — pula pipeline | - | - | - |
| **Médio** | Feature clara, <10 tarefas | Spec (breve) | Pula — design inline | Pula — tarefas implícitas | Implementar + verificar |
| **Grande** | Feature multi-componente | Spec completo + IDs de requisito | Arquitetura + componentes | Breakdown completo + dependências | Implementar + verificar por tarefa |
| **Complexo** | Ambiguidade, domínio novo | Spec completo + [discussão de áreas cinzas](referencias/discutir.md) | [Pesquisa](referencias/design.md) + arquitetura | Breakdown + plano paralelo | Implementar + [UAT interativo](referencias/validar.md) |

**Regras:**

- **Especificar e Executar são sempre obrigatórios** — você sempre precisa saber O QUÊ e FAZER
- **Design é pulado** quando a mudança é direta (sem decisões arquiteturais, sem novos padrões)
- **Tarefas é pulado** quando há ≤3 passos óbvios (ficam implícitos no Executar)
- **Discussão é ativada dentro de Especificar** apenas quando o agente detecta áreas cinzas ambíguas
- **UAT interativo é ativado dentro de Executar** apenas para features com comportamento complexo voltado ao usuário
- **Modo rápido** é a via expressa — para bugs, mudanças de config e ajustes pequenos

**Válvula de segurança:** Mesmo quando Tarefas é pulado, Executar SEMPRE começa listando passos atômicos inline (veja [implementar.md](referencias/implementar.md)). Se essa listagem revelar >5 passos ou dependências complexas, PARE e crie um `tarefas.md` formal — a fase Tarefas foi erroneamente pulada.

## Estrutura do Projeto

```
.specs/
├── project/
│   ├── PROJECT.md      # Visão e objetivos
│   ├── ROADMAP.md      # Features e marcos
│   └── STATE.md        # Memória: decisões, blockers, lições, todos, ideias adiadas
├── codebase/           # Análise brownfield (projetos existentes)
│   ├── STACK.md
│   ├── ARCHITECTURE.md
│   ├── CONVENTIONS.md
│   ├── STRUCTURE.md
│   ├── TESTING.md
│   ├── INTEGRATIONS.md
│   └── CONCERNS.md
├── features/           # Especificações de features
│   └── [feature]/
│       ├── spec.md     # Requisitos com IDs rastreáveis
│       ├── context.md  # Decisões do usuário para áreas cinzas
│       ├── design.md   # Arquitetura e componentes (só para Grande/Complexo)
│       └── tasks.md    # Tarefas atômicas com verificação (só para Grande/Complexo)
└── quick/              # Tarefas ad-hoc (modo rápido)
    └── NNN-slug/
        ├── TASK.md
        └── SUMMARY.md
```

## Fluxo de Trabalho

**Novo projeto:**

1. Inicializar projeto → PROJECT.md + ROADMAP.md
2. Para cada feature → Especificar → (Design) → (Tarefas) → Executar (profundidade auto-dimensionada)

**Codebase existente:**

1. Mapear codebase → 7 docs brownfield
2. Inicializar projeto → PROJECT.md + ROADMAP.md
3. Para cada feature → mesmo fluxo adaptativo

**Modo rápido:** Descrever → Implementar → Verificar → Commit (para ≤3 arquivos, escopo de uma frase)

## Estratégia de Carregamento de Contexto

**Carga base (~15k tokens):**

- PROJECT.md (se existir)
- ROADMAP.md (quando planejando/trabalhando em features)
- STATE.md (memória persistente)

**Carregamento sob demanda:**

- Docs de codebase (quando trabalhando em projeto existente)
- CONCERNS.md (quando planejando features que tocam áreas sinalizadas, estimando risco ou modificando componentes frágeis)
- TESTING.md (quando criando tarefas ou executando — orienta tipo de teste e gate checks)
- spec.md (quando trabalhando em feature específica)
- context.md (quando fazendo design ou implementando a partir de decisões do usuário)
- design.md (quando implementando a partir do design)
- tasks.md (quando executando tarefas)

**Nunca carregar simultaneamente:**

- Múltiplas specs de features
- Múltiplos docs de arquitetura
- Documentos arquivados

**Meta:** <40k tokens de contexto total
**Reserva:** 160k+ tokens para trabalho, raciocínio, outputs
**Monitoramento:** Exibir status quando >40k (veja [limites-contexto.md](referencias/limites-contexto.md))

## Delegação a Sub-Agentes

Use sub-agentes (Task tool ou equivalente) para manter o contexto principal enxuto e habilitar execução paralela. O agente orquestrador planeja e coordena; sub-agentes fazem o trabalho pesado.

**Quando delegar a um sub-agente:**

| Atividade | Delegar? | Por quê |
|---|---|---|
| Pesquisa (fase de design, mapeamento brownfield) | Sim | Output de pesquisa é grande; só o resumo importa para o contexto principal |
| Implementar uma tarefa | Sim | Leituras de arquivo, edições, saída de testes consomem contexto |
| Tarefas paralelas `[P]` | Sim (uma por tarefa) | Única forma de executar tarefas em paralelo |
| Tarefas sequenciais sem `[P]` | Sim | Mantém artefatos de implementação fora do contexto principal |
| Planejamento, criação de tarefas, relatórios de validação | Não | Requerem o contexto acumulado completo para ser coerentes |
| Tarefas do modo rápido | Não | Pequenas demais para justificar o overhead |

**Contexto que cada sub-agente recebe:**

O agente orquestrador DEVE fornecer a cada sub-agente:
- A definição específica da tarefa do tasks.md
- Princípios de código do kit (`referencias/principios-codigo.md`)
- Convenções do projeto (`.specs/codebase/CONVENTIONS.md`), se já gerado via mapeamento brownfield
- TESTING.md, se existir
- Qualquer contexto de spec/design que a tarefa referencia

O sub-agente NÃO recebe: definições de outras tarefas, histórico de chat acumulado, relatórios de validação de outras tarefas ou STATE.md (a menos que a tarefa referencie explicitamente uma decisão/blocker).

**O que sub-agentes retornam:**

- Status: Completo | Bloqueado | Parcial
- Arquivos alterados: [lista]
- Resultado do gate check: [passou/falhou + contagem de testes]
- Marcadores SPEC_DEVIATION (se houver)
- Problemas encontrados (se houver)

O agente orquestrador usa isso para atualizar o status do tasks.md, rastreabilidade e decidir os próximos passos.

## Comandos

**Nível de projeto:**
| Padrão de Ativação | Referência |
|----------------|----------|
| Inicializar projeto, configurar projeto | [iniciar-projeto.md](referencias/iniciar-projeto.md) |
| Criar roadmap, planejar features | [roadmap.md](referencias/roadmap.md) |
| Mapear codebase, analisar código existente | [mapeamento-brownfield.md](referencias/mapeamento-brownfield.md) |
| Documentar preocupações, encontrar dívida técnica, o que é arriscado | [preocupacoes.md](referencias/preocupacoes.md) |
| Registrar decisão, logar blocker, adicionar todo | [gestao-estado.md](referencias/gestao-estado.md) |
| Pausar trabalho, encerrar sessão | [handoff-sessao.md](referencias/handoff-sessao.md) |
| Retomar trabalho, continuar | [handoff-sessao.md](referencias/handoff-sessao.md) |

**Nível de feature (auto-dimensionado):**
| Padrão de Ativação | Referência |
|----------------|----------|
| Especificar feature, definir requisitos | [especificar.md](referencias/especificar.md) |
| Discutir feature, capturar contexto, como isso deve funcionar | [discutir.md](referencias/discutir.md) |
| Design da feature, arquitetura | [design.md](referencias/design.md) |
| Quebrar em tarefas, criar tarefas | [tarefas.md](referencias/tarefas.md) |
| Implementar tarefa, construir, executar | [implementar.md](referencias/implementar.md) |
| Validar, verificar, testar, UAT, mostre-me | [validar.md](referencias/validar.md) |
| Correção rápida, tarefa rápida, mudança pequena, bug fix | [modo-rapido.md](referencias/modo-rapido.md) |

## Integrações com Outros Skills

Este skill coexiste com outros skills. Antes de tarefas específicas, verifique se skills complementares estão instalados e prefira-os quando disponíveis.

### Diagramas

Use blocos de código mermaid inline sempre que um diagrama ajudar a comunicar arquitetura ou fluxo. Não é necessário nenhum skill externo — o agente gera os blocos `mermaid` diretamente no documento.

### Exploração de Código → navegador-codebase

Sempre que o fluxo de trabalho exigir explorar ou descobrir coisas em um repositório existente (mapeamento brownfield, análise de reuso de código, identificação de padrões, rastreamento de dependências), **sempre** verifique se o skill `navegador-codebase` está instalado. Se estiver, delegue tarefas de exploração e navegação de código a ele. Se não estiver, use as ferramentas de análise de código disponíveis (veja [analise-codigo.md](referencias/analise-codigo.md)) e recomende a instalação (uma vez por sessão).

## Cadeia de Verificação de Conhecimento

Ao pesquisar, projetar ou tomar qualquer decisão técnica, siga esta cadeia em ordem estrita. Nunca pule etapas.

```
Passo 1: Codebase → verifique código, convenções e padrões já em uso
Passo 2: Docs do projeto → README, docs/, comentários inline, .specs/codebase/
Passo 3: Context7 MCP → resolva ID da biblioteca, consulte API/padrões atuais
Passo 4: Busca web → docs oficiais, fontes confiáveis, padrões da comunidade
Passo 5: Sinalizar como incerto → "Não tenho certeza sobre X — aqui está meu raciocínio, mas verifique"
```

**Regras:**

- Nunca pule para o Passo 5 se os Passos 1-4 estiverem disponíveis
- Passo 5 é SEMPRE sinalizado como incerto — nunca apresentado como fato
- **NUNCA assuma ou fabrique.** Se não conseguir encontrar uma resposta, diga "Não sei" ou "Não encontrei documentação para isso". Inventar APIs, padrões ou comportamentos causa falhas em cascata.

## Análise de Código

Use as ferramentas disponíveis com degradação graciosa. Veja [analise-codigo.md](referencias/analise-codigo.md).
