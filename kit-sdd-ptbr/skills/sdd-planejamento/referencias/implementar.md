# Executar

**Objetivo**: Implementar UMA tarefa de cada vez. Mudanças cirúrgicas. Verificar. Commit. Repetir.

Aqui é onde o código é escrito. Cada tarefa segue o mesmo ciclo: planejar → implementar → verificar → commit. Verificação está embutida em cada tarefa, não é uma fase separada.

---

## OBRIGATÓRIO: Antes de Iniciar Qualquer Implementação

**Leia [principios-codigo.md](principios-codigo.md) e declare:**

1. **Suposições** - O que estou assumindo? Alguma incerteza?
2. **Arquivos a tocar** - Liste APENAS os arquivos que esta tarefa requer
3. **Critérios de sucesso** - Como verificarei que isso funciona?

⚠️ **Não prossiga sem declarar esses itens explicitamente.**

---

## Processo

**Contexto de sub-agente:** Quando esta tarefa é executada por um sub-agente, o sub-agente recebe a definição da tarefa, princípios de codificação, TESTING.md e contexto relevante de spec/design. Todos os passos abaixo se aplicam igualmente seja rodando no contexto principal ou em um sub-agente.

### 0. Listar Passos Atômicos (OBRIGATÓRIO quando a fase Tarefas foi pulada)

Se não há `tasks.md` para esta feature, DEVE listar passos atômicos antes de escrever qualquer código.

```
## Plano de Execução

1. [Passo] → arquivos: [lista] → verificar: [como] → commit: [mensagem]
2. [Passo] → arquivos: [lista] → verificar: [como] → commit: [mensagem]
3. [Passo] → arquivos: [lista] → verificar: [como] → commit: [mensagem]
```

**Cada passo deve ser:**

- UM entregvel (um componente, uma função, um endpoint, uma mudança de arquivo)
- Independentemente verificável (pode provar que funciona antes de seguir)
- Independentemente committable (tem seu próprio commit atômico de git)

Se listar os passos revelar >5 passos ou dependências complexas, PARE e crie um `tarefas.md` formal. A fase Tarefas foi erroneamente pulada.

### 1. Escolher Tarefa

Do tasks.md (se existir) ou do plano de execução acima. O usuário especifica ("implemente T3") ou sugira a próxima disponível.

### 2. Verificar Dependências

Se tasks.md existir, verifique dependências. Se usar plano inline, siga a ordem listada.

❌ Se bloqueado: "T3 depende de T2 que não está concluído. Devo fazer T2 primeiro?"

### 3. Declarar Plano de Implementação

Antes de escrever código:

```
Arquivos: [lista]
Abordagem: [breve descrição]
Sucesso: [como verificar]
```

### 4. Escrever Testes Primeiro (RED)

Se a tarefa inclui testes:

1. Escreva o(s) arquivo(s) de teste ANTES de escrever qualquer implementação
2. Testes devem codificar o comportamento esperado dos critérios "Pronto quando" da tarefa
3. Rode o comando de teste — confirme que testes FALHAM (estado RED)
4. Se testes passam antes da implementação existir, os testes são fracos demais — reescreva-os

**Restrições:**

- Testes definem comportamento correto independentemente da implementação
- Cada critério de aceite do "Pronto quando" mapeia para pelo menos uma asserção de teste
- Casos extremos da spec.md que se aplicam a esta tarefa ganham casos de teste também

Se a tarefa NÃO inclui testes (ex: só entidade, só config), pule para o Passo 4b.

### 4b. Implementar (GREEN)

Escreva a implementação mínima necessária para satisfazer os critérios de sucesso da tarefa.

**RESTRIÇÕES ABSOLUTAS:**

- NÃO modifique testes escritos no Passo 4. Os testes são a spec — a implementação se conforma a eles.
- NÃO enfraça assertions (torná-las menos específicas para passar mais facilmente)
- NÃO delete ou pule casos de teste
- NÃO use mecanismos skip/disable/pending do framework de testes para contornar testes falhando
- Código mínimo para passar — guarde melhorias estruturais para uma tarefa de refatoração

Se um teste está genuinamente errado (testa o comportamento errado conforme a spec), PARE e pergunte ao usuário antes de modificá-lo. Nunca mude um teste silenciosamente.

Siga [principios-codigo.md](principios-codigo.md):

- Código mais simples que funciona
- Toque APENAS os arquivos listados
- Sem scope creep

### 5. Gate Check (VERIFICAR)

