# Modo Rápido

**Objetivo:** Executar tarefas pequenas e ad-hoc com os mesmos princípios de qualidade, mas sem a cerimônia completa do pipeline.

**Gatilho:** "Correção rápida", "Tarefa rápida", "Mudança pequena", "Bug fix", "Apenas faça X"

## Quando Usar

| Use o modo rápido              | Use o pipeline completo                    |
| ------------------------------ | ------------------------------------------ |
| Bug fixes com causa conhecida  | Novas features com múltiplas histórias     |
| Mudanças de configuração       | Mudanças arquiteturais                     |
| Ajustes pequenos de UI         | Features que requerem decisões de design   |
| Adicionar um campo/coluna      | Features com múltiplos componentes         |
| Scripts pontuais               | Qualquer coisa com escopo indefinido       |
| Atualizações de dependências   | Features que requerem histórias de usuário |

**Regra geral:** Se você pode descrevê-la em uma frase E ela toca ≤3 arquivos, é uma tarefa rápida.

## Processo

### 1. Descrever a Tarefa

Usuário fornece uma descrição clara em uma frase. Se vaga, peça especificações:

- ❌ "Corrija o login" → Pergunte: "O que está quebrado? O que deveria acontecer?"
- ✅ "Correção: botão de login retorna 401 porque o refresh de token pula verificação de expirado"

### 2. Verificação Pré-Implementação

Antes de escrever código, declare:

```
Tarefa Rápida: [descrição]
Arquivos: [liste APENAS os arquivos a tocar]
Abordagem: [uma frase]
Verificação: [como provar que funciona]
```

Obtenha aprovação do usuário antes de prosseguir. Se a verificação pré-implementação revelar que a tarefa é maior do que esperado (>3 arquivos, dependências incertas, decisões de design necessárias), recomende o pipeline completo.

### 3. Implementar

Siga [principios-codigo.md](principios-codigo.md):

- Código mais simples que funciona
- Toque APENAS os arquivos listados
- Sem desvio de escopo — corrija o que foi pedido, nada mais

### 4. Verificar

Execute a verificação do passo 2. Marque como concluído apenas após a verificação passar.

### 5. Commit

Commit atômico seguindo [Conventional Commits 1.0.0](https://www.conventionalcommits.org/en/v1.0.0/):

```
<tipo>(<escopo>): <descrição>
```

Use modo imperativo, minúsculas, sem ponto final. Veja [implementar.md](implementar.md) para a tabela completa de tipos.

Exemplos:

- `fix(auth): prevenir 401 no refresh de token`
- `feat(configuracoes): adicionar toggle de modo escuro`
- `chore(deps): atualizar eslint para v9`

### 6. Registrar

Atualize `.specs/project/STATE.md` com registro de tarefa rápida (veja seção Tarefas Rápidas em gestao-estado.md).

---

## Estrutura

Tarefas rápidas vivem separadamente das features planejadas:

```
.specs/
└── rapidas/
    └── NNN-slug/
        ├── TAREFA.md     # Descrição + verificação
        └── RESUMO.md     # O que foi feito + commit
```

**Template TAREFA.md:**

```markdown
# Tarefa Rápida NNN: [Título]

**Data:** [data]
**Status:** Concluída | Em Andamento | Bloqueada

## Descrição

[Uma frase: o que e por quê]

## Arquivos Modificados

- `src/caminho/para/arquivo.ts` — [o que mudou]
- `src/caminho/para/outro.ts` — [o que mudou]

## Verificação

- [ ] [Como verificar que funciona]
- [ ] [Comportamento esperado após a correção]

## Commit

`[hash]` — [mensagem de commit]
```

---

## Limites

- **Máx 3 arquivos** — Se mais, use o pipeline completo
- **Máx 1 hora** — Se mais, o escopo está errado
- **Sem decisões de design** — Se está escolhendo entre abordagens, use o pipeline completo
- **Sem novas dependências** — Adicionar pacotes precisa de revisão do pipeline completo
- **Registre tudo** — Mesmo tarefas rápidas têm commits e entradas no STATE.md

---

## Dicas

- **Rápido ≠ desleixado** — Os mesmos princípios de código se aplicam, apenas menos cerimônia
- **Na dúvida, vá completo** — Melhor planejar demais do que entregar código quebrado
- **Tarefas rápidas se acumulam** — Se você está fazendo 5+ tarefas rápidas para a mesma área, é uma feature que precisa de planejamento
- **Verifique antes de marcar concluído** — O objetivo é qualidade, mesmo para tarefas pequenas
