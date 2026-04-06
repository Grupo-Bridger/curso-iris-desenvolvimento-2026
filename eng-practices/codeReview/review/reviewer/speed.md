# Velocidade das revisões de código



## Por Que As Revisões Devem Ser Rápidas? {#why}

**No Google, otimizamos para a velocidade com que uma equipe de desenvolvedores
pode produzir um produto em conjunto**, em vez de otimizar para a velocidade
com que um desenvolvedor individual escreve código. A velocidade do
desenvolvimento individual é importante; só não é *tão* importante quanto a
velocidade de toda a equipe.

Quando as revisões de código são lentas, várias coisas acontecem:

*   **A velocidade da equipe como um todo diminui.** Sim, o indivíduo que não
    responde rapidamente à revisão consegue fazer outros trabalhos. No entanto,
    novos recursos e correções de bug para o restante da equipe ficam atrasados
    por dias, semanas ou meses enquanto cada CL espera por revisão e nova
    revisão.
*   **Os desenvolvedores começam a contestar o processo de revisão de código.**
    Se um revisor só responde a cada poucos dias, mas solicita mudanças grandes
    na CL a cada vez, isso pode ser frustrante e difícil para os desenvolvedores.
    Muitas vezes isso se manifesta como reclamações sobre o quão "rigoroso" o
    revisor está sendo. Se o revisor solicita as *mesmas* mudanças substanciais
    (mudanças que realmente melhoram a saúde do código), mas responde *rápido*
    toda vez que o desenvolvedor faz uma atualização, as reclamações tendem a
    desaparecer. **A maioria das reclamações sobre o processo de revisão de
    código é, na verdade, resolvida tornando o processo mais rápido.**
*   **A saúde do código pode ser afetada.** Quando as revisões são lentas, há
    mais pressão para permitir que desenvolvedores enviem CLs que não estão tão
    boas quanto poderiam estar. Revisões lentas também desencorajam limpezas de
    código, refatorações e melhorias adicionais em CLs existentes.

## Quão Rápidas Devem Ser As Revisões? {#fast}

Se você não estiver no meio de uma tarefa focada, **deve fazer uma revisão de
 código logo após ela chegar**.

**Um dia útil é o tempo máximo que se deve levar para responder** a um pedido
de revisão de código (ou seja, responder logo na manhã seguinte).

Seguir essas diretrizes significa que uma CL típica deve passar por várias
rodadas de revisão (se necessário) dentro de um único dia.

## Velocidade vs. Interrupção {#interruption}

Há um momento em que a consideração da velocidade individual supera a velocidade
da equipe. **Se você estiver no meio de uma tarefa focada, como escrever código,
não se interrompa para fazer uma revisão de código.**
Pesquisas mostram que pode levar muito tempo para um desenvolvedor voltar a um
fluxo de desenvolvimento suave depois de ser interrompido. Então se interromper
 enquanto codifica é, na verdade, *mais* caro para a equipe do que fazer outro
desenvolvedor esperar um pouco por uma revisão de código.

Em vez disso, espere um ponto de pausa no seu trabalho antes de responder a um
pedido de revisão. Isso pode ser quando sua tarefa atual de codificação é
concluída, depois do almoço, ao voltar de uma reunião, ao retornar da sala de
descanso etc.

## Respostas Rápidas {#responses}

Quando falamos sobre velocidade das revisões de código, estamos nos referindo ao
tempo de *resposta*, e não ao tempo que leva para uma CL passar por toda a
revisão e ser enviada. O processo inteiro também deve ser rápido, idealmente,
mas **é ainda mais importante que as *respostas individuais* sejam rápidas do
que o processo inteiro acontecer rapidamente.**

Mesmo que às vezes demore muito para passar por todo o *processo* de revisão,
ter respostas rápidas do revisor ao longo do processo reduz significativamente a
frustração que os desenvolvedores podem sentir com revisões "lentas".

