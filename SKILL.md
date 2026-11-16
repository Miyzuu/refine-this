---
name: refine-this
description: Melhora o design e a UX/UI de um site existente sem deixar cara de template ou de "design de IA". Avalia o site pelas 12 leis de UX, roda a skill unslop, consulta a documentação atual pelo Context7, valida cada mudança com o Playwright em desktop, tablet e celular, e só altera algo depois que o usuário aprova. Use quando pedirem para refinar, polir, revisar ou melhorar o design, a UX ou a UI de um site ou landing page.
---

# refine-this

Deixa um site mais claro, mais fácil de usar e com aparência intencional, sempre fiel ao que o dono pediu. Nada muda sem aprovação.

## Antes de começar: dependências

Toda vez, confira quais ferramentas existem nesta sessão. Se faltar alguma, avise antes de tudo: "Esta skill roda melhor com o plugin Playwright, o plugin Context7 e a skill unslop. Falta: [lista]." Em seguida, pergunte (múltipla escolha):

- **Instalar o que falta (Recomendado):** mostre os comandos abaixo e espere a confirmação.
- **Rodar sem dependências:** siga no modo sem dependências.

Fora do Claude Code, não use os comandos `/plugin`. Procure ferramentas equivalentes (servidor MCP de navegador ou de documentação) e diga quais achou.

| Ferramenta | Para quê | Como instalar |
|---|---|---|
| Plugin **Playwright** | abrir o site, tirar prints, ler o console, clicar | `/plugin install playwright@claude-plugins-official` |
| Plugin **Context7** | documentação atual do framework antes de escrever código | `/plugin install context7@claude-plugins-official` |
| Skill **unslop** | achar e corrigir padrões genéricos de "design de IA" | `git clone https://github.com/heydamir/unslop` e copiar `unslop/skills/unslop` para `~/.claude/skills/` |

Se o marketplace oficial não aparecer, adicione-o antes com `/plugin marketplace add anthropics/claude-plugins-official`. Plugins novos só carregam depois de reiniciar o Claude Code.

### Modo sem dependências
- **Sem Playwright:** use qualquer navegador disponível na sessão. Sem nenhum, revise só o código e marque cada item como "não validado visualmente".
- **Sem unslop:** use a lista de padrões de [references/regras.md](references/regras.md).
- **Sem Context7:** leia a versão no `package.json` e a documentação que vem instalada junto com o pacote.
- **Nunca diga que testou algo que não testou.**

## Regras fixas

1. **Nada muda sem aprovação explícita do usuário.** Entregue uma etapa por vez e espere o "sim" antes de seguir.
2. **Toda sugestão cita a lei de UX que a justifica** (ver [references/leis-ux.md](references/leis-ux.md)). Exemplo: "Lei de Hick: menu de 9 para 5 itens, menos tempo para decidir".
3. **Siga as regras de design, de texto e de credibilidade** de [references/regras.md](references/regras.md) em toda proposta e em todo código. Não invente funcionalidades. Se faltar informação, pergunte.
4. **Preserve** marca, identidade visual e funcionalidades existentes, a menos que o usuário aprove a mudança.
5. **Se o site não abrir ou o navegador falhar,** avise e pergunte como seguir. Não suponha.
6. **Antes de escrever código de um framework ou biblioteca** (Next.js, React, Tailwind etc.), consulte a documentação atual pelo Context7. Confira também a versão no `package.json`.
7. **Segurança:** não leia nem edite `.env`, chaves ou segredos. Não rode comandos destrutivos (apagar arquivos, `git reset --hard`, push forçado).
8. **Escreva em português, de forma direta e simples.** Faça resumos em checklist.

## Fluxo

### 1. Entender o negócio
- Leia o pedido do usuário e o site. Resuma em 3 a 5 linhas: o que o negócio faz, para quem, o tom visual e as restrições.
- Faça **até 5 perguntas** sobre o que falta (público, diferencial, prova real disponível, paleta, prioridade entre seções). Se a ferramenta de perguntas estiver disponível, use múltipla escolha. Não escreva código antes das respostas.
- Se for uma nova rodada, compare com a anterior e diga o que mudou no site.

### 2. Diagnóstico
1. **Playwright.** Abra o site e tire prints em **1440, 768 e 375px**, salvos em `refine-this/antes/<pagina>-<largura>.png`. Anote:
   - hierarquia visual
   - contraste (WCAG AA: 4,5:1 para texto normal, 3:1 para texto grande)
   - espaçamento, tipografia e alinhamento
   - alvos de toque (mínimo de 24×24px pela WCAG 2.2 AA; recomendado 44×44px)
   - estados de hover, foco e erro
   - navegação só pelo teclado (Tab, Enter, Esc), com foco sempre visível
   - nomes acessíveis em botões, ícones e campos; HTML semântico (`header`, `nav`, `main`, `button`, `label`)
   - mensagens de erro claras, presas ao campo certo
   - erros no console
   - requisições que falham
   - tempo até o conteúdo aparecer
2. **unslop.** Rode a auditoria do unslop (etapas "Look" e "Audit" dele) para listar os padrões genéricos que existem hoje.
3. **Leis de UX.** Avalie o site com as 12 leis de [references/leis-ux.md](references/leis-ux.md), usando as perguntas de lá.
4. **Checklist de "pronto".** Marque o que já existe e o que falta (ver [references/regras.md](references/regras.md)).

### 3. Relatório
- **A avaliação das 12 leis,** no formato de [references/leis-ux.md](references/leis-ux.md): nota por lei, as 5 mudanças de maior impacto e a proposta de título, subtítulo e botão.
- **Padrões genéricos achados pelo unslop.**
- **Itens do checklist de "pronto" que faltam,** separando o que depende do usuário.

### 4. Escolha
Primeiro, pergunte se o usuário quer seguir para as mudanças ou **parar no diagnóstico**. Se ele parar, pule para a entrega final.

No máximo 5 mudanças por rodada. Faça uma pergunta de múltipla escolha para cada uma, com até 4 por vez:

- **A) Manter como está:** prós e contras
- **B) e C) Alternativas:** prós e contras de cada uma
- A opção recomendada vem primeiro, marcada **(Recomendado)**, com o motivo ligado à lei de UX e ao pedido do usuário.

### 5. Aplicar e validar
1. Aplique **só** o que foi aprovado, uma mudança ou um lote pequeno por vez.
2. Antes de editar um arquivo, guarde uma cópia em `refine-this/backup/`, mesmo com git. Assim, desfazer é sempre possível.
3. Siga a ordem de passes do unslop (espaçamento, cor, ícones, texto, tipografia, layout, detalhes, visuais, movimento) dentro do que foi aprovado.
4. Valide com o Playwright:
   - prints **depois** nas 3 larguras, em `refine-this/depois/`
   - console sem erros novos
   - links e interações principais funcionando
5. Confira se o resultado continua fiel ao pedido original. Se divergir, avise e proponha a correção no formato da etapa 4.

### 6. Entrega final
Devolva um checklist com:
- [x] **O que foi feito:** cada mudança com a lei de UX correspondente
- [ ] **O que está pendente**
- [ ] **O que depende do usuário:** domínio, fotos, depoimentos reais, dados do rodapé etc.
- **Mudanças recusadas,** para revisar depois
- **Pares antes/depois:** caminhos dos prints em `refine-this/antes/` e `refine-this/depois/`
