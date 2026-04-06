## Introdução {#intro}

Uma revisão de código é um processo em que alguém que não é o autor de um trecho de
código examina esse código.

No Google, usamos revisão de código para manter a qualidade do nosso código e dos
nossos produtos.

Esta documentação é a descrição canônica dos processos e políticas de revisão
de código do Google.



Esta página é uma visão geral do nosso processo de revisão de código. Há outros
dois documentos grandes que fazem parte deste guia:

-   **[Como Fazer Uma Revisão de Código](reviewer/index.md)**: Um guia detalhado
    para revisores de código.
-   **[O Guia do Autor da CL](developer/index.md)**: Um guia detalhado para
    desenvolvedores cujas CLs estão passando por revisão.

## O Que Os Revisores de Código Procuram? {#look_for}

As revisões de código devem observar:

-   **Design**: O código foi bem projetado e é apropriado para o seu sistema?
-   **Funcionalidade**: O código se comporta como o autor provavelmente
    pretendia? A forma como o código se comporta é boa para os usuários?
-   **Complexidade**: O código poderia ser simplificado? Outro desenvolvedor
    conseguiria entender e usar esse código com facilidade quando o encontrasse
    no futuro?
-   **Testes**: O código possui testes automatizados corretos e bem projetados?
-   **Nomenclatura**: O desenvolvedor escolheu nomes claros para variáveis,
    classes, métodos etc.?
-   **Comentários**: Os comentários são claros e úteis?
-   **Estilo**: O código segue nossos
    [guias de estilo](http://google.github.io/styleguide/)?
-   **Documentação**: O desenvolvedor também atualizou a documentação
    relevante?

Consulte **[Como Fazer Uma Revisão de Código](reviewer/index.md)** para obter
mais informações.

### Escolhendo Os Melhores Revisores {#best_reviewers}

Em geral, você quer encontrar os *melhores* revisores possíveis, capazes de
responder à sua revisão dentro de um prazo razoável.

O melhor revisor é a pessoa que conseguirá fazer a revisão mais completa e
correta do trecho de código que você está escrevendo. Normalmente isso significa
o(s) proprietário(s) do código, que podem ou não ser as pessoas listadas no
arquivo OWNERS. Às vezes isso significa pedir para pessoas diferentes revisarem
partes diferentes da CL.

Se você encontrar um revisor ideal, mas ele não estiver disponível, pelo menos
inclua-o em cópia no seu change.

### Revisões Presenciais (e Programação em Par) {#in_person}

Se você programou em par um trecho de código com alguém qualificado para fazer
uma boa revisão de código, então esse código é considerado revisado.

Você também pode fazer revisões presenciais, nas quais o revisor faz perguntas e
o desenvolvedor da mudança só fala quando for questionado.

## Veja Também {#seealso}

-   [Como Fazer Uma Revisão de Código](reviewer/index.md): Um guia detalhado
    para revisores de código.
-   [O Guia do Autor da CL](developer/index.md): Um guia detalhado para
    desenvolvedores cujas CLs estão passando por revisão.