Se você estiver ocupado demais para fazer uma revisão completa de uma CL quando
ele chegar, ainda pode enviar uma resposta rápida informando ao desenvolvedor
quando você vai chegar a ela, sugerindo outros revisores que talvez consigam
responder mais rapidamente ou [fornecendo alguns comentários iniciais mais
amplos](navigate.md). (Observação: nada disso significa que você deva se
interromper para enviar uma resposta assim — envie a resposta em um ponto de
pausa razoável do seu trabalho.)

**É importante que os revisores dediquem tempo suficiente à revisão para terem
certeza de que seu "LGTM" significa "este código atende aos [nossos padrões](standard.md)".**
No entanto, as respostas individuais ainda devem idealmente ser [rápidas](#fast).

## Revisões Entre Fusos Horários {#tz}

Ao lidar com diferenças de fuso horário, tente responder ao autor enquanto ele
ainda tem tempo para responder antes do fim do expediente. Se ele já tiver
terminado o trabalho do dia, então tente garantir que sua revisão esteja pronta
antes de ele começar a trabalhar no dia seguinte.

## LGTM Com Comentários {#lgtm-with-comments}

Para acelerar as revisões de código, há certas situações em que um revisor deve
dar LGTM/Aprovação mesmo deixando comentários não resolvidos na CL. Isso deve
ser feito quando pelo menos uma das opções a seguir se aplicar:

*   O revisor tem certeza de que o desenvolvedor tratará adequadamente todos os
    comentários restantes do revisor.
*   Os comentários não *precisam* ser tratados pelo desenvolvedor.
*   As sugestões são pequenas, por exemplo, organizar imports, corrigir um
    typo próximo, aplicar uma correção sugerida, remover uma dependência não
    utilizada etc.

O revisor deve especificar qual dessas opções ele pretende, se isso não estiver
claro de outra forma.

LGTM com comentários vale especialmente a pena quando o desenvolvedor e o
revisor estão em fusos horários diferentes e, de outro modo, o desenvolvedor
ficaria esperando um dia inteiro só para receber "LGTM, Aprovação".

## CLs Grandes {#large}

Se alguém lhe enviar uma revisão de código tão grande que você não tem certeza
de quando terá tempo para revisá-la, sua resposta típica deve ser pedir ao
desenvolvedor que [divida a CL em várias CLs menores](../developer/small-cls.md)
que se apoiem umas nas outras, em vez de uma CL enorme que precisa ser revisada
toda de uma vez. Isso normalmente é possível e muito útil para os revisores,
mesmo que dê trabalho adicional ao desenvolvedor.

Se uma CL *não puder* ser dividida em CLs menores e você não tiver tempo para
revisar tudo rapidamente, então pelo menos escreva alguns comentários sobre o
design geral da CL e envie-a de volta para o desenvolvedor para melhoria. Um dos
seus objetivos como revisor deve ser sempre desbloquear o desenvolvedor ou
permitir que ele tome algum tipo de ação adicional rapidamente, sem sacrificar a
saúde do código para isso.

## Melhorias na Revisão de Código Com o Tempo {#time}

Se você seguir estas diretrizes e for rigoroso nas suas revisões de código,
você deve perceber que todo o processo tende a ficar cada vez mais rápido com o
tempo. Os desenvolvedores aprendem o que é necessário para um código saudável e
passam a enviar CLs excelentes desde o início, exigindo cada vez menos tempo de
revisão. Os revisores aprendem a responder rapidamente e a não adicionar
latência desnecessária ao processo de revisão.
Mas **não comprometa os [padrões de revisão de código](standard.md) nem a
qualidade por causa de uma melhora imaginada na velocidade** — isso não vai
fazer nada acontecer mais rapidamente, no longo prazo.

## Emergências

Também existem [emergências](../emergencies.md) em que as CLs precisam passar
pelo *processo inteiro* de revisão muito rapidamente, e em que as diretrizes de
qualidade seriam relaxadas. No entanto, veja [O Que É Uma Emergência?](../emergencies.md#what)
para uma descrição de quais situações realmente se qualificam como emergências
e quais não.

Próximo: [Como escrever comentários de revisão de código](comments.md)
