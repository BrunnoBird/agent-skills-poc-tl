# Instruções para o Agente — [Nome do Projeto]

> Este arquivo é lido automaticamente pelo Claude Code CLI e pelo Devin CLI antes de qualquer sessão.
> Edite as seções marcadas com `← EDITE` para configurar este projeto.

---

## Metodologia de Desenvolvimento

Este projeto usa **SDD (Desenvolvimento Orientado a Especificação)**.
Antes de implementar qualquer feature nova, siga o fluxo SDD com o skill `sdd-planejamento`.

### Quando usar o SDD

- Feature nova com mais de 3 arquivos → use o pipeline completo (`especificar feature`)
- Bug simples ou ajuste pequeno → use modo rápido (`correção rápida: descrição`)
- Explorando código existente → use `navegador-codebase` antes de especificar
- Incerto sobre uma decisão → use `desafiador-ideias` antes de commitar

### Comandos Principais

```
inicializar projeto        → cria PROJECT.md + ROADMAP.md
especificar feature [x]    → inicia pipeline SDD para a feature
correção rápida: [desc]    → bug fix ou ajuste pequeno, sem cerimônia
mapear codebase            → analisa projeto existente (brownfield)
pausar trabalho            → salva handoff para retomada
retomar trabalho           → carrega handoff e STATE.md
desafie minha ideia        → stress-test antes de commitar em um design
```

---

## Stack do Projeto

<!-- ← EDITE: descreva o stack usado neste projeto -->

- Linguagem: <!-- ex: TypeScript, Swift, Kotlin, Python -->
- Framework: <!-- ex: NestJS, SwiftUI, Spring Boot, FastAPI -->
- Banco de dados: <!-- ex: PostgreSQL, SQLite, MongoDB -->
- Testes: <!-- ex: Jest, XCTest, JUnit, pytest -->

---

## Comandos de Build e Teste

<!-- ← EDITE: substitua pelos comandos reais do projeto -->

```bash
# ── Descomente e adapte o bloco do seu stack ──────────────────────────

# Node.js / TypeScript
# npm install && npm run build && npm test && npm run lint

# Python / pytest
# pip install -r requirements.txt && pytest && flake8 src/

# Java / Maven
# mvn clean install && mvn test && mvn checkstyle:check

# Java / Gradle
# ./gradlew build test checkstyleMain

# .NET / C#
# dotnet restore && dotnet build && dotnet test
```

---

## Convenções do Projeto

<!-- ← EDITE: liste as convenções relevantes para o agente -->

### Nomenclatura
- Arquivos: <!-- ex: kebab-case, PascalCase -->
- Funções: <!-- ex: camelCase -->
- Classes: <!-- ex: PascalCase -->

### Estilo de Commit (Conventional Commits)
```
feat(scope): descrição       → nova funcionalidade
fix(scope): descrição        → correção de bug
refactor(scope): descrição   → refatoração sem mudança de comportamento
docs(scope): descrição       → documentação
test(scope): descrição       → testes
```

### Onde as Coisas Ficam
- Código fonte: <!-- ex: src/ -->
- Testes: <!-- ex: src/__tests__/ ou tests/ -->
- Documentação: <!-- ex: docs/ -->

---

## Restrições e Cuidados

<!-- ← EDITE: liste restrições específicas do projeto/empresa -->

- Não adicionar dependências externas sem aprovação
- <!-- adicione outras restrições relevantes -->

---

## Contexto do Projeto

<!-- ← EDITE: descreva brevemente o que o projeto faz -->

[Descreva aqui o que o projeto faz, o domínio de negócio e qualquer contexto relevante para o agente.]

---

## Arquivos Importantes

<!-- ← EDITE: liste os arquivos mais importantes para o agente conhecer -->

- `README.md` — visão geral do projeto
- `.specs/project/PROJECT.md` — visão e objetivos (criado pelo SDD)
- `.specs/project/STATE.md` — memória de decisões (criado pelo SDD)
