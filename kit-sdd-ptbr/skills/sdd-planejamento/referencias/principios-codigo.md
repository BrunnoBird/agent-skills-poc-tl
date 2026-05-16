# Princípios de Código

Viés comportamental, não checklist. Leia antes de cada implementação.

---

## Antes de Codar

- Declare suposições explicitamente. Se incerto, pergunte.
- Existem múltiplas interpretações? Apresente todas — não escolha silenciosamente.
- Existe abordagem mais simples? Diga. Questione quando justificado.
- Algo não está claro? Pare. Nomeie o que está confuso. Pergunte.
- A abordagem do usuário parece errada? Discorde honestamente. Não seja sycophantic.

---

## Durante a Implementação

### Simplicidade

- Nenhuma feature além do que foi pedido
- Nenhuma abstração para código de uso único
- Nenhuma "flexibilidade" ou "configurabilidade" não solicitada
- Nenhum tratamento de erro para cenários impossíveis
- 200 linhas que poderiam ser 50? Reescreva.

### Mudanças Cirúrgicas

- Não "melhore" código adjacente, comentários ou formatação
- Não refatore coisas que não estão quebradas
- Corresponda ao estilo existente, mesmo que você faria diferente
- Código morto não relacionado notado? Mencione — não delete
- Remova SOMENTE imports/variáveis/funções que SUAS mudanças tornaram órfãos
- Não remova código morto pré-existente a menos que solicitado

### Integridade dos Testes

- NUNCA enfraqueça uma asserção de teste existente para fazê-la passar
- NUNCA delete um teste para reduzir o contador de falhas
- NUNCA use o mecanismo skip/disable/pending do framework de teste para contornar um teste falhando
- NUNCA modifique testes escritos na fase RED durante a fase GREEN
- Se um teste estiver genuinamente errado, PARE e confirme com o usuário antes de mudar
- Testes são a spec — a implementação se conforma aos testes, não o contrário

### Orientado a Objetivos

- Transforme tarefas vagas em objetivos verificáveis
- Trabalho em múltiplas etapas? Declare um plano breve com checkpoints de verificação
- Cada linha modificada deve traçar diretamente à solicitação do usuário

---

## Após Cada Mudança

Pergunte: "Um engenheiro sênior chamaria isso de complicado demais?"
Se sim → simplifique antes de prosseguir.
