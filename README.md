# devstudio-factory-actions-proof

Repositório sintético de prova de integração de recibos do GitHub Actions. Contém somente o workflow em `.github/workflows/receipt-proof.yml`. Não há código de produto, segredos nem deploy.

Repositório: https://github.com/rafaexcf/devstudio-factory-actions-proof

## O que é

Artefato de teste para uma integração local de recibos de CI. O próprio workflow se descreve como prova: um job confere se o SHA do commit tem 40 caracteres e outro confere a expressão `6 * 7 = 42`. Nada além disso é executado.

## Público

Uso interno de quem opera essa prova de CI. Não há interface, conta de usuário nem documentação de produto voltada a clientes.

## Status

Protótipo de infraestrutura. Não é uma aplicação em produção, beta ou piloto de produto. O branch padrão do GitHub é `pilot`. Não existe branch `main`.

A única execução registrada do workflow, em 15 de novembro de 2026, terminou com sucesso em cerca de 8 segundos: https://github.com/rafaexcf/devstudio-factory-actions-proof/actions/runs/43739681979

## Domínios e URLs

| Item | Situação |
| --- | --- |
| Domínio de produção | Nenhum. Não há `vercel.json`, `wrangler.toml`, `capacitor.config`, `app.json` nem outro manifesto de hospedagem. |
| URL de privacidade | Nenhuma no código. |
| Homepage do GitHub | Vazia no momento desta revisão. |
| Repositório | https://github.com/rafaexcf/devstudio-factory-actions-proof |

Não foi feita requisição HTTP a um domínio de produto porque nenhum domínio aparece na árvore. Presença de domínio fora deste repositório: a confirmar.

## Stack

| Camada | O que existe aqui |
| --- | --- |
| Linguagem de aplicação | Nenhuma. Os passos são shell POSIX (`test`) dentro do runner. |
| Framework | Nenhum. |
| Banco de dados | Nenhum. |
| Autenticação | Nenhuma. |
| Hospedagem de aplicação | Nenhuma. O CI usa `ubuntu-latest` no GitHub Actions. |
| Pagamentos | Nenhum. |
| Analytics | Nenhum. |
| CI | GitHub Actions, workflow `Receipt proof`. |
| Pacote Android / Play Store | Não é aplicativo Android. Sem package name e sem ficha na Play Store. |

## Arquitetura

O evento `push` dispara dois jobs independentes, cada um com `timeout-minutes: 2` e `runs-on: ubuntu-latest`. O workflow declara `permissions: {}`, então o `GITHUB_TOKEN` do job não recebe escopos.

```text
push
 ├── build (Build proof)  → test de que ${#GITHUB_SHA} é 40
 └── tests (Test proof)   → test de que $((6 * 7)) é 42
```

Nenhum job faz checkout do repositório, não usa actions de terceiros (`uses:`) e não publica artefato.

## Como rodar localmente

Não há servidor, instalador nem dependências. As duas asserções do workflow podem ser reproduzidas no shell. `GITHUB_SHA` só existe dentro do Actions; localmente use um SHA de 40 caracteres:

```bash
SHA=c2642bef0791a2df90710db0843dd6014c658f1a
test "${#SHA}" -eq 40 && echo "sha ok"
test "$((6 * 7))" -eq 42 && echo "contrato ok"
```

O arquivo YAML foi conferido com o parser da PyYAML nesta revisão. Não há comando de build.

## Variáveis de ambiente

Nenhuma variável de aplicação é necessária. A lista está em [`.env.example`](.env.example).

O workflow lê somente `GITHUB_SHA`, injetada pelo GitHub Actions. Não defina segredos neste repositório.

## Scripts

Não há `package.json`, `Makefile`, `pyproject.toml` nem scripts de build, lint ou teste locais. O único automatismo versionado é `.github/workflows/receipt-proof.yml`.

## Testes

| Verificação | Onde | O que afirma |
| --- | --- | --- |
| Build proof | job `build` | O SHA do commit tem 40 caracteres. |
| Test proof | job `tests` | A expressão aritmética `6 * 7` vale 42. |

Não há framework de teste, cobertura nem suíte que leia os arquivos do repositório.

## Deploy

Não há pipeline de deploy, ambiente de preview nem domínio ligado a este código. Não altere DNS, produção, banco, cobrança ou segredos a partir daqui: este repositório não tem esses sistemas.

## Licença

Propriedade de Metaquantics Technologies. Veja [LICENSE](LICENSE).

## Contribuir

Veja [CONTRIBUTING.md](CONTRIBUTING.md). A avaliação do estado do código, da segurança e dos riscos está em [docs/REVISAO.md](docs/REVISAO.md).
