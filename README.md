# refine-this

Skill para agentes de código (Claude Code, Codex, Cursor, Copilot, entre outros) que melhora o design e a UX/UI de um site existente sem deixar cara de template ou de "design de IA".

Ela é escrita em Markdown puro, então funciona em qualquer agente que lê instruções de arquivo. Foi testada até agora só no Claude Code.

- Avalia o site pelas 12 leis de UX; cada lei recebe uma nota de 0 a 10 por uma régua fixa, com evidência e a correção exata.
- Confere acessibilidade: contraste e alvo de toque (WCAG 2.2 AA), teclado e foco visível, nomes acessíveis, HTML semântico e mensagens de erro.
- Usa o unslop para achar padrões genéricos de "design de IA", sem tratar como erro o que já é identidade da marca.
- Consulta a documentação atual do framework antes de escrever código, quando o agente tiver uma ferramenta para isso.
- Valida cada mudança no navegador em 1440, 768 e 375px, com prints de antes e depois.
- **Só altera algo depois que você aprova**, escolhendo entre opções. Também dá para parar só no diagnóstico.
- Não inventa depoimentos, números nem clientes. Não mexe em `.env` nem em segredos, e não roda comandos destrutivos.

## Instalação

1. Copie a pasta `refine-this` para a pasta de skills do seu agente.

   No Claude Code:

   ```bash
   git clone https://github.com/Miyzuu/refine-this ~/.claude/skills/refine-this
   ```

   Em outros agentes, copie a pasta para o local equivalente (ou cole o conteúdo de `SKILL.md` nas instruções do agente, como `AGENTS.md`, regras do Cursor ou instruções do Copilot). Os arquivos de `references/` precisam ficar junto do `SKILL.md`.

2. Para atualizar depois: `git -C <pasta-da-skill> pull`.

### Ferramentas recomendadas (opcionais)

A skill funciona sem elas, mas rende mais com elas. Se faltar alguma, ela avisa no começo e pergunta se você quer instalar ou seguir sem. Sem elas, ela:
- usa o navegador que houver na sessão, ou só revisa o código, marcando o que não foi validado visualmente;
- usa a própria lista de padrões no lugar do unslop;
- lê a documentação instalada junto com os pacotes no lugar do Context7.

Exemplo no Claude Code, dentro do próprio app:

```
/plugin marketplace add anthropics/claude-plugins-official
/plugin install playwright@claude-plugins-official
/plugin install context7@claude-plugins-official
```

E o unslop, no terminal:

```bash
git clone https://github.com/heydamir/unslop
cp -r unslop/skills/unslop ~/.claude/skills/
```

Reinicie o agente depois de instalar os plugins.

## Uso

No Claude Code:

```
/refine-this melhore o design da minha landing page
```

Em outros agentes, peça a mesma coisa em linguagem natural e mencione a skill pelo nome.

A skill trabalha nesta ordem:

1. Confere as ferramentas e avisa se faltar alguma.
2. Resume o seu pedido e faz até 5 perguntas sobre o negócio.
3. Faz o diagnóstico: prints, acessibilidade, unslop, 12 leis de UX e checklist de "pronto".
4. Entrega o relatório: nota por lei, as 5 mudanças de maior impacto e uma proposta de título, subtítulo e botão.
5. Pergunta se você quer parar no diagnóstico ou escolher as mudanças (no máximo 5 por rodada).
6. Aplica só o que você aprovou, com backup antes de cada edição, e valida com prints de antes e depois.
7. Devolve um checklist com o que foi feito, o que está pendente, o que depende de você e o que foi recusado.

Os prints e os backups ficam na pasta `refine-this/` do projeto.

## Arquivos

- `SKILL.md`: ferramentas, regras fixas e o fluxo
- `references/leis-ux.md`: as 12 leis de UX, a régua das notas e o formato da avaliação (definições adaptadas de [Laws of UX](https://lawsofux.com), de Jon Yablonski)
- `references/regras.md`: regras de design, texto e credibilidade, e o checklist antes de publicar

## Licença

MIT
