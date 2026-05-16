# Especificação do .notebook/

Leia este arquivo quando precisar criar ou atualizar notas durante a
fase de Debrief, ou quando precisar entender o formato do caderno
durante o Briefing.

## Estrutura

```
.notebook/
├── INDEX.md          # Sempre leia primeiro. Índice compacto de todas as notas.
├── fluxo-auth.md     # Arquivos de notas individuais — flat por padrão.
├── tratamento-erros.md
└── race-checkout.md
```

Notas começam flat na raiz do `.notebook/`. Quando o volume exceder
~15 notas, organize em subdiretórios por categoria:

```
.notebook/
├── INDEX.md
├── fluxos/
│   ├── fluxo-auth.md
│   └── fluxo-checkout.md
├── padroes/
│   └── tratamento-erros.md
├── armadilhas/
│   └── race-checkout.md
└── dominio/
    └── tipos-cupom.md
```

Categorias:

- **fluxos** — Como as coisas funcionam. Integrações, sequências, caminhos de dados.
- **padroes** — Como as coisas são feitas aqui. Convenções, estruturas recorrentes.
- **armadilhas** — Armadilhas. Bugs, quirks, comportamento contraintuitivo.
- **dominio** — Conceitos de negócio. Terminologia, regras, lógica não óbvia no código.

Estas categorias são diretrizes, não regras rígidas. Se uma nota se encaixa
em múltiplas categorias, escolha a principal. Se nenhuma se encaixa, coloque na raiz.

## Formato do INDEX.md

O índice deve ser compacto. Uma linha por nota. A IA lê isso toda
sessão, então cada byte conta.

```markdown
# .notebook
> Inteligência do projeto — leia antes de cada missão

Última atualização: 2026-02-22

- [fluxo-auth](fluxo-auth.md) — OAuth2 + rotação de refresh | fluxo | auth, segurança
- [tratamento-erros](tratamento-erros.md) — Error boundaries + hook customizado | padrão | react, erros
- [race-checkout](race-checkout.md) — Race condition na atualização do carrinho | armadilha | checkout, carrinho
- [tipos-cupom](tipos-cupom.md) — Regras: percentual vs fixo vs BOGO | domínio | cupões, preços
```

Formato por linha:

```
- [slug](caminho) — resumo (máx ~80 chars) | categoria | tags
```

Regras para INDEX.md:

- Manter resumos curtos e escaneáveis.
- Tags são minúsculas, separadas por vírgula. Use para grep rápido.
- Atualizar `Última atualização` sempre que o índice mudar.
- Se usar subdiretórios, caminhos incluem a pasta: `fluxos/fluxo-auth.md`.
- Ordenar por mais recentemente atualizado, não alfabeticamente.

## Formato de Nota Individual

Notas são telegráficas. Pense em notas de campo, não documentação.

```markdown
# Fluxo de Auth
> OAuth2 com rotação de refresh token

Entrada: `src/middleware/auth.ts:authMiddleware()` (L12)
Fluxo: middleware → `services/auth/jwt.ts:verify()` → `services/user/find.ts:findById()`

Refresh: `services/auth/refresh.ts:rotateToken()`
- Tokens de uso único — consumidos no refresh, novo par emitido
- Armazenado no Redis com TTL (veja `lib/redis.ts:sessionStore`)

Provedores OAuth: `config/oauth.ts` — Google, GitHub
- Cada provedor mapeia para `services/auth/oauth/[provedor].ts`

Sessão: Respaldada por Redis via `lib/redis.ts` (L45-62)

Atualizado: 2026-02-22
```

### Princípios de formato

1. **Ponteiros, não cópias.** Sempre referencie como:
   - `arquivo/caminho.ts:nomeFuncao()` para funções
   - `arquivo/caminho.ts` (L10-25) para intervalos de linha específicos
   - `arquivo/caminho.ts:NomeClasse.metodo()` para métodos de classe
   Nunca cole blocos de código em notas. O código muda; ponteiros
   podem ser re-verificados. Código colado se torna mentiras obsoletas.

2. **Um conceito por nota.** Se precisa de rolagem, divida.
   Uma nota sobre fluxo de auth não deve também cobrir gerenciamento de sessão
   a menos que sejam insepáráveis.

3. **Prosa mínima.** Use fragmentos, setas, travessões. Não frases.
   "middleware → verificar JWT → carregar usuário → anexar ao req" é melhor
   do que "O middleware primeiro verifica o token JWT, depois carrega
   o usuário do banco de dados, e finalmente o anexa ao
   objeto request."

4. **Sempre inclua ponto de entrada.** Cada nota deve ter um ponto
   de partida claro para o leitor saber por onde começar a explorar.

5. **Sempre inclua data de atualização.** Para o leitor saber quão
   recente é a informação.

6. **Sem opiniões, apenas observações.** "Usa Redux para estado" não
   "Usa Redux em vez de uma solução melhor." Se algo é
   genuinamente problemático, declare o impacto observável:
   "Store do Redux tem 47 chaves no nível raiz — encontrar estado relevante
   requer busca em 12 reducers."

## Criando o .notebook/ pela Primeira Vez

Quando `.notebook/` ainda não existe:

1. Criar o diretório.
2. Criar INDEX.md apenas com o cabeçalho:

   ```markdown
   # .notebook
   > Inteligência do projeto — leia antes de cada missão

   Última atualização: [hoje]
   ```

3. NÃO faça uma análise completa do projeto. Notas são criadas organicamente
   conforme você trabalha. As primeiras notas virão do Debrief da sua primeira missão.

## Atualizando Notas

Ao atualizar uma nota existente:

1. Leia o conteúdo atual.
2. Adicione, modifique ou remova informações com base no que descobriu.
3. Atualize a data `Atualizado` no rodapé.
4. Se o resumo no INDEX.md mudou, atualize-o também.

Quando informações se tornam inválidas (ex: um fluxo mudou por causa
do seu trabalho), atualize a nota imediatamente — notas obsoletas são piores
do que nenhuma nota.

## Orçamento de Tokens

Todo o sistema `.notebook/` é projetado para divulgação progressiva:

- **INDEX.md** é lido toda sessão (~5-50 linhas). Custo: mínimo.
- **Notas individuais** são lidas apenas quando relevantes à missão atual.
  A IA decide quais abrir com base nas tags do INDEX.md.
- **Custo total por sessão:** INDEX.md + 0-3 notas relevantes.

Se INDEX.md crescer além de 50 entradas, considere arquivar notas antigas
em um subdiretório `arquivo/` e removê-las do índice ativo.
Notas arquivadas ainda são pesquisáveis, mas não são carregadas por padrão.