Rode o comando de gate check da definição da tarefa. OBRIGATÓRIO — não "se aplicável".

1. Consulte o comando para o nível de Gate da tarefa (quick/full/build) na seção Comandos de Gate Check do TESTING.md, depois rode-o
2. Código de saída diferente de zero = PARE. Corrija a falha. Rode novamente. Não prossiga até verde.
3. Confirme que a contagem de testes corresponde ao esperado (nenhum teste foi silenciosamente deletado ou pulado)

**Gates por nível (de TESTING.md):**

| A tarefa inclui | Nível de Gate | O que roda |
| --- | --- | --- |
| Só testes unitários | Quick | Comando de teste unitário |
| Testes E2E ou integração | Full | Comandos de unitário + E2E |
| Última tarefa de uma fase | Build | Build + lint + todos os testes |
| Sem testes (config, entidades, etc) | Build | Só build + lint |

### 6. Revisão Pós-Gate

Após o gate check passar:

1. Verifique contagem de testes: Há pelo menos tantos casos de teste quanto antes? (evita deleção silenciosa)
2. Verifique se não há SPEC_DEVIATION: Se a implementação divergiu da spec/design, adicione um marcador:

```
// SPEC_DEVIATION: [o que divergiu]
// Motivo: [por que o desvio foi necessário]
```

3. Verificação rápida de complexidade: "Um engenheiro sênior sinalizaria isso como complicado demais?"
   - Sim → Simplifique, rode o gate novamente
   - Não → Prossiga para o commit

### 7. Commit Atômico de Git

Cada tarefa recebe seu próprio commit imediatamente após a verificação. Nunca agrupe múltiplas tarefas em um commit.

**Formato ([Conventional Commits 1.0.0](https://www.conventionalcommits.org/en/v1.0.0/)):**

```
<tipo>(<escopo>): <descrição>

[corpo opcional]

[rodapé(s) opcional(is)]
```

**Tipos:**

| Tipo | Quando usar |
| --- | --- |
| `feat` | Nova feature ou capacidade |
| `fix` | Correção de bug |
| `refactor` | Mudança de código que nem corrige bug nem adiciona feature |
| `docs` | Só documentação |
| `test` | Adicionando ou corrigindo testes |
| `style` | Formatação, ponto-e-vírgula faltando, etc. (sem mudança de código) |
| `perf` | Melhoria de performance |
| `build` | Sistema de build ou dependências externas |
| `ci` | Arquivos e scripts de configuração de CI |
| `chore` | Tarefas de manutenção que não modificam src ou arquivos de teste |

**Escopo:** Nome da feature ou área do módulo, minúsculo, ex: `auth`, `cart`, `api`

**Regras de descrição:**

- Modo imperativo ("adiciona", não "adicionado" ou "adicionando")
- Primeira letra minúscula
- Sem ponto no final
- Complete a frase: "Se aplicado, este commit irá _[sua descrição]_"

**Exemplos:**

```
feat(auth): adiciona validação de email no formulário de login
```

```
fix(cart): evita quantidade negativa ao decrementar item
```

```
refactor(api): extrai lógica de refresh de token para serviço

Move refresh de token do handler inline para AuthTokenService dedicado
para reuso em múltiplos endpoints.
```

### 8. Guarda-Chuva de Escopo

Durante a implementação, você notará coisas que poderiam ser melhoradas, refatoradas ou adicionadas. **Não aja sobre elas.** Em vez disso:

- Se é um bug: anote no STATE.md como blocker ou use o modo rápido
- Se é uma melhoria: anote no STATE.md em "Ideias Adiadas" ou "Lições Aprendidas"
- Se está relacionado à tarefa atual: inclua só se estiver nos critérios "Pronto quando"

**A heurística:** "Isso está na minha definição de tarefa?" Se não, não toque.

### 9. Atualizar Status da Tarefa

Marque a tarefa como completa no tasks.md. Atualize a rastreabilidade de requisitos no spec.md se IDs de requisito são usados.

---

## Dicas

- **Uma tarefa de cada vez** — Foco previne erros
- **Reuso economiza tokens** — Copie padrões, não reinvente
- **Verifique antes do commit** — Valide todos os critérios, depois commit
- **Permaneça cirúrgico** — Toque só o necessário
- **Commit por tarefa** — Histórico limpo de git habilita bisect e rollback
- **Nunca "enquanto estou aqui"** — Scope creep durante implementação é o assassino #1 da qualidade
- **Aprenda com os erros** — Se algo der errado, adicione uma Lição Aprendida ao STATE.md
