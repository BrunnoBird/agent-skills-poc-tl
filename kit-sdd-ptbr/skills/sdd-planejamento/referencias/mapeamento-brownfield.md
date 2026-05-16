# Mapeamento Brownfield

**Gatilho:** "Mapear codebase", "Analisar código existente", "Documentar arquitetura atual"

**Propósito:** Entender a estrutura do projeto existente antes de adicionar features.

## Processo

Antes de começar, verifique se o skill `navegador-codebase` está disponível para exploração de código (veja Integrações com Skills no SKILL.md). Se disponível, prefira-o para todas as tarefas de descoberta e navegação abaixo.

**Abordagem de alto nível:**

1. Explorar a estrutura de diretórios sistematicamente
2. Identificar o tech stack a partir dos manifestos de dependências
3. Extrair padrões de amostras representativas de código
4. Documentar convenções e arquiteturas observadas
5. Catalogar integrações externas
6. Identificar preocupações: dívida técnica, bugs conhecidos, riscos de segurança, gargalos de performance, áreas frágeis

**Profundidade de análise:**

- Amostrar 5-10 arquivos representativos por categoria
- Foco em consistência e padrões, não cobertura exaustiva
- Extrair exemplos reais, não suposições

## Saída: 7 Arquivos em .specs/codebase/

---

### 1. STACK.md

**Propósito:** Documentar tech stack e dependências.

**Limite de tamanho:** 2.000 tokens (~1.200 palavras)

**Extrair de:**

- Arquivos de manifesto de dependências
- Configuração de build
- Configuração de runtime

**Documentar:**

```markdown
# Tech Stack

**Analisado em:** [data]

## Core

- Framework: [nome + versão detectados]
- Linguagem: [nome + versão detectados]
- Runtime: [nome + versão detectados]
- Gerenciador de pacotes: [gerenciador detectado]

## Frontend (se aplicável)

- UI Framework: [nome + versão]
- Estilização: [abordagem + ferramentas]
- Gerenciamento de Estado: [biblioteca/padrão]
- Formulários: [biblioteca se presente]

## Backend (se aplicável)

- Estilo de API: [REST/GraphQL/gRPC + framework]
- Banco de Dados: [ORM/query builder + sistema de banco]
- Autenticação: [biblioteca/abordagem]

## Testes

- Unitários: [framework]
- Integração: [framework]
- E2E: [framework se presente]

## Serviços Externos

- [Categoria]: [Nome do serviço]
- [Categoria]: [Nome do serviço]

## Ferramentas de Desenvolvimento

- [Categoria de ferramenta]: [Nome da ferramenta]
```

**Instruções:**

- Extrair dos arquivos de dependências reais
- Incluir versões para dependências principais
- Categorizar por propósito
- Anotar frameworks de teste explicitamente

---

### 2. ARCHITECTURE.md

**Propósito:** Documentar padrões arquiteturais e fluxo de dados.

**Limite de tamanho:** 4.000 tokens (~2.400 palavras)

**Extrair de:**

- Organização de diretórios
- Análise de estrutura de código
- Padrões repetidos em arquivos

**Documentar:**

```markdown
# Arquitetura

**Padrão:** [Padrão identificado - monolito/microsserviços/modular/etc]

## Estrutura de Alto Nível

[Criar diagrama/descrição baseado na organização real]

## Padrões Identificados

### [Nome do Padrão]

**Localização:** [onde este padrão vive]
**Propósito:** [o que isso alcança]
**Implementação:** [como é estruturado]
**Exemplo:** [referência a arquivo/função real]

### [Nome do Padrão]

[Mesma estrutura]

## Fluxo de Dados

### [Fluxo-Chave - ex: Autenticação/Pagamento/etc]

[Mapear fluxo real a partir da análise de código]

### [Fluxo-Chave]

[Mapear fluxo real]

## Organização de Código

**Abordagem:** [por feature/por camada/orientado a domínio/etc]

**Estrutura:**
[Documentar organização real de diretórios]

**Limites de módulo:**
[Como o código é dividido em módulos/pacotes]
```

**Instruções:**

- Identificar padrões do código real, não suposições
- Documentar decisões arquiteturais observadas
- Criar diagramas de fluxo para caminhos críticos
- Referenciar exemplos concretos do codebase

---

### 3. CONVENTIONS.md

**Propósito:** Documentar estilo de código e convenções de nomenclatura.

**Limite de tamanho:** 3.000 tokens (~1.800 palavras)

**Extrair de:**

