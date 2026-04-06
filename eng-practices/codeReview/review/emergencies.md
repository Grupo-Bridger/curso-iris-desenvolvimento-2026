# Emergências

Às vezes há CLs de emergência que precisam passar por todo o processo de
revisão de código o mais rápido possível.



## O Que É Uma Emergência? {#what}

Uma CL de emergência seria uma mudança **pequena** que: permite que um grande
lançamento continue em vez de ser revertido, corrige um bug que afeta
significativamente os usuários em produção, trata de uma questão jurídica
urgente, fecha uma grande falha de segurança etc.

Em emergências, de fato nos importamos com a velocidade de todo o processo de
revisão de código, e não apenas com a [velocidade de resposta](reviewer/speed.md).
Nesse caso *somente*, o revisor deve se importar mais com a velocidade da
revisão e com a correção do código (ele realmente resolve a emergência?) do que
com qualquer outra coisa. Além disso (talvez seja óbvio), essas revisões devem
ter prioridade sobre todas as outras revisões de código quando aparecerem.

No entanto, depois que a emergência for resolvida, você deve revisar as CLs de
emergência novamente e dar a elas uma [revisão mais completa](reviewer/looking-for.md).

## O Que NÃO É Uma Emergência? {#not}

Para deixar claro, os casos a seguir *não* são uma emergência:

-   Querer lançar nesta semana em vez da próxima (a menos que exista algum
    [prazo rígido](#deadlines) real para o lançamento, como um acordo com um
    parceiro).
-   O desenvolvedor trabalhou em uma funcionalidade por muito tempo e quer muito
    que a CL entre.
-   Todos os revisores estão em outro fuso horário, onde é noite, ou estão fora
    do escritório em um evento externo.
-   É o fim da tarde de uma sexta-feira e seria ótimo conseguir incluir essa CL
    antes de o desenvolvedor sair para o fim de semana.
-   Um gerente diz que essa revisão precisa ser concluída e que a CL deve ser
    integrada hoje por causa de um [prazo flexível, não rígido](#deadlines).
-   Reverter uma CL que está causando falhas de teste ou quebras de compilação.

E assim por diante.

## O Que É Um Prazo Rígido? {#deadlines}

Um prazo rígido é aquele em que **algo desastroso aconteceria** se você o
perdesse. Por exemplo:

-   Enviar sua CL até uma determinada data é necessário para cumprir uma
    obrigação contratual.
-   Seu produto falhará completamente no mercado se não for lançado até uma
    determinada data.
-   Alguns fabricantes de hardware só lançam novo hardware uma vez por ano. Se
    você perder o prazo para enviar o código para eles, isso pode ser desastroso,
    dependendo do tipo de código que você está tentando entregar.

Atrasar um lançamento por uma semana não é desastroso. Perder uma conferência
importante pode ser desastroso, mas muitas vezes não é.

A maioria dos prazos é flexível, não rígida. Eles representam o desejo de que
uma funcionalidade fique pronta até certo momento. São importantes, mas você
não deveria sacrificar a saúde do código para cumpri-los.

Se você tiver um ciclo de lançamento longo (várias semanas), pode ser tentador
sacrificar a qualidade da revisão de código para incluir uma funcionalidade
antes do próximo ciclo. No entanto, esse padrão, se repetido, é uma maneira
comum de os projetos acumularem uma dívida técnica enorme. Se os
 desenvolvedores estiverem enviando CLs rotineiramente perto do fim do ciclo
que “precisam entrar” com apenas uma revisão superficial, então a equipe deve
modificar seu processo para que mudanças grandes de funcionalidade aconteçam no
início do ciclo e tenham tempo suficiente para uma boa revisão.
