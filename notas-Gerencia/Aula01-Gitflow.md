## Introdução

O Gitflow é um fluxo de trabalho legado do Git que originalmente era uma estratégia inovadora e disruptiva para gerenciar ramificações do Git. A popularidade do Gitflow caiu em favor dos [fluxos de trabalho baseados em trunk](https://www.atlassian.com/continuous-delivery/continuous-integration/trunk-based-development), que agora são consideradas práticas recomendadas para desenvolvimento de software contínuo moderno e práticas de [DevOps](https://www.atlassian.com/devops/what-is-devops).

## O que é Gitflow

O Gitflow é um modelo alternativo de ramificação do Git que envolve o uso de ramificações de recursos e várias ramificações primárias. Comparado ao desenvolvimento baseado em tronco, o Gitflow tem várias ramificações de vida mais longa e confirmações maiores.

O Gitflow pode ser usado para projetos que têm um ciclo de lançamento agendado e para a [prática recomendada de DevOps](https://www.atlassian.com/devops/what-is-devops/devops-best-practices) de [entrega contínua](https://www.atlassian.com/continuous-delivery). Este fluxo de trabalho não adiciona novos conceitos ou comandos além do que é necessário para o [Fluxo de trabalho do ramo de recursos](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow).

## Iniciando ...

O Gitflow é realmente apenas uma ideia abstrata de um fluxo de trabalho do Git. Isso significa que determina que tipo de branches configurar e como mesclá-los. Abordaremos os propósitos dos ramos abaixo. O conjunto de ferramentas git-flow é uma ferramenta de linha de comando real que possui um processo de instalação.

## Como isso funciona?

![img01](./images/svg01.svg)

### `develop` e `main` branches

Em vez de uma ramificação `main` única, esse fluxo de trabalho usa duas ramificações para registrar o histórico do projeto. A ramificação `main` armazena o histórico de lançamento oficial e a ramificação `develop` serve como uma ramificação de integração para recursos.

Também é conveniente marcar todos os commits no branch `main` com um número de versão.

## `feature` branches

Cada novo recurso deve residir em sua própria ramificação, que pode ser [enviada para o repositório central](https://www.atlassian.com/git/tutorials/syncing/git-push) para backup/colaboração. Mas, em vez de ramificar os branches `main`, `feature` usam `develop` como seu branch pai. Quando um recurso é concluído, ele é [mesclado novamente no desenvolvimento](https://www.atlassian.com/git/tutorials/using-branches/git-merge). Os recursos nunca devem interagir diretamente com a branch `main`.

![img02](./images/svg02.svg)

Observe que as ramificações `feature` combinadas com a ramificação `develop` é, para todos os efeitos, o fluxo de trabalho da ramificação de recursos. Mas o fluxo de trabalho do Gitflow não para por aí.

As branches `feature` geralmente são criados para o branch `develop` mais recente.

## `release` branches

![img03](./images/svg03.svg)

Uma vez que `develop` adquiriu recursos suficientes para um lançamento, você cria um branch `release` de `develop`.

A criação desta ramificação inicia o próximo ciclo de lançamento, portanto, nenhum novo recurso pode ser adicionado após este ponto - apenas correções de bugs, geração de documentação e outras tarefas orientadas à versão devem ser incluídas nesta ramificação.

Usar uma ramificação dedicada para preparar lançamentos permite que uma equipe aperfeiçoe o lançamento atual enquanto outra equipe continua trabalhando em recursos para o próximo lançamento.

Fazer ramificações `release` é outra operação de ramificação direta. Assim como os branches `feature` , os branches `release` são baseados no branch `develop` . Uma nova ramificação `release` pode ser criada usando os seguintes métodos.

Assim que a versão estiver pronta para envio, ela será mesclada em `main` e `develop`, então a ramificação `release` será excluída. É importante mesclar novamente em `develop` porque atualizações críticas podem ter sido adicionadas à ramificação `release` e precisam estar acessíveis para novos recursos.
## `hotfix` branches

![img04](./images/svg04.svg)

Ramos de manutenção ou `hotfix` são usados para corrigir rapidamente as versões de produção. Os branches `hotfix` são muito parecidos com os branches `release` e os branches `feature` , exceto que são baseados na branch `main`  em vez de `develop`. Esta é a única ramificação que deve ser bifurcada diretamente de `main`.

Ter uma linha de desenvolvimento dedicada para correções de bugs permite que sua equipe resolva problemas sem interromper o restante do fluxo de trabalho ou aguardar o próximo ciclo de lançamento. Você pode pensar em branches de manutenção como branches ad hoc `release` que funcionam diretamente com branch `main`.

## Resumo

O fluxo geral do Gitflow é:

1. Uma ramificação `develop` é criada a partir de `main`

2. Uma ramificação `release` é criada a partir de `develop`

3. As ramificações `feature` são criadas a partir `develop`

4. Quando uma `feature` é concluído, ela é mesclado no ramo `develop`

5. Quando a ramificação `release` é concluída, ela é mesclada em `develop` e `main`

6. Se um problema em `main` for detectado, uma ramificação `hotfix` será criada a partir de `main`

7. Depois que o `hotfix` é concluído, ele é mesclado com `develop` e `main`
