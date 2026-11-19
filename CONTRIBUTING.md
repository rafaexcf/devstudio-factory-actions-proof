# Como contribuir

Este repositório é uma prova sintética de GitHub Actions. Não há aplicação para subir localmente.

- Abra pull requests contra o branch `pilot`. Não existe `main`.
- Não faça merge por conta própria se o pedido for só revisão ou documentação.
- Não coloque tokens, senhas, chaves ou connection strings em arquivos, issues ou logs.
- Não há variáveis de aplicação. Se alguma passar a existir, documente apenas o nome em `.env.example`.
- Preserve o workflow em `.github/workflows/receipt-proof.yml` a menos que a mudança de comportamento esteja explícita no pedido. Os jobs atuais não testam o produto; eles só executam as duas asserções descritas no README.
- Escreva documentação nova em português do Brasil e descreva só o que o código faz.
