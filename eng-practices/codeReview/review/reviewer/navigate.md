# Navegando em uma CL em revisão



## Resumo

Agora que você sabe [o que procurar](looking-for.md), qual é a forma mais
 eficiente de gerenciar uma revisão espalhada por vários arquivos?

1.  A mudança faz sentido? Ela tem uma boa
    [descrição](../developer/cl-descriptions.md)?
2.  Veja primeiro a parte mais importante da mudança. O design geral está bom?
3.  Percorra o restante da CL em uma sequência apropriada.

## Etapa Um: Tenha uma visão ampla da mudança {#step_one}

Observe a [descrição da CL](../developer/cl-descriptions.md) e o que a CL faz
de modo geral. Essa mudança faz sentido? Se essa mudança não deveria ter
acontecido desde o começo, responda imediatamente com uma explicação de por que
a mudança não deveria estar acontecendo. Quando você rejeita uma mudança assim,
também é uma boa ideia sugerir ao desenvolvedor o que ele deveria ter feito em
vez disso.

Por exemplo, você poderia dizer: "Parece que você fez um bom trabalho aqui,
obrigado! No entanto, na verdade estamos indo na direção de remover o sistema
FooWidget que você está modificando aqui, então não queremos fazer nenhuma nova
modificação nele agora. Que tal, em vez disso, refatorar nossa nova classe
BarWidget?"

Observe que o revisor não apenas rejeitou a CL atual e deu uma sugestão
alternativa, mas fez isso com *cortesia*. Esse tipo de cortesia é importante
porque queremos mostrar que respeitamos uns aos outros como desenvolvedores,
mesmo quando discordamos.

Se você receber mais do que algumas CLs que representam mudanças que você não
quer fazer, considere reajustar o processo de desenvolvimento da sua equipe ou o
processo publicado para colaboradores externos, para que haja mais comunicação
antes de as CLs serem escritas. É melhor dizer às pessoas "não" antes que elas
tenham feito um monte de trabalho que agora precisa ser jogado fora ou
reescrito drasticamente.

## Etapa Dois: Examine as partes principais da CL {#step_two}

Encontre o arquivo ou os arquivos que são a parte "principal" desta CL.
Muitas vezes, há um arquivo que contém o maior número de mudanças lógicas, e
essa é a peça central da CL. Olhe essas partes principais primeiro. Isso ajuda a
dar contexto para todas as partes menores da CL e, em geral, acelera a revisão
de código. Se a CL for grande demais para você descobrir quais partes são as
principais, pergunte ao desenvolvedor o que você deve ver primeiro, ou peça que
ele [divida a CL em várias CLs](../developer/small-cls.md).

Se você perceber problemas de design importantes nessa parte da CL, envie esses
comentários imediatamente, mesmo que não tenha tempo para revisar o restante da
CL agora. Na verdade, revisar o restante da CL pode ser perda de tempo, porque
se os problemas de design forem graves o suficiente, grande parte do outro
código em revisão vai desaparecer e deixar de importar.

Há dois motivos principais para ser tão importante enviar esses comentários de
design maiores imediatamente:

-   Os desenvolvedores muitas vezes enviam uma CL e imediatamente começam um
    novo trabalho baseado nessa CL enquanto esperam a revisão. Se houver
    problemas de design grandes na CL que você está revisando, eles também terão
    de refazer a CL posterior. Você quer pegá-los antes que eles tenham feito
demais em cima do design problemático.
-   Mudanças de design grandes levam mais tempo para serem feitas do que mudanças
    pequenas. Quase todos os desenvolvedores têm prazos; para cumprir esses
    prazos e ainda ter código de qualidade na base, o desenvolvedor precisa
    começar o quanto antes qualquer grande retrabalho da CL.

## Etapa Três: Examine o restante da CL em uma sequência apropriada {#step_three}

Depois de confirmar que não há grandes problemas de design com a CL como um
 todo, tente descobrir uma sequência lógica para percorrer os arquivos sem
deixar de revisar nenhum. Normalmente, depois de olhar os arquivos principais, o
mais simples é apenas passar por cada arquivo na ordem em que a ferramenta de
revisão de código os apresenta. Às vezes também é útil ler primeiro os testes
antes de ler o código principal, porque assim você tem uma ideia do que a
mudança deveria fazer.

Próximo: [Velocidade das revisões de código](speed.md)
