# O Padrão da Revisão de Código



O principal objetivo da revisão de código é garantir que a saúde geral do código
da base de código do Google esteja melhorando ao longo do tempo. Todas as
ferramentas e processos de revisão de código são projetados com esse objetivo.

Para conseguir isso, é preciso equilibrar uma série de trade-offs.

Primeiro, os desenvolvedores devem ser capazes de _progredir_ nas suas tarefas.
Se você nunca enviar uma melhoria para a base de código, então a base nunca
melhora. Além disso, se um revisor dificultar muito a entrada de _qualquer_
mudança, os desenvolvedores ficam desestimulados a fazer melhorias no futuro.

Por outro lado, é dever do revisor garantir que cada CL tenha qualidade
suficiente para que a saúde geral do código da sua base não esteja diminuindo
com o passar do tempo. Isso pode ser complicado, porque muitas vezes as bases de
código se degradam por pequenas reduções na saúde do código ao longo do tempo,
especialmente quando uma equipe está sob forte pressão de prazo e sente que
precisa adotar atalhos para cumprir seus objetivos.

Além disso, o revisor tem propriedade e responsabilidade sobre o código que está
revisando. Ele quer garantir que a base continue consistente, mantível e com
todas as outras qualidades mencionadas em
["O que procurar numa revisão de código."](looking-for.md)

Assim, chegamos à seguinte regra como o padrão que esperamos nas revisões de
código:

**Em geral, os revisores devem favorecer a aprovação de uma CL assim que ela
estiver em um estado que definitivamente melhore a saúde geral do código do
sistema que está sendo trabalhado, mesmo que a CL não seja perfeita.**

Esse é o principal princípio entre todas as diretrizes de revisão de código.

Claro que há limitações. Por exemplo, se uma CL adiciona uma funcionalidade que
o revisor não quer no seu sistema, então ele certamente pode negar a aprovação
mesmo que o código esteja bem projetado.

Um ponto-chave aqui é que não existe código “perfeito” — existe apenas código
_melhor_. Revisores não devem exigir que o autor aperfeiçoe cada pequena parte
de uma CL antes de conceder aprovação. Em vez disso, o revisor deve equilibrar
a necessidade de fazer progresso com a importância das mudanças que está
sugerindo. Em vez de buscar perfeição, o que o revisor deve buscar é
_melhoria contínua_. Uma CL que, no todo, melhora a manutenibilidade,
legibilidade e compreensibilidade do sistema não deve ser atrasada por dias ou
semanas porque não está “perfeita”.

Os revisores devem _sempre_ se sentir livres para deixar comentários dizendo que
algo poderia ser melhor, mas se isso não for muito importante, prefixe com algo
como "Nit:" para deixar claro ao autor que é apenas um ponto de polimento que
ele pode optar por ignorar.

Observação: nada neste documento justifica enviar CLs que definitivamente
_piorem_ a saúde geral do código do sistema. A única vez em que você faria isso
seria em uma [emergência](../emergencies.md).

## Mentoria

A revisão de código pode ter uma função importante de ensinar ao desenvolvedor
algo novo sobre uma linguagem, um framework ou princípios gerais de design de
software. É sempre aceitável deixar comentários que ajudem um desenvolvedor a
aprender algo novo. Compartilhar conhecimento faz parte de melhorar a saúde do
código de um sistema ao longo do tempo. Apenas lembre-se de que, se seu
comentário for puramente educacional, mas não for crítico para atender aos
padrões descritos neste documento, prefixe-o com "Nit:" ou indique de outra
forma que o autor não é obrigado a resolvê-lo nesta CL.

## Princípios {#principles}

*   Fatos técnicos e dados prevalecem sobre opiniões e preferências pessoais.

*   Em assuntos de estilo, o [guia de estilo](http://google.github.io/styleguide/)
    é a autoridade absoluta. Qualquer ponto puramente de estilo (espaçamento
    etc.) que não esteja no guia de estilo é uma questão de preferência pessoal.
    O estilo deve ser consistente com o que já existe. Se não houver estilo
    anterior, aceite o do autor.

*   **Aspectos de design de software quase nunca são uma questão pura de estilo
    ou apenas preferência pessoal.** Eles se baseiam em princípios subjacentes e
    devem ser avaliados com base nesses princípios, e não apenas por opinião.
    Às vezes existem algumas opções válidas. Se o autor puder demonstrar (seja
    por meio de dados ou com base em sólidos princípios de engenharia) que várias
    abordagens são igualmente válidas, então o revisor deve aceitar a preferência
    do autor. Caso contrário, a escolha é ditada pelos princípios padrão de
    design de software.

*   Se nenhuma outra regra se aplicar, então o revisor pode pedir ao autor que
    seja consistente com o que existe na base de código atual, desde que isso
    não piore a saúde geral do código do sistema.

## Resolvendo Conflitos {#conflicts}

Em qualquer conflito numa revisão de código, o primeiro passo deve ser sempre o
 desenvolvedor e o revisor tentarem chegar a um consenso, com base no conteúdo
deste documento e dos outros documentos em [O Guia do Autor da CL](../developer/index.md)
e deste [Guia do Revisor](index.md).

Quando chegar a um consenso se torna especialmente difícil, pode ajudar ter uma
reunião presencial ou por videochamada entre o revisor e o autor, em vez de
tentar resolver o conflito apenas por comentários na revisão de código. (Se
fizer isso, porém, certifique-se de registrar os resultados da discussão como um
comentário na CL, para leitores futuros.)

Se isso não resolver a situação, a forma mais comum de resolver seria escalar.
Muitas vezes o caminho de escalonamento é para uma discussão mais ampla da
equipe, pedir a opinião de um Tech Lead, pedir uma decisão de alguém que faça a
manutenção do código ou pedir ajuda a um Eng Manager. **Não deixe uma CL parada
porque o autor e o revisor não conseguem chegar a um acordo.**

Próximo: [O que procurar numa revisão de código](looking-for.md)
