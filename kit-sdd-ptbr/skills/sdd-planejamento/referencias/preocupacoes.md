# Fase: Preocupações do Codebase

**Gatilho:** Parte do mapeamento brownfield, ou explicitamente "documentar preocupações", "encontrar dívida técnica", "o que é arriscado neste codebase"

**Propósito:** Surfaçar alertas acionáveis sobre o codebase. Focado em "o que observar ao fazer mudanças." Esta é documentação viva, não uma lista de reclamações.

## Quando Gerar

CONCERNS.md é gerado como parte do fluxo de mapeamento brownfield (junto com STACK.md, ARCHITECTURE.md, etc.). Também pode ser criado ou atualizado independentemente quando:

- Explorar uma nova área do codebase revela riscos
- Uma investigação de bug descobre problemas sistêmicos
- Uma implementação de feature encontra fragilidade inesperada
- Uma auditoria de dependência revela riscos

## Processo

### 1. Coletar Evidências

Durante a exploração do codebase, busque sinais concretos — não opiniões. Fontes de evidência:

- Padrões de código que indicam atalhos (comentários TODO/FIXME/HACK, lógica duplicada, tratamento de erro ausente)
- Lacunas de cobertura de testes (caminhos críticos não testados, casos extremos ausentes)
- Manifestos de dependências (pacotes desatualizados, bibliotecas deprecadas, avisos de segurança)
- Indicadores de performance (queries N+1, índices ausentes, chamadas bloqueantes síncronas)
- Padrões de segurança (verificações de auth somente no cliente, entradas não validadas, segredos expostos)

### 2. Classificar e Documentar

Cada preocupação deve ter: **o quê** é o problema, **onde** vive (caminhos de arquivo), **por quê** importa (impacto), e **como** corrigir (abordagem).

### 3. Priorizar por Risco

Focar em preocupações que poderiam causar danos reais — perda de dados, brechas de segurança, falhas visíveis ao usuário, limites de escala. Problemas menores de estilo e TODOs normais não pertencem aqui.

---

## Template: `.specs/codebase/CONCERNS.md`

**Limite de tamanho:** 5.000 tokens (~3.000 palavras)

```markdown
# Preocupações do Codebase

**Data de Análise:** [YYYY-MM-DD]

## Dívida Técnica

**[Área/Componente]:**

- Problema: [Qual é o atalho/gambiarra]
- Arquivos: [Caminhos específicos de arquivo com backticks]
- Por quê: [Por que foi feito assim]
- Impacto: [O que quebra ou degrada por causa disso]
- Abordagem de correção: [Como tratar adequadamente]

## Bugs Conhecidos

**[Descrição do bug]:**

- Sintomas: [O que acontece]
- Gatilho: [Como reproduzir]
- Arquivos: [Onde o bug vive]
- Contorno: [Mitigação temporária se houver]
- Causa raiz: [Se conhecida]
- Bloqueado por: [Se aguardando algo]

## Considerações de Segurança

**[Área que requer cuidado de segurança]:**

- Risco: [O que pode dar errado]
- Arquivos: [Onde o risco vive]
- Mitigação atual: [O que está em vigor agora]
- Recomendações: [O que deve ser adicionado]

## Gargalos de Performance

**[Operação/Endpoint lento]:**

- Problema: [O que é lento]
- Arquivos: [Onde está o gargalo]
- Medição: [Números reais: "500ms p95", "2s de carregamento"]
- Causa: [Por que é lento]
- Caminho de melhoria: [Como acelerar]

## Áreas Frágeis

**[Componente/Módulo]:**

- Arquivos: [Onde a fragilidade vive]
- Por que frágil: [O que faz quebrar facilmente]
- Falhas comuns: [O que normalmente dá errado]
- Modificação segura: [Como mudar sem quebrar]
- Cobertura de testes: [Está testado? Lacunas?]

## Limites de Escala

**[Recurso/Sistema]:**

- Capacidade atual: [Números: "100 req/s", "10k usuários"]
- Limite: [Onde quebra]
- Sintomas no limite: [O que acontece]
- Caminho de escala: [Como aumentar capacidade]

## Dependências em Risco

**[Pacote/Serviço]:**

- Risco: [ex: "deprecado", "sem manutenção", "mudanças breaking chegando"]
- Impacto: [O que quebra se falhar]
- Plano de migração: [Alternativa ou caminho de upgrade]

## Features Críticas Ausentes

**[Lacuna de feature]:**

- Problema: [O que está ausente]
- Contorno atual: [Como os usuários lidam]
- Bloqueia: [O que não pode ser feito sem isso]
- Complexidade de implementação: [Estimativa aproximada de esforço]

## Lacunas de Cobertura de Testes

**[Área não testada]:**

- O que não está testado: [Funcionalidade específica]
- Risco: [O que pode quebrar despercebido]
- Prioridade: [Alta/Média/Baixa]
- Dificuldade de testar: [Por que ainda não está testado]

---

_Auditoria de preocupações: [data]_
_Atualize conforme problemas são corrigidos ou novos descobertos_
```

**Incluir apenas seções com achados.** Seções vazias devem ser completamente omitidas.

---

## O Que Pertence vs. O Que Não Pertence

**Incluir:**

- Dívida técnica com impacto claro e abordagem de correção
- Bugs conhecidos com passos de reprodução
- Lacunas de segurança e recomendações de mitigação
- Gargalos de performance com medições
- Código frágil que quebra facilmente
- Limites de escala com números
- Dependências que precisam de atenção
- Features ausentes que bloqueiam fluxos
- Lacunas de cobertura de testes

**Excluir:**

- Opiniões sem evidências ("código está bagunçado")
- Reclamações sem soluções ("auth é ruim")
- Ideias de features futuras (isso é para planejamento de produto)
- TODOs normais (esses vivem em comentários de código)
- Decisões arquiteturais que estão funcionando bem
- Problemas menores de estilo de código

---

## Diretrizes de Escrita

- **Sempre incluir caminhos de arquivo** — Preocupações sem localização não são acionáveis. Use backticks: `src/arquivo.ts`
- Seja específico com medições ("500ms p95" não "lento")
- Incluir passos de reprodução para bugs
- Sugerir abordagens de correção, não apenas problemas
- Focar em itens acionáveis
- Priorizar por risco/impacto

**Tom:** Profissional, não emocional. Orientado a soluções. Focado em riscos. Factual.

- ✅ "Padrão de query N+1 em `app/api/cursos/route.ts` — 1.2s p95 com 50+ cursos"
- ❌ "Queries terríveis, tudo é lento"
- ✅ "Correção: adicionar índice em `user_id` na tabela `subscriptions`"
- ❌ "Precisa de correção"

---

## Como CONCERNS.md é Utilizado

- **Planejamento de features:** Verificar CONCERNS.md antes de criar features que tocam áreas sinalizadas
- **Estimativa de risco:** Usar áreas frágeis e limites de escala para estimar risco de mudança
- **Onboarding de novas sessões:** Carregar CONCERNS.md para dar contexto sobre o que observar
- **Priorização de refatoração:** Usar dívida técnica e lacunas de testes para planejar sprints de melhoria
- **Fase de implementação:** Consultar antes de modificar qualquer componente sinalizado

Esta é documentação viva. Atualize conforme problemas são corrigidos ou novos descobertos durante qualquer fase do workflow.
