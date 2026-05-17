# Kit SDD — Português-BR

Kit mínimo para aplicar **Spec-Driven Development (SDD)** nos seus projetos.
Compatível com **Claude Code CLI** e **Devin CLI**. Zero dependências externas — só copiar e usar.

---

## O que é SDD?

SDD (Desenvolvimento Orientado a Especificação) organiza o trabalho em 4 fases adaptativas:

```
┌─────────────┐   ┌────────┐   ┌─────────┐   ┌─────────┐
│  ESPECIFICAR │ → │ DESIGN │ → │ TAREFAS │ → │ EXECUTAR│
└─────────────┘   └────────┘   └─────────┘   └─────────┘
    obrigatório     opcional*    opcional*     obrigatório

* O agente pula automaticamente quando o escopo não justifica
```

**Princípio central:** A complexidade determina a profundidade — não uma pipeline fixa.

| Escopo | Descrição | Fases usadas |
|--------|-----------|---------------|
| **Pequeno** | ≤3 arquivos, uma frase | Modo rápido (pula tudo) |
| **Médio** | Feature clara, <10 tarefas | Especificar + Executar |
| **Grande** | Múltiplos componentes | Todas as 4 fases |
| **Complexo** | Ambiguidade, domínio novo | Todas + discussão de áreas cinzas |

---

## Skills Incluídos

### 1. `sdd-planejamento` — Core do SDD

O núcleo da metodologia. Cobre as 4 fases, memória persistente entre sessões, quebra atômica de tarefas, rastreabilidade de requisitos e suporte a projetos novos e existentes.

**Use quando:** Iniciar projeto, planejar feature, implementar com verificação, pausar/retomar trabalho.

**Comandos em PT-BR:**
```
inicializar projeto
mapear codebase
especificar feature [nome]
discutir feature
design
tarefas
implementar
validar
correção rápida: [descrição]
pausar trabalho
retomar trabalho
```

---

### 2. `navegador-codebase` — Exploração de Código

Navegador metódico para codebases desconhecidos. Investiga antes de agir, executa com precisão cirúrgica, mantém base de conhecimento em `.notebook/` que cresce entre sessões.

**Use quando:** Entender código existente, investigar bugs, mapear fluxos, antes de especificar mudanças em projetos existentes.

**Comandos em PT-BR:**
```
explorar codebase
navegar código
investigar [módulo/área]
entender estrutura de [X]
como funciona [módulo/fluxo]?
investigue esse fluxo
mapear dependências
```

---

### 3. `diretrizes-codigo` — Princípios de Execução

4 princípios comportamentais que guiam qualquer implementação:
1. **Pense Antes de Codar** — Explicite suposições, não assuma
2. **Simplicidade Primeiro** — Código mínimo que resolve o problema
3. **Mudanças Cirúrgicas** — Toque só o que o task exige
4. **Execução Orientada a Objetivos** — Defina critérios de sucesso, itere até verificar

**Uso:** Ativo durante implementação de qualquer tarefa.

---

### 4. `desafiador-ideias` — Refinamento e Stress-Test

Desafia ideias, planos e decisões antes de commitar nelas. Aplica 5 modos de questionamento estruturado: exposição de suposições, contra-argumentação, pré-mortem, red team e auditoria de evidências.

**Use quando:** Quiser stress-test de uma spec, design ou decisão arquitetural antes de investir tempo nela.

**Comandos em PT-BR:**
```
desafie minha ideia
questione essa abordagem
faça um pré-mortem
ataque esse design
expõe as suposições
contra-argumente
```

---

## Fluxo Completo SDD

### Novo Projeto

```
1. Iniciando
   → "inicializar projeto"
   → Cria .specs/project/PROJECT.md + ROADMAP.md

2. Para cada feature:

   a. ESPECIFICAR (sempre)
      → "especificar feature: [nome da feature]"
      → Cria .specs/features/[nome]/spec.md
        com histórias de usuário, critérios de aceite e IDs rastreáveis

   b. DISCUTIR (opcional — só quando há áreas cinzas)
      → "discutir feature" ou o agente ativa automaticamente
      → Cria .specs/features/[nome]/context.md
        com decisões de layout, comportamento e interação

   c. DESIGN (opcional — só para features grandes/complexas)
      → "design"
      → Cria .specs/features/[nome]/design.md
        com arquitetura, componentes, modelos de dados

   d. TAREFAS (opcional — só quando há >3 passos ou dependências)
      → "tarefas"
      → Cria .specs/features/[nome]/tasks.md
        com breakdown atômico, dependências e plano de paralelismo

   e. EXECUTAR (sempre)
      → "implementar"
      → Implementa tarefa por tarefa com verificação + commit atômico

   f. VALIDAR (ao final ou sob demanda)
      → "validar"
      → Verifica contra spec + UAT interativo (se feature voltada ao usuário)
```

### Projeto Existente (Brownfield)

```
1. "mapear codebase"
   → Cria 7 docs em .specs/codebase/:
     STACK.md, ARCHITECTURE.md, CONVENTIONS.md,
     STRUCTURE.md, TESTING.md, INTEGRATIONS.md, CONCERNS.md

2. "inicializar projeto"
   → Cria PROJECT.md + ROADMAP.md

3. Para cada feature → mesmo fluxo adaptativo acima
   (o skill usa navegador-codebase automaticamente para exploração)
```

### Tarefa Rápida (Modo Rápido)

```
"correção rápida: [descrição em uma frase]"
→ Direto para implementação, sem cerimônia de spec/design/tasks
→ Regra: ≤3 arquivos, descrição em uma frase
```

---

## Estrutura de Arquivos Criada pelo SDD

```
.specs/
├── project/
│   ├── PROJECT.md      # Visão e objetivos do projeto
│   ├── ROADMAP.md      # Features e marcos
│   └── STATE.md        # Memória persistente: decisões, blockers, ideias
├── codebase/           # Análise brownfield (projetos existentes)
│   ├── STACK.md
│   ├── ARCHITECTURE.md
│   ├── CONVENTIONS.md
│   ├── STRUCTURE.md
│   ├── TESTING.md
│   ├── INTEGRATIONS.md
│   └── CONCERNS.md
├── features/
│   └── [nome-da-feature]/
│       ├── spec.md     # Requisitos com IDs rastreáveis
│       ├── context.md  # Decisões de comportamento/UI
│       ├── design.md   # Arquitetura e componentes
│       └── tasks.md    # Tarefas atômicas com verificação
└── quick/
    └── NNN-slug/
        ├── TASK.md
        └── SUMMARY.md
```

---

## Compatibilidade

| Agente | Pasta de Skills (projeto) | Pasta Global |
|--------|--------------------------|---------------|
| **Claude Code CLI** | `.claude/skills/` | `~/.claude/skills/` |
| **Devin CLI** | `.devin/skills/` | `~/.config/devin/skills/` |

Os mesmos arquivos SKILL.md funcionam nos dois agentes — só muda a pasta de destino.

Veja [INSTALACAO.md](INSTALACAO.md) para instruções detalhadas.

---

## Dicas de Uso

- **Fale em PT-BR** com o agente — os triggers estão configurados em português
- **O agente dimensiona automaticamente** — não precisa escolher a profundidade manualmente
- **STATE.md é sua memória** — consulte para ver decisões de sessões anteriores
- **Use `navegador-codebase` antes de especificar** em projetos existentes
- **Use `desafiador-ideias` antes de commitar** em um design ou decisão importante
- **Modo rápido para bugs simples** — não force o pipeline completo em fixes triviais