- Analisar 5-10 arquivos representativos
- Identificar padrões consistentes
- Observar convenções reais em uso

**Documentar:**

```markdown
# Convenções de Código

## Convenções de Nomenclatura

**Arquivos:**
[Padrão observado - documentar abordagem real]
Exemplos: [nomes de arquivo reais do codebase]

**Funções/Métodos:**
[Padrão observado]
Exemplos: [nomes de funções reais]

**Variáveis:**
[Padrão observado]
Exemplos: [nomes de variáveis reais]

**Constantes:**
[Padrão observado]
Exemplos: [nomes de constantes reais]

## Organização de Código

**Declaração de Imports/Dependências:**
[Padrão de ordenação observado]
[Exemplo de arquivo real]

**Estrutura de Arquivo:**
[Organização observada dentro dos arquivos]
[Exemplo de arquivo real]

## Tipagem/Documentação

**Abordagem:** [Sistema de tipos/abordagem de documentação utilizada]
[Exemplo do código real]

## Tratamento de Erros

**Padrão:** [Abordagem observada de tratamento de erros]
[Exemplo do código real]

## Comentários/Documentação

**Estilo:** [Quando/como comentários são usados]
[Exemplo do código real]
```

**Instruções:**

- Extrair padrões de amostras de código reais
- Documentar convenções observadas, não ideais
- Incluir exemplos concretos do codebase
- Anotar exceções ou variações onde encontradas

---

### 4. STRUCTURE.md

**Propósito:** Documentar layout de diretórios e organização de arquivos.

**Limite de tamanho:** 2.000 tokens (~1.200 palavras)

**Documentar:**

```markdown
# Estrutura do Projeto

**Raiz:** [caminho raiz do projeto]

## Árvore de Diretórios

[Representação visual em árvore - máx 3 níveis de profundidade]

## Organização de Módulos

### [Nome do Módulo/Área]

**Propósito:** [o que esta área gerencia]
**Localização:** [onde os arquivos vivem]
**Arquivos-chave:** [arquivos importantes nesta área]

### [Nome do Módulo/Área]

[Mesma estrutura]

## Onde as Coisas Vivem

**[Capacidade/Feature]:**

- UI/Interface: [localização]
- Lógica de Negócio: [localização]
- Acesso a Dados: [localização]
- Configuração: [localização]

**[Capacidade/Feature]:**
[Mesma estrutura]

## Diretórios Especiais

**[Nome do diretório]:**
**Propósito:** [o que pertence aqui]
**Exemplos:** [arquivos-chave neste diretório]
```

**Instruções:**

- Criar visão em árvore da estrutura real de diretórios
- Limitar profundidade para manter legibilidade
- Documentar propósito dos diretórios-chave
- Mapear capacidades para localizações físicas

---

### 5. TESTING.md

**Propósito:** Documentar infraestrutura de testes e padrões.

**Limite de tamanho:** 4.000 tokens (~2.400 palavras)

**Documentar:**

```markdown
# Infraestrutura de Testes

## Frameworks de Teste

**Unitário/Integração:** [nome do framework + versão]
**E2E:** [nome do framework + versão]
**Cobertura:** [ferramenta se utilizada]

## Organização dos Testes

**Localização:** [onde os testes vivem]
**Nomenclatura:** [padrão de nomenclatura de arquivos de teste]
**Estrutura:** [como os testes são organizados]

## Padrões de Teste

### Testes Unitários

**Abordagem:** [padrão observado]
**Localização:** [onde os testes unitários vivem]
[Descrição do padrão real utilizado]

### Testes de Integração

**Abordagem:** [padrão observado]
**Localização:** [onde os testes de integração vivem]
[Descrição do padrão real utilizado]

### Testes E2E

**Abordagem:** [padrão observado se presente]
**Localização:** [onde os testes E2E vivem]
[Descrição do padrão real utilizado]

## Execução de Testes

**Comandos:** [como executar os testes]
**Configuração:** [abordagem de configuração de testes]

## Metas de Cobertura

**Atual:** [se mensurável]
**Objetivos:** [se documentados]
**Aplicação:** [se automatizada]

## Matriz de Cobertura de Testes

Analise o codebase para determinar quais camadas de código requerem quais tipos de teste.
Para cada camada, documente o tipo de teste necessário, padrão de localização de arquivo e comando de execução.

| Camada de Código | Tipo de Teste Necessário    | Padrão de Localização  | Comando de Execução |
| ---------------- | --------------------------- | ---------------------- | ------------------- |
| [camada]         | [unit/integration/e2e/none] | [padrão glob ou path]  | [comando]           |

## Avaliação de Paralelismo

| Tipo de Teste | Paralelo-Seguro? | Modelo de Isolamento | Evidência                     |
| ------------- | ---------------- | -------------------- | ----------------------------- |
| [tipo]        | [Sim/Não]        | [descrição]          | [arquivo/padrão que comprova] |

## Comandos de Verificação Gate

| Nível Gate | Quando Usar                                    | Comando                     |
| ---------- | ---------------------------------------------- | --------------------------- |
| Rápido     | Após tarefas com apenas testes unitários       | [comando de teste unitário] |
| Completo   | Após tarefas com testes e2e/integração         | [unit + e2e commands]       |
| Build      | Após conclusão de fase                         | [build + lint + unit + e2e] |
```

