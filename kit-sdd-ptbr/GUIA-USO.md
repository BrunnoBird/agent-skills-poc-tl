# Guia de Uso — Kit SDD em PT-BR

**Spec-Driven Development para equipes brasileiras**
Compatível com Claude Code CLI e Devin CLI. Zero dependências externas.

---

## Índice

1. [O que é SDD?](#1-o-que-é-sdd)
2. [Por que usar SDD?](#2-por-que-usar-sdd)
3. [Skills incluídos](#3-skills-incluídos)
4. [Fluxo completo](#4-fluxo-completo-sdd)
5. [Referência de comandos](#5-referência-de-comandos)
6. [Guia de instalação](#6-guia-de-instalação)
7. [Perguntas frequentes](#7-perguntas-frequentes)

---

## 1. O que é SDD?

**SDD (Spec-Driven Development)** — Desenvolvimento Orientado a Especificação — é uma metodologia de trabalho com agentes de IA que organiza o desenvolvimento em 4 fases adaptativas:

```
┌─────────────┐   ┌────────┐   ┌─────────┐   ┌─────────┐
│  ESPECIFICAR │ → │ DESIGN │ → │ TAREFAS │ → │ EXECUTAR│
└─────────────┘   └────────┘   └─────────┘   └─────────┘
    obrigatório     opcional*    opcional*     obrigatório

* O agente pula automaticamente quando o escopo não justifica
```

**Princípio central:** A complexidade determina a profundidade — não uma pipeline fixa.

| Escopo | Descrição | Fases usadas |
|--------|-----------|--------------|
| **Pequeno** | ≤3 arquivos, uma frase | Modo rápido (direto para execução) |
| **Médio** | Feature clara, menos de 10 tarefas | Especificar + Executar |
| **Grande** | Múltiplos componentes, dependências | Todas as 4 fases |
| **Complexo** | Ambiguidade, domínio novo | Todas + discussão de áreas cinzas |

---

## 2. Por que usar SDD?

Sem metodologia, agentes de IA tendem a:
- Implementar sem entender o que foi pedido
- Criar código difícil de manter (sem rastreabilidade)
- Perder contexto entre sessões
- Tomar decisões arquiteturais sem validação

Com SDD:
- **Rastreabilidade:** cada linha de código rastreia a um requisito com ID
- **Memória persistente:** STATE.md guarda decisões, blockers e ideias entre sessões
- **Tarefas atômicas:** cada tarefa tem critério de verificação — sem ambiguidade de "pronto"
- **Commits atômicos:** cada commit corresponde a uma tarefa verificada
- **Auto-dimensionamento:** sem cerimônia desnecessária para tarefas simples

---

## 3. Skills Incluídos

### `sdd-planejamento` — Core do SDD

O núcleo da metodologia. Cobre as 4 fases, memória persistente entre sessões, quebra atômica de tarefas e suporte a projetos novos e existentes.

**Quando usar:** Iniciar projeto, planejar feature, implementar com verificação, pausar/retomar trabalho.

---

### `navegador-codebase` — Exploração de Código

Navegador metódico para codebases desconhecidos. Investiga antes de agir, executa com precisão cirúrgica, mantém base de conhecimento em `.notebook/` que cresce entre sessões.

**Quando usar:** Entender código existente, investigar bugs, mapear fluxos — sempre antes de especificar mudanças em projetos existentes.

---

### `diretrizes-codigo` — Princípios de Execução

4 princípios comportamentais que guiam qualquer implementação:
1. **Pense Antes de Codar** — Explicite suposições, não assuma
2. **Simplicidade Primeiro** — Código mínimo que resolve o problema
3. **Mudanças Cirúrgicas** — Toque só o que a tarefa exige
4. **Execução Orientada a Objetivos** — Defina critérios de sucesso, itere até verificar

**Quando usar:** Ativo automaticamente durante qualquer implementação.

---

### `desafiador-ideias` — Stress-Test de Ideias

Desafia specs, designs e decisões antes de commitar nelas. Aplica 5 modos de questionamento estruturado.

**Quando usar:** Antes de investir tempo em uma abordagem complexa ou irreversível.

---

## 4. Fluxo Completo SDD

### Novo Projeto

```
1. "inicializar projeto"
   → Cria .specs/project/PROJECT.md + ROADMAP.md

2. Para cada feature:

   a. ESPECIFICAR (sempre)
      → "especificar feature: [nome]"
      → Cria .specs/features/[nome]/spec.md

   b. DISCUTIR (opcional — só quando há áreas cinzas)
      → "discutir feature"
      → Cria .specs/features/[nome]/context.md

   c. DESIGN (opcional — só para features grandes/complexas)
      → "design"
      → Cria .specs/features/[nome]/design.md

   d. TAREFAS (opcional — só quando há mais de 3 passos ou dependências)
      → "tarefas"
      → Cria .specs/features/[nome]/tasks.md

   e. EXECUTAR (sempre)
      → "implementar"
      → Implementa tarefa por tarefa com verificação + commit atômico

   f. VALIDAR (ao final ou sob demanda)
      → "validar"
```

### Projeto Existente (Brownfield)

```
1. "mapear codebase"
   → Cria 7 docs em .specs/codebase/

2. "inicializar projeto"
   → Cria PROJECT.md + ROADMAP.md

3. Para cada feature → mesmo fluxo adaptativo acima
```

### Tarefa Rápida

```
"correção rápida: [descrição em uma frase]"
→ Direto para implementação, sem cerimônia
→ Regra: ≤3 arquivos, descrição em uma frase
```

---

## 5. Referência de Comandos

### `sdd-planejamento`

| Comando | O que faz |
|---------|----------|
| `inicializar projeto` | Cria PROJECT.md e ROADMAP.md |
| `mapear codebase` | Analisa projeto existente (7 docs brownfield) |
| `especificar feature [nome]` | Inicia pipeline SDD com spec.md |
| `discutir feature` | Captura decisões de comportamento/UI |
| `design` | Cria documento de arquitetura |
| `tarefas` | Quebra feature em tarefas atômicas |
| `implementar` | Executa tarefas com verificação |
| `validar` | Verifica contra spec + UAT |
| `correção rápida: [desc]` | Bug fix sem cerimônia |
| `pausar trabalho` | Salva handoff para retomada |
| `retomar trabalho` | Carrega STATE.md e retoma |

### `navegador-codebase`

| Comando | O que faz |
|---------|----------|
| `explorar codebase` | Exploração geral do projeto |
| `navegar código` | Navegação estruturada |
| `investigar [módulo/área]` | Investigação focada em área específica |
| `entender estrutura de [X]` | Mapear estrutura de módulo/fluxo |
| `como funciona [módulo/fluxo]?` | Explicar funcionamento |
| `investigue esse fluxo` | Rastrear fluxo de dados/controle |
| `mapear dependências` | Identificar dependências e integrações |

### `desafiador-ideias`

| Comando | O que faz |
|---------|----------|
| `desafie minha ideia` | Questionamento estruturado completo |
| `questione essa abordagem` | Contra-argumentação |
| `faça um pré-mortem` | Projeção de falhas futuras |
| `ataque esse design` | Red team do design |
| `expõe as suposições` | Auditoria de premissas ocultas |

---

## 6. Guia de Instalação

### Sem npm — Copiar a pasta de skills

#### Para Claude Code CLI (projeto)

```bash
git clone --depth=1 \
  --branch=claude/extract-sdd-skills-o9hxv \
  https://github.com/brunnobird/agent-skills-poc-tl.git _agentskills_tmp

mkdir -p .claude/skills
cp -r _agentskills_tmp/kit-sdd-ptbr/skills/* .claude/skills/
cp _agentskills_tmp/kit-sdd-ptbr/AGENTS.md ./AGENTS.md
rm -rf _agentskills_tmp
```

Edite `AGENTS.md` na raiz do projeto com o stack e comandos reais.

#### Para Devin CLI (projeto)

```bash
git clone --depth=1 \
  --branch=claude/extract-sdd-skills-o9hxv \
  https://github.com/brunnobird/agent-skills-poc-tl.git _agentskills_tmp

mkdir -p .devin/skills
cp -r _agentskills_tmp/kit-sdd-ptbr/skills/* .devin/skills/
cp _agentskills_tmp/kit-sdd-ptbr/AGENTS.md ./AGENTS.md
rm -rf _agentskills_tmp
```

#### Para ambos ao mesmo tempo

```bash
git clone --depth=1 \
  --branch=claude/extract-sdd-skills-o9hxv \
  https://github.com/brunnobird/agent-skills-poc-tl.git _agentskills_tmp

mkdir -p .claude/skills .devin/skills
cp -r _agentskills_tmp/kit-sdd-ptbr/skills/* .claude/skills/
cp -r _agentskills_tmp/kit-sdd-ptbr/skills/* .devin/skills/
cp _agentskills_tmp/kit-sdd-ptbr/AGENTS.md ./AGENTS.md
rm -rf _agentskills_tmp
```

#### Instalação global (todos os projetos da máquina)

```bash
# Clone primeiro
git clone --depth=1 \
  --branch=claude/extract-sdd-skills-o9hxv \
  https://github.com/brunnobird/agent-skills-poc-tl.git _agentskills_tmp

# Claude Code global
mkdir -p ~/.claude/skills
cp -r _agentskills_tmp/kit-sdd-ptbr/skills/* ~/.claude/skills/

# Devin CLI global
mkdir -p ~/.config/devin/skills
cp -r _agentskills_tmp/kit-sdd-ptbr/skills/* ~/.config/devin/skills/

rm -rf _agentskills_tmp
```

### Verificar instalação

**Claude Code:**
```bash
ls .claude/skills/
# Deve mostrar: sdd-planejamento  navegador-codebase  diretrizes-codigo  desafiador-ideias
```

Abra o Claude Code CLI no projeto e digite: `especificar feature: teste`
O agente deve reconhecer o comando e iniciar o fluxo SDD.

**Devin CLI:**
```bash
ls .devin/skills/
```

### Compatibilidade por agente

| Agente | Pasta de Skills (projeto) | Pasta Global |
|--------|--------------------------|---------------|
| **Claude Code CLI** | `.claude/skills/` | `~/.claude/skills/` |
| **Devin CLI** | `.devin/skills/` | `~/.config/devin/skills/` |

Os mesmos arquivos SKILL.md funcionam nos dois agentes — só muda a pasta de destino.

---

## 7. Perguntas Frequentes

**P: Preciso do npm ou Node.js instalado?**
R: Não. O kit é apenas arquivos markdown. Nenhuma dependência de runtime.

**P: Posso usar em projetos Java/Python/.NET?**
R: Sim. O SDD é agnóstico de linguagem e framework. Edite o `AGENTS.md` com os comandos do seu stack.

**P: O que acontece se eu esquecer de usar o SDD numa feature?**
R: Nada quebra. Você pode iniciar o SDD em qualquer momento — inclusive depois de começar a implementar. Use `especificar feature` para retroativamente criar a spec do que está construindo.

**P: Preciso usar os 4 skills ou posso usar só o `sdd-planejamento`?**
R: Você pode usar apenas o `sdd-planejamento`. Os outros skills são complementares:
- `navegador-codebase` é especialmente valioso para projetos brownfield
- `diretrizes-codigo` entra automaticamente durante a execução
- `desafiador-ideias` é opcional, use quando quiser stress-test de uma ideia

**P: O `.notebook/` do `navegador-codebase` conflita com o `.specs/` do `sdd-planejamento`?**
R: Não. São complementares:
- `.specs/` é documentação formal de projeto/features (spec, design, tasks)
- `.notebook/` é inteligência informal sobre o codebase (fluxos descobertos, armadilhas, padrões)

**P: Posso adicionar os skills em projetos com git já iniciado?**
R: Sim. Adicione a pasta `.claude/skills/` (ou `.devin/skills/`) ao `.gitignore` se não quiser commitar os skills junto com o projeto, ou comite-os para que toda a equipe os tenha.

**P: O agente vai falar em PT-BR automaticamente?**
R: Sim. Os triggers estão configurados em PT-BR. Se você escrever em PT-BR, o agente responde em PT-BR.

---

*Kit SDD PT-BR — branch `claude/extract-sdd-skills-o9hxv` — brunnobird/agent-skills-poc-tl*
