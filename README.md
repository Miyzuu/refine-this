# refine-this

Skill do [Claude Code](https://claude.com/claude-code) que melhora o design e a UX/UI de um site existente sem deixar cara de template ou de "design de IA".

- Avalia o site pelas 12 leis de UX; cada lei recebe uma nota de 0 a 10 por uma régua fixa, com evidência e a correção exata.
- Confere acessibilidade:
  - contraste e alvo de toque (WCAG 2.2 AA)
  - teclado e foco visível
  - nomes acessíveis e HTML semântico
  - mensagens de erro
- Usa a skill [unslop](https://github.com/heydamir/unslop) para achar padrões genéricos de "design de IA", sem tratar como erro o que já é identidade da marca.
- Consulta a documentação atual do framework pelo Context7 antes de escrever código.
- Valida cada mudança com o Playwright em 1440, 768 e 375px, com prints de antes e depois.
- **Só altera algo depois que você aprova**, escolhendo entre opções de múltipla escolha. Também dá para parar só no diagnóstico.
- Não inventa depoimentos, números nem clientes. Não mexe em `.env` nem em segredos, e não roda comandos destrutivos.

## Instalação

```bash
git clone https://github.com/Miyzuu/refine-this ~/.claude/skills/refine-this
```

Para atualizar depois: `git -C ~/.claude/skills/refine-this pull`.

### Dependências recomendadas (opcionais)

A skill funciona sem elas, mas fica melhor com elas. Se faltar alguma, ela avisa no começo e pergunta se você quer instalar ou seguir sem. Sem dependências, ela:
- usa o navegador que houver na sessão, ou só revisa o código, marcando o que não foi validado visualmente;
- usa a própria lista de padrões no lugar do unslop;
- lê a documentação instalada junto com os pacotes no lugar do Context7.

Para instalar, dentro do Claude Code:

```
/plugin marketplace add anthropics/claude-plugins-official
/plugin install playwright@claude-plugins-official
/plugin install context7@claude-plugins-official
```

E a skill unslop, no terminal:

```bash
git clone https://github.com/heydamir/unslop
cp -r unslop/skills/unslop ~/.claude/skills/
```

Reinicie o Claude Code para os plugins carregarem. Fora do Claude Code, a skill procura ferramentas equivalentes, como um servidor MCP de navegador ou de documentação.

## Uso

```
/refine-this melhore o design da minha landing page
```

A skill trabalha nesta ordem:

1. Confere as dependências e avisa se faltar alguma.
2. Resume o seu pedido e faz até 5 perguntas sobre o negócio.
3. Faz o diagnóstico: prints, acessibilidade, unslop, 12 leis de UX e checklist de "pronto".
4. Entrega o relatório: nota por lei, as 5 mudanças de maior impacto e uma proposta de título, subtítulo e botão.
5. Pergunta se você quer parar no diagnóstico ou escolher as mudanças (no máximo 5 por rodada).
6. Aplica só o que você aprovou, com backup antes de cada edição, e valida com prints de antes e depois.
7. Devolve um checklist com o que foi feito, o que está pendente, o que depende de você e o que foi recusado.

Os prints e os backups ficam na pasta `refine-this/` do projeto.

## Arquivos

- `SKILL.md`: dependências, regras fixas e o fluxo
- `references/leis-ux.md`: as 12 leis de UX, a régua das notas e o formato da avaliação (definições adaptadas de [Laws of UX](https://lawsofux.com), de Jon Yablonski)
- `references/regras.md`: regras de design, texto e credibilidade, e o checklist antes de publicar

## Licença

MIT
