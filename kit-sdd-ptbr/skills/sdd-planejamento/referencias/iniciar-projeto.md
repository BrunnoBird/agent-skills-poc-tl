# Inicialização de Projeto

**Gatilho:** "Inicializar projeto", "Configurar projeto", "Começar novo projeto"

## Processo

Extrair visão do projeto via Q&A iterativo (máx 3-5 perguntas por mensagem):

**Perguntas essenciais:**

1. O que você está construindo?
2. Para quem é e qual problema resolve?
3. Qual tech stack você está usando? (se conhecido)
4. O que está no escopo da v1? O que está explicitamente excluído?
5. Restrições críticas? (prazo, técnicas, recursos)

**Parar quando:** Entendimento claro da visão, objetivos e limites.

## Saída: .specs/project/PROJECT.md

**Estrutura:**

```markdown
# [Nome do Projeto]

**Visão:** [Descrição em 1-2 frases]
**Para:** [usuários-alvo]
**Resolve:** [problema central sendo endereçado]

## Objetivos

- [Objetivo principal com métrica de sucesso mensurável]
- [Objetivo secundário com métrica de sucesso mensurável]

## Tech Stack

**Core:**

- Framework: [nome + versão]
- Linguagem: [nome + versão]
- Banco de dados: [nome]

**Dependências-chave:** [3-5 bibliotecas/frameworks críticos]

## Escopo

**v1 inclui:**

- [Capacidade central 1]
- [Capacidade central 2]
- [Capacidade central 3]

**Explicitamente fora do escopo:**

- [O que NÃO está sendo construído]
- [O que NÃO está sendo construído]

## Restrições

- Prazo: [se aplicável]
- Técnicas: [se aplicável]
- Recursos: [se aplicável]
```

**Limite de tamanho:** 2.000 tokens (~1.200 palavras)

**Validação:**

- Visão clara em 1-2 frases?
- Objetivos têm resultados mensuráveis?
- Limites de escopo explícitos?
