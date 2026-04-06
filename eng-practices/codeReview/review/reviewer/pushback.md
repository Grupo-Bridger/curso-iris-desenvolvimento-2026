# Lidando com resistência nas revisões de código



Às vezes um desenvolvedor vai resistir a um comentário de revisão de código.
Ou ele vai discordar da sua sugestão ou vai reclamar que você está sendo
exigente demais em geral.

## Quem está certo? {#who_is_right}

Quando um desenvolvedor discorda da sua sugestão, primeiro pare um momento para
considerar se ele está correto. Muitas vezes ele está mais próximo do código do
que você e pode realmente ter uma visão melhor sobre certos aspectos dele. O
argumento dele faz sentido? Faz sentido do ponto de vista da saúde do código? Se
sim, diga a ele que está certo e deixe o assunto de lado.

No entanto, desenvolvedores nem sempre estão certos. Nesse caso, o revisor deve
explicar melhor por que acredita que sua sugestão está correta. Uma boa
explicação demonstra tanto o entendimento da resposta do desenvolvedor quanto
informações adicionais sobre por que a mudança está sendo solicitada.

Em particular, quando o revisor acredita que sua sugestão vai melhorar a saúde
do código, ele deve continuar defendendo a mudança se acreditar que o aumento
de qualidade resultante justifica o trabalho adicional solicitado.
**Melhorar a saúde do código tende a acontecer em pequenos passos.**

Às vezes são necessárias algumas rodadas de explicação até que a sugestão
realmente seja absorvida. Apenas certifique-se de sempre ser [educado](comments.md#courtesy)
e deixar o desenvolvedor saber que você *entendeu* o que ele está dizendo, mas
simplesmente não *concorda*.

## Deixando os desenvolvedores chateados {#upsetting_developers}

Revisores às vezes acreditam que o desenvolvedor vai ficar chateado se o revisor
insistir em uma melhoria. Às vezes os desenvolvedores realmente ficam chateados,
mas isso normalmente é breve e eles acabam ficando muito gratos depois por você
ter ajudado a melhorar a qualidade do código. Em geral, se você for
[educado](comments.md#courtesy) nos seus comentários, os desenvolvedores na
verdade nem ficam chateados, e a preocupação está apenas na mente do revisor.
As chateações geralmente têm mais a ver com [a forma como os comentários são
escritos](comments.md#courtesy) do que com a insistência do revisor na qualidade
do código.

## Arrumar depois {#later}

Uma fonte comum de resistência é que os desenvolvedores (compreensivelmente)
querem concluir as coisas. Eles não querem passar por outra rodada de revisão só
para conseguir integrar a CL. Então dizem que vão arrumar algo em uma CL
posterior e, assim, você deve dar LGTM *nesta* CL agora. Alguns desenvolvedores
são muito bons nisso e imediatamente escrevem uma CL de acompanhamento que
corrige o problema. No entanto, a experiência mostra que, quanto mais tempo
passa depois que o desenvolvedor escreve a CL original, menor a chance de essa
arrumação realmente acontecer. Na prática, a menos que o desenvolvedor faça a
arrumação *imediatamente* após a CL atual, ela nunca acontece. Isso não ocorre
porque os desenvolvedores sejam irresponsáveis, mas porque eles têm muito
trabalho para fazer e a limpeza acaba se perdendo ou sendo esquecida em meio às
outras demandas. Portanto, normalmente é melhor insistir que o desenvolvedor
limpe a própria CL *agora*, antes que o código entre na base e esteja “pronto”.
Deixar as pessoas “arrumarem depois” é uma forma comum de as bases de código se
degenerarem.

Se uma CL introduzir nova complexidade, ela deve ser corrigida antes da
submissão, a menos que seja uma [emergência](../emergencies.md). Se a CL expuser
problemas ao redor e eles não puderem ser tratados agora, o desenvolvedor deve
abrir um bug para a limpeza e atribuí-lo a si mesmo para que não se perca. Ele
pode opcionalmente também escrever um comentário TODO no código que faça
referência ao bug aberto.

## Reclamações gerais sobre rigidez {#strictness}

Se você anteriormente tinha revisões de código bastante permissivas e passou a
ter revisões rigorosas, alguns desenvolvedores reclamarão bastante. Melhorar a
[velocidade](speed.md) das suas revisões de código geralmente faz essas
reclamações desaparecerem.

Às vezes pode levar meses para essas reclamações sumirem, mas, com o tempo, os
desenvolvedores tendem a ver o valor das revisões rigorosas à medida que percebem
quão ótimo código elas ajudam a gerar. Às vezes até os maiores protestantes se
transformam nos seus maiores apoiadores depois que algo acontece que os faz ver
realmente o valor que você agrega sendo rigoroso.

## Resolvendo Conflitos {#conflicts}

Se você estiver seguindo tudo o que foi dito acima, mas ainda assim encontrar
um conflito entre você e um desenvolvedor que não pode ser resolvido, veja
[O Padrão da Revisão de Código](standard.md) para diretrizes e princípios que
podem ajudar a resolver o conflito.
