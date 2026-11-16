# Regras que valem em toda proposta e em todo código

## Design (nunca faça)
Exceção: se um destes itens já faz parte da identidade da marca (ex.: o roxo é a cor oficial), ele não é "slop". Mantenha e, no máximo, sugira um refinamento.

- **Gradientes roxos ou azul-roxo genéricos.**
- **Botões em formato de pílula em todo lugar.** Escolha um formato de botão coerente com a marca e use sempre o mesmo.
- **Emojis no lugar de ícones.** Use um único conjunto de ícones consistente, como o que o projeto já usa ou Lucide, Phosphor ou Heroicons.
- **Animações de rolagem exageradas ou animações no cursor.** Respeite `prefers-reduced-motion`.
- **Fotos genéricas ou imagens "lixo" geradas por IA.** Se faltar imagem, diga ao usuário o que fotografar ou use um espaço reservado claro (ex.: `[FOTO: fachada da loja, horizontal]`).
- **Página cheia de cartões idênticos e seções repetidas.**

## Texto (nunca faça)
- **Frases vagas no topo da página**, como "Soluções inovadoras para o seu futuro". O título principal diz o que o negócio faz e para quem.
- **Travessões em excesso ou o estilo típico de texto de IA:** "não é só X, é Y", listas de três adjetivos, "eleve", "transforme", "desbloqueie".
- **Texto genérico que serviria para qualquer empresa.** Use as informações do negócio.

## Credibilidade (nunca faça)
- **Inventar avaliações, depoimentos, nomes de clientes ou logos de clientes.**
- **Inventar números, métricas, selos ou prêmios.**
- **Sem prova real ainda,** deixe um espaço marcado como `[PREENCHER COM DEPOIMENTO REAL]` e explique o que coletar: nome, cargo ou cidade, foto com autorização e uma frase sobre o resultado concreto.

## Pontos de publicação a verificar
Não são exigências gerais. Cada item depende do contexto do site, e a skill pergunta ao usuário antes de marcar algo como pendente. Nenhum deles bloqueia o refinamento de design.
- [ ] **Domínio próprio:** verificar se o site vai ao ar e, se sim, se o domínio já existe.
- [ ] **Favicon** (o ícone da aba), também em 180×180 para `apple-touch-icon`.
- [ ] **Nenhuma etiqueta ou selo** "feito com IA" ou do construtor do site.
- [ ] **Página de política de privacidade.** No Brasil, segue a LGPD (Lei 13.709/2018) e informa quais dados são coletados, para quê, por quanto tempo e como pedir a exclusão.
- [ ] **Termos de uso:** verificar se o site coleta dados, vende ou tem cadastro. Se sim, perguntar ao usuário se quer incluir a página.
- [ ] **Identificação no rodapé (contato e documento):** perguntar ao usuário quais dados quer exibir e se a atividade exige algum documento, como CNPJ ou CPF. Use `[PREENCHER]` e não invente.
- [ ] **Testado no celular e no computador.** Prints do Playwright em 375, 768 e 1440px.

Textos legais (privacidade e termos) são um modelo inicial. Avise o usuário para revisar com um profissional.
