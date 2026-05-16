# Instalação do Kit SDD — Sem npm, sem dependências

Este kit é composto apenas de arquivos Markdown. Nenhuma biblioteca externa é necessária.
Só copie os arquivos para o diretório correto do seu agente.

---

## Para Claude Code CLI

### Instalação por projeto (recomendado)

Só afeta o projeto atual. O diretório `.claude/skills/` fica dentro do repositório.

```bash
# Clone raso da branch com o kit
git clone --depth=1 \
  --branch=claude/extract-sdd-skills-o9hxv \
  https://github.com/brunnobird/agent-skills-poc-tl.git _sdd_tmp

# Cria a pasta de skills do projeto (se não existir)
mkdir -p .claude/skills

# Copia os skills
cp -r _sdd_tmp/kit-sdd-ptbr/skills/* .claude/skills/

# (Opcional) Copia o template de AGENTS.md
cp _sdd_tmp/kit-sdd-ptbr/AGENTS.md ./AGENTS.md

# Limpa o clone temporário
rm -rf _sdd_tmp
```

### Instalação global (todos os projetos da máquina)

```bash
git clone --depth=1 \
  --branch=claude/extract-sdd-skills-o9hxv \
  https://github.com/brunnobird/agent-skills-poc-tl.git _sdd_tmp

mkdir -p ~/.claude/skills
cp -r _sdd_tmp/kit-sdd-ptbr/skills/* ~/.claude/skills/
rm -rf _sdd_tmp
```

### Verificar instalação (Claude Code)

Abra o Claude Code no projeto e execute:
```
/skills
```
Você deverá ver listados:
- `sdd-planejamento`
- `navegador-codebase`
- `diretrizes-codigo`
- `desafiador-ideias`

---

## Para Devin CLI

### Instalação por projeto (recomendado)

```bash
git clone --depth=1 \
  --branch=claude/extract-sdd-skills-o9hxv \
  https://github.com/brunnobird/agent-skills-poc-tl.git _sdd_tmp

mkdir -p .devin/skills
cp -r _sdd_tmp/kit-sdd-ptbr/skills/* .devin/skills/

# (Opcional) Copia o template de AGENTS.md
cp _sdd_tmp/kit-sdd-ptbr/AGENTS.md ./AGENTS.md

rm -rf _sdd_tmp
```

### Instalação global (todos os projetos da máquina)

```bash
git clone --depth=1 \
  --branch=claude/extract-sdd-skills-o9hxv \
  https://github.com/brunnobird/agent-skills-poc-tl.git _sdd_tmp

mkdir -p ~/.config/devin/skills
cp -r _sdd_tmp/kit-sdd-ptbr/skills/* ~/.config/devin/skills/
rm -rf _sdd_tmp
```

### Verificar instalação (Devin)

No Devin CLI, liste os skills disponíveis:
```bash
devin skills list
```

---

## Para Ambos ao Mesmo Tempo (Claude Code + Devin)

```bash
git clone --depth=1 \
  --branch=claude/extract-sdd-skills-o9hxv \
  https://github.com/brunnobird/agent-skills-poc-tl.git _sdd_tmp

mkdir -p .claude/skills .devin/skills
cp -r _sdd_tmp/kit-sdd-ptbr/skills/* .claude/skills/
cp -r _sdd_tmp/kit-sdd-ptbr/skills/* .devin/skills/
cp _sdd_tmp/kit-sdd-ptbr/AGENTS.md ./AGENTS.md
rm -rf _sdd_tmp

echo "✅ Skills instalados para Claude Code e Devin"
```

---

## Instalação Manual (sem git)

Se não tiver acesso ao git no ambiente:

1. Acesse `https://github.com/brunnobird/agent-skills-poc-tl/tree/claude/extract-sdd-skills-o9hxv`
2. Clique em **Code → Download ZIP**
3. Extraia o ZIP
4. Copie a pasta `kit-sdd-ptbr/skills/` para:
   - Claude Code: `.claude/skills/` no projeto
   - Devin: `.devin/skills/` no projeto
5. (Opcional) Copie `kit-sdd-ptbr/AGENTS.md` para a raiz do projeto

---

## Estrutura Após Instalação

```
seu-projeto/
├── .claude/
│   └── skills/
│       ├── sdd-planejamento/      ← skill principal do SDD
│       │   ├── SKILL.md
│       │   └── referencias/
│       ├── navegador-codebase/    ← exploração de código
│       │   ├── SKILL.md
│       │   └── referencias/
│       ├── diretrizes-codigo/     ← princípios de execução
│       │   └── SKILL.md
│       └── desafiador-ideias/     ← refinamento de ideias
│           └── SKILL.md
├── .devin/
│   └── skills/                   ← (mesma estrutura, se instalado)
├── AGENTS.md                     ← instruções para o agente (edite para seu projeto)
└── ... (arquivos do seu projeto)
```

---

## Atualizar para Nova Versão

```bash
# Repita o processo de instalação — os arquivos serão sobrescritos
git clone --depth=1 \
  --branch=claude/extract-sdd-skills-o9hxv \
  https://github.com/brunnobird/agent-skills-poc-tl.git _sdd_tmp

cp -r _sdd_tmp/kit-sdd-ptbr/skills/* .claude/skills/
# e/ou
cp -r _sdd_tmp/kit-sdd-ptbr/skills/* .devin/skills/
rm -rf _sdd_tmp
```

---

## Commitar os Skills no Repositório

Recomendamos versionar os skills junto com o código do projeto:

```bash
git add .claude/skills/ .devin/skills/ AGENTS.md
git commit -m "chore: adiciona kit SDD em PT-BR para Claude Code e Devin"
```

Assim toda a equipe tem acesso aos mesmos skills sem precisar instalar individualmente.