**Instruções:**

- Identificar frameworks de teste por dependências e código
- Documentar padrões de teste reais observados
- Anotar abordagem de organização de testes
- Incluir instruções de execução
- **Matriz de Cobertura de Testes:** Amostrar 5-10 arquivos de teste existentes para identificar quais camadas são testadas e como. Ver localização dos arquivos de teste em relação ao código-fonte para determinar padrões. Extrair comandos de execução de `package.json`, `project.json`, `Makefile`, config de CI. Marcar camadas sem testes existentes como "none" com nota em CONCERNS.md.
- **Avaliação de Paralelismo:** Sinais NÃO paralelo-seguro: conexão DB compartilhada (mesma URL de config), limpeza no nível de tabela em `beforeEach`/`afterAll` (`.del()`, `DELETE FROM`, `TRUNCATE`), reset de estado de mock compartilhado em globais. Sinais paralelo-seguro: criação de DB por teste (Testcontainers, schema dinâmico, SQLite em memória), namespace de dados (todos os dados com chave por ID único de teste), sem estado mutável compartilhado entre arquivos de teste, todos os deps mockados (`jest.fn()`, `vi.fn()`).
- **Comandos de Verificação Gate:** Extrair dos comandos reais do projeto — não inventar comandos.

---

### 6. INTEGRATIONS.md

**Propósito:** Documentar integrações com serviços externos.

**Limite de tamanho:** 5.000 tokens (~3.000 palavras)

**Documentar:**

```markdown
# Integrações Externas

## [Categoria de Serviço]

**Serviço:** [nome do serviço]
**Propósito:** [o que esta integração fornece]
**Implementação:** [onde a integração vive no código]
**Configuração:** [como o serviço é configurado]
**Autenticação:** [abordagem de auth se aplicável]

## [Categoria de Serviço]

[Mesma estrutura]

## Integrações de API

### [Nome da API]

**Propósito:** [o que esta API fornece]
**Localização:** [onde o cliente/código da API vive]
**Autenticação:** [método de auth]
**Endpoints-chave:** [principais endpoints utilizados]

## Webhooks

### [Fonte do Webhook]

**Propósito:** [quais eventos são tratados]
**Localização:** [localização do handler do webhook]
**Eventos:** [tipos de eventos processados]

## Jobs em Background

**Sistema de fila:** [sistema se utilizado]
**Localização:** [onde as definições de job vivem]
**Jobs:** [principais jobs em background]
```

**Instruções:**

- Identificar integrações a partir de código e configuração
- Documentar abordagens de autenticação
- Anotar handlers de webhook se presentes
- Incluir infraestrutura de jobs em background

---

### 7. CONCERNS.md

**Propósito:** Surfaçar alertas acionáveis sobre o codebase — dívida técnica, bugs conhecidos, lacunas de segurança, gargalos de performance, áreas frágeis, limites de escala, dependências arriscadas, features ausentes e lacunas de cobertura de testes.

**Limite de tamanho:** 5.000 tokens (~3.000 palavras)

Veja [preocupacoes.md](preocupacoes.md) para o template completo, diretrizes e exemplos.

**Instruções:**

- Documentar apenas preocupações com evidências (caminhos de arquivo, medições, passos de reprodução)
- Incluir abordagens de correção, não apenas problemas
- Omitir seções sem achados
- Priorizar por risco/impacto
- Usar tom profissional e orientado a soluções

---

## Orçamento Total de Contexto

**Combinado:** ~19.000 tokens (10% da janela de contexto)
**Aceitável para:** Projetos brownfield que requerem entendimento do codebase
**Estratégia de carregamento:** Carregar documentos relevantes sob demanda baseado na tarefa
