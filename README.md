# refine-this

Skill do [Claude Code](https://claude.com/claude-code) que melhora o design e a UX/UI de um site existente sem deixar cara de template ou de "design de IA".

- Avalia o site pelas 12 leis de UX, com nota de 0 a 10 e a correção exata de cada uma.
- Usa a skill [unslop](https://github.com/heydamir/unslop) para achar padrões genéricos de "design de IA".
- Consulta a documentação atual do framework pelo Context7 antes de escrever código.
- Valida cada mudança com o Playwright em 1440, 768 e 375px, com prints de antes e depois.
- **Só altera algo depois que você aprova**, escolhendo entre opções de múltipla escolha.
- Funciona sem dependências: se faltar Playwright, Context7 ou unslop, ela avisa e pergunta se você quer instalar ou seguir sem. Também dá para parar só no diagnóstico.

## Instalação

1. Instale a skill:

   ```bash
   git clone https://github.com/Miyzuu/refine-this ~/.claude/skills/refine-this
   ```

2. Instale as dependências dentro do Claude Code:

   ```
   /plugin marketplace add anthropics/claude-plugins-official
   /plugin install playwright@claude-plugins-official
   /plugin install context7@claude-plugins-official
   ```

3. Instale a skill unslop:

   ```bash
   git clone https://github.com/heydamir/unslop
   cp -r unslop/skills/unslop ~/.claude/skills/
   ```

4. Reinicie o Claude Code para os plugins carregarem.

Para atualizar a skill depois: `git -C ~/.claude/skills/refine-this pull`.

## Uso

```
/refine-this melhore o design da minha landing page
```

A skill trabalha nesta ordem:

1. Resume o seu pedido e faz até 5 perguntas sobre o negócio.
2. Faz o diagnóstico do site.
3. Entrega o relatório.
4. Pergunta o que aplicar.
5. Aplica e valida o que você aprovou.
6. Devolve um checklist do que foi feito, do que está pendente e do que depende de você.

## Arquivos

- `SKILL.md`: o fluxo e as regras fixas
- `references/leis-ux.md`: as 12 leis de UX (definições adaptadas de [Laws of UX](https://lawsofux.com), de Jon Yablonski)
- `references/regras.md`: as regras de design, texto e credibilidade, e o checklist antes de publicar

## Licença

MIT
