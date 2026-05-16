# Princípios de Código

Leia este arquivo durante a fase de Execução ao implementar mudanças.
Estes princípios reduzem erros comuns de codificação por IA e garantem
saída consistente e de alta qualidade.

## 1. Pense Antes de Codar

Antes de escrever qualquer código:

- Declare suas suposições explicitamente. Se incerto, pergunte.
- Se múltiplas abordagens existem, apresente-as com trade-offs.
- Se uma abordagem mais simples existe, diga. Questione quando justificado.
- Se algo não está claro, pare. Nomeie o que está confuso. Pergunte.
- Se a abordagem do desenvolvedor parece errada, diga construtivamente.
  Não seja sycophantic — honestidade previne bugs.

## 2. Simplicidade Primeiro

Escreva o mínimo de código que resolve o problema.

- Nenhuma feature além do que foi pedido.
- Nenhuma abstração para código de uso único.
- Nenhuma "flexibilidade" ou "configurabilidade" que não foi solicitada.
- Nenhum tratamento de erro para cenários impossíveis.
- Nenhuma otimização especulativa.
- Se você escreveu 200 linhas e poderia ser 50, reescreva.

O teste: "Um engenheiro sênior diria que isso está complicado demais?"
Se sim, simplifique.

## 3. Mudanças Cirúrgicas

Ao editar código existente:

- Não "melhore" código adjacente, comentários ou formatação.
- Não refatore coisas que não estão quebradas.
- Corresponda ao estilo existente, mesmo que você faria diferente.
- Se notar problemas não relacionados, mencione-os — não os corrija.

Quando suas mudanças criam órfãos:

- Remova imports, variáveis e funções que SUAS mudanças tornaram não utilizados.
- Não remova código morto pré-existente a menos que solicitado.

O teste: Cada linha modificada traça diretamente ao objetivo da missão.

## 4. Execução Orientada a Objetivos

Transforme tarefas vagas em objetivos verificáveis:

- "Adicionar validação" → "Escrever testes para entradas inválidas, depois fazê-los passar"
- "Corrigir o bug" → "Escrever um teste que reproduz o bug, depois corrigi-lo"
- "Refatorar X" → "Garantir que os testes passam antes e depois"

Para tarefas em múltiplas etapas, declare um plano breve com checkpoints de verificação.
Critérios de sucesso fortes permitem execução autônoma. Critérios fracos
("faça funcionar") requerem clarificação constante — peça melhores
critérios em vez de adivinhar.

## 5. Respeite o Codebase

Você é um convidado neste codebase. Aja como tal.

- Use as mesmas convenções de nomenclatura já no projeto.
- Use os mesmos padrões de organização de arquivo.
- Use a mesma abordagem de tratamento de erros.
- Use o mesmo estilo de import (nomeado vs padrão, relativo vs absoluto).
- Se o projeto usa ponto e vírgula, use ponto e vírgula. Se não, não use.

Se as convenções existentes conflitam com boas práticas da linguagem, sinalize
para o desenvolvedor. Não introduza silenciosamente uma convenção diferente.

## 6. Boas Práticas da Linguagem

Sempre siga as boas práticas oficiais para a linguagem e
frameworks em uso. Isso significa:

- Usar padrões idiomáticos para a linguagem (ex: list comprehensions
  em Python, optional chaining em TypeScript).
- Seguir o guia de estilo oficial quando o projeto não tem o seu.
- Usar APIs e métodos atuais, não deprecados.
- Tratar erros conforme as convenções da linguagem (try/catch,
  tipos Result, retornos de erro — o que o ecossistema preferir).

Crítico: Nunca confie na memória de treinamento para assinaturas de API, parâmetros
de método ou comportamento de framework. Sempre verifique na documentação atual usando
a Cadeia de Verificação de Conhecimento:

```
.notebook/ → docs do projeto → MCP Context7 → busca web → sinalizar como incerto
```

## 7. Dependências e Imports

Ao adicionar novas dependências ou imports:

- Verifique se o projeto já tem uma dependência que resolve o
  problema antes de adicionar uma nova.
- Verifique o gerenciador de pacotes do projeto e o lockfile para
  versões existentes.
- Se adicionar uma nova dependência, mencione ao desenvolvedor com
  justificativa — nunca adicione pacotes silenciosamente.
- Corresponda ao estilo e ordem de import do projeto.

## 8. Tratamento de Erros

- Trate erros que podem realisticamente ocorrer.
- Não adicione blocos catch para cenários teoricamente impossíveis.
- Use os padrões existentes de tratamento de erros do projeto.
- Mensagens de erro devem ser acionáveis — diga o que aconteceu e
  o que fazer a respeito, não apenas "Algo deu errado."
- Nunca engula erros silenciosamente (blocos catch vazios) a menos que
  haja uma razão explícita documentada em um comentário.

## 9. Testes

Quando testes são parte da missão:

- Escreva testes que verificam comportamento, não detalhes de implementação.
- Teste o contrato (entrada → saída), não o estado interno.
- Nomeie testes descritivamente: "deve rejeitar cupóm expirado"
  não "teste1" ou "teste cupóm."
- Se modificar código existente, execute os testes existentes primeiro para
  estabelecer uma baseline.
- Se adicionar um bug fix, escreva um teste que reproduz o bug
  primeiro, depois corrija-o.

Quando testes NÃO são parte da missão:

- Não adicione testes a menos que solicitado.
- Mas MENCIONE se a mudança é arriscada e não testada:
  "Esta mudança afeta o fluxo de pagamento, mas não há testes
  cobrindo este caminho. Considere adicionar testes para [casos específicos]."

## 10. Comentários

- Não adicione comentários que repetem o código.
- Não remova comentários existentes a menos que estejam comprovadamente errados.
- Adicione comentários apenas para lógica de negócio não óbvia ou contornos.
- Se adicionar um contorno, explique POR QUÊ é necessário e vincule
  ao issue/ticket relevante se disponível.
- Corresponda ao estilo de comentário e idioma do projeto (idioma humano).
