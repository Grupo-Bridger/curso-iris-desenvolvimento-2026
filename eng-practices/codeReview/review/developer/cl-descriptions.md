# Escrevendo boas descrições de CL



Uma descrição de CL é um registro público da mudança, e é importante que ela
comunique:

1.  **O que** está sendo alterado? Isso deve resumir as principais mudanças de
    forma que os leitores entendam o que está sendo alterado sem precisar ler a
    CL inteira.

1.  **Por que** essas mudanças estão sendo feitas? Que contexto você tinha como
    autor ao fazer essa mudança? Houve decisões que você tomou e que não estão
    refletidas no código-fonte? etc.

A descrição da CL se tornará parte permanente do nosso histórico de controle de
versão e poderá ser lida por centenas de pessoas ao longo dos anos.

Desenvolvedores futuros vão procurar sua CL com base na descrição. Alguém no
futuro pode estar procurando sua mudança por causa de uma lembrança vaga de sua
relevância, mas sem ter os detalhes à mão. Se todas as informações importantes
estiverem no código e não na descrição, vai ser muito mais difícil localizar a
sua CL.

E então, depois que encontrarem a CL, conseguirão entender *por que* a mudança
foi feita? Ler o código-fonte pode revelar o que o software faz, mas talvez não
revele por que ele existe, o que pode dificultar para futuros desenvolvedores
saberem se podem mover
[Cerca de Chesterton](https://abseil.io/resources/swe-book/html/ch03.html#understand_context).

Uma descrição bem escrita da CL ajudará esses futuros engenheiros — às vezes,
inclusive você mesmo!

## Primeira Linha {#first-line}

<a id="firstline"></a> <!-- Keep previous permalink to avoid breaking old links. -->

*   Resumo curto do que está sendo feito.
*   Frase completa, escrita como se fosse uma ordem.
*   Seguido por uma linha em branco.

A **primeira linha** de uma descrição de CL deve ser um resumo curto do que
*especificamente* **está sendo feito pela CL**, seguido por uma linha em branco.
Isso é o que aparece nos resumos do histórico de controle de versão, então deve
ser informativo o suficiente para que quem estiver pesquisando no histórico não
precise ler a sua CL ou a descrição inteira para entender o que a CL realmente
*fez* ou como ela difere de outras CLs. Em outras palavras, a primeira linha
deve se sustentar sozinha, permitindo que os leitores percorram o histórico de
código muito mais rapidamente.

Tente manter sua primeira linha curta, focada e direta. A clareza e a utilidade
para o leitor devem ser a principal preocupação.

Por tradição, a primeira linha de uma descrição de CL é uma frase completa,
escrita como se fosse uma ordem (uma frase no imperativo). Por exemplo, diga
"**Delete** a RPC FizzBuzz e **substitua-a** pelo novo sistema." em vez de
"**Deletando** a RPC FizzBuzz e **substituindo-a** pelo novo sistema." Você não
precisa escrever o restante da descrição como uma frase no imperativo, embora
possa.

## O Corpo é Informativo {#informative}

A [primeira linha](#first-line) deve ser um resumo curto e focado, enquanto o
restante da descrição deve preencher os detalhes e incluir qualquer informação
suplementar que o leitor precise para entender a CL como um todo. Isso pode
incluir uma breve descrição do problema que está sendo resolvido e por que essa
é a melhor abordagem. Se houver limitações na abordagem, elas devem ser
mencionadas. Se for relevante, inclua informações de contexto como números de
bug, resultados de benchmark e links para documentos de design.

Se você incluir links para recursos externos, considere que eles talvez não
efetuem para leitores futuros devido a restrições de acesso ou políticas de
retenção. Sempre que possível, inclua contexto suficiente para que revisores e
leitores futuros entendam a CL.

Mesmo CLs pequenas merecem um pouco de atenção aos detalhes. Coloque a CL em
contexto.

## Más Descrições de CL {#bad}

"Corrigir bug" é uma descrição inadequada de CL. Qual bug? O que você fez para
corrigi-lo? Outras descrições igualmente ruins incluem:

-   "Corrigir build."
-   "Adicionar patch."
-   "Movendo código de A para B."
-   "Fase 1."
-   "Adicionar funções de conveniência."
-   "matar URLs estranhas."

Algumas dessas são descrições reais de CL. Embora curtas, elas não fornecem
informação útil suficiente.

## Boas Descrições de CL {#good}

Aqui estão alguns exemplos de boas descrições.

### Mudança de funcionalidade {#functionality-change}

Exemplo:

> RPC: Remover o limite de tamanho da freelist de mensagens do servidor RPC.
>
> Servidores como o FizzBuzz têm mensagens muito grandes e se beneficiariam da
> reutilização. Tornar a freelist maior e adicionar uma goroutine que libera os
> itens da freelist lentamente ao longo do tempo, para que servidores ociosos
> acabem liberando todos os itens da freelist.

As primeiras palavras descrevem o que a CL realmente faz. O restante da
descrição fala sobre o problema que está sendo resolvido, por que essa é uma boa
solução e um pouco mais de informação sobre a implementação específica.

### Refatoração {#refactoring}

Exemplo:

> Construir uma Task com um TimeKeeper para usar seus métodos TimeStr e Now.
>
> Adicionar um método Now à Task, para que o método getter borglet() possa ser
> removido (ele era usado apenas por OOMCandidate para chamar o método Now do
> borglet). Isso substitui os métodos em Borglet que delegam a um TimeKeeper.
>
> Permitir que Tasks forneçam Now é um passo em direção a eliminar a dependência
> de Borglet. No futuro, colaboradores que dependem de obter Now a partir da
> Task devem passar a usar um TimeKeeper diretamente, mas isso tem sido uma
> adaptação para permitir a refatoração em pequenos passos.
>
> Continuando a meta de longo prazo de refatorar a Hierarquia Borglet.

A primeira linha descreve o que a CL faz e como isso muda em relação ao passado.
O restante da descrição fala sobre a implementação específica, o contexto da
CL, o fato de a solução não ser ideal e a direção futura possível. Também
explica *por que* essa mudança está sendo feita.

### Pequena CL que precisa de algum contexto

Exemplo:

> Criar uma regra de build em Python3 para status.py.
>
> Isso permite que consumidores que já estejam usando isso em Python3 dependam de
> uma regra que fica ao lado da regra de build original em vez de estar em algum
> lugar na própria árvore deles. Isso incentiva novos consumidores a usar
> Python3, se puderem, em vez de Python2, e simplifica significativamente algumas
> ferramentas automatizadas de refatoração de arquivos de build que estão sendo
> desenvolvidas atualmente.

A primeira frase descreve o que está realmente sendo feito. O restante da
descrição explica *por que* a mudança está sendo feita e dá ao revisor bastante
contexto.

## Usando tags {#tags}

Tags são rótulos inseridos manualmente que podem ser usados para categorizar
CLs. Elas podem ser suportadas por ferramentas ou usadas apenas por convenção da
equipe.

Por exemplo:

-   "[tag]"
-   "[uma tag mais longa]"
-   "#tag"
-   "tag:"

Usar tags é opcional.

Ao adicionar tags, considere se elas devem estar no [corpo](#informative) da
descrição da CL ou na [primeira linha](#first-line). Limite o uso de tags na
primeira linha, porque isso pode obscurecer o conteúdo.

Exemplos com e sem tags:

``` {.good}
// Tags são aceitáveis na primeira linha se forem curtas.
[banana] Descasque a banana antes de comer.

// Tags podem aparecer no meio do conteúdo.
Descasque a #banana antes de comer.

// Tags são opcionais.
Descasque a banana antes de comer.

// Várias tags são aceitáveis se forem curtas.
#banana #apple: Monte uma cesta de frutas.

// Tags podem aparecer em qualquer lugar da descrição da CL.
> Monte uma cesta de frutas.
>
> #banana #apple
```

``` {.bad}
// Tags demais (ou tags muito longas) sobrecarregam a primeira linha.
//
// Em vez disso, considere se as tags podem ser movidas para o corpo da
// descrição e/ou encurtadas.
[banana peeler factory factory][apple picking service] Monte uma cesta de frutas.
```

## Descrições de CL geradas

Algumas CLs são geradas por ferramentas. Sempre que possível, as descrições
delas também devem seguir as orientações aqui. Ou seja, a primeira linha deve
ser curta, focada e se sustentar sozinha, e o corpo da descrição deve incluir
detalhes informativos que ajudem revisores e futuros pesquisadores de código a
entender o efeito de cada CL.

## Revise a descrição antes de enviar a CL

CLs podem mudar bastante durante a revisão. Pode valer a pena revisar a
descrição de uma CL antes de enviá-la, para garantir que ela ainda reflita o que
a CL realmente faz.

Próximo: [CLs pequenas](small-cls.md)
