# Ferramentas de Análise de Código

Use degradação graciosa para busca de código e análise estrutural.

## Prioridade de Ferramentas

1. **ast-grep** (`sg`) - Busca baseada em padrões estruturais
2. **ripgrep** (`rg`) - Busca de texto rápida com contexto
3. **grep** - Busca de texto padrão (sempre disponível)

## Detecção

Verifique a disponibilidade da ferramenta antes de usar:

```bash
# Verificar ast-grep
if command -v sg >/dev/null 2>&1; then
  # Usar ast-grep para busca estrutural
elif command -v rg >/dev/null 2>&1; then
  # Fallback para ripgrep
else
  # Usar grep padrão como fallback final
fi
```

## Exemplos de Uso

**Encontrar definições de função:**

```bash
# ast-grep (melhor - estrutural)
sg -p 'function $NAME($$$) { $$$ }'

# ripgrep (fallback - texto rápido)
rg '^function\s+\w+\(' --type-add 'source:*.[extensao]' -t source

# grep (último recurso - básico)
grep -r '^function ' --include="*.[extensao]"
```

**Encontrar imports/requires:**

```bash
# ast-grep
sg -p 'import { $$$ } from "$MODULE"'

# ripgrep
rg '^import .* from' --type-add 'source:*.[extensao]' -t source

# grep
grep -r '^import ' --include="*.[extensao]"
```

**Encontrar definições de classe/componente:**

```bash
# ast-grep
sg -p 'class $NAME { $$$ }'

# ripgrep
rg '^(class|export class)\s+\w+' --type-add 'source:*.[extensao]' -t source

# grep
grep -r '^class ' --include="*.[extensao]"
```

## Escopo de Busca

**Boas práticas:**

- Limitar às extensões de arquivo fonte relevantes para o projeto
- Excluir diretórios: `node_modules`, `vendor`, `dist`, `build`, `.git`
- Focar em diretórios fonte: `src`, `lib`, `app`
- Usar filtros de tipo de arquivo quando disponíveis

**Dicas de performance:**

- Usar padrões específicos em vez de buscas amplas
- Limitar profundidade de diretório com `--max-depth` (ripgrep/grep)
- Cachear resultados para consultas repetidas

## Aviso de Fallback

Se ast-grep não estiver disponível, exibir uma vez por sessão:

```
⚠️ ast-grep não detectado. Instale para análise estrutural de código mais precisa.
   https://ast-grep.github.io/guide/quick-start.html
```

## Quando Usar

- Encontrar padrões de uso em todo o codebase
- Identificar estrutura e organização de código
- Localizar definições de função/classe/componente
- Analisar padrões de import/dependência
- Análise de impacto de refatoração
- Navegação de código em codebases desconhecidos
