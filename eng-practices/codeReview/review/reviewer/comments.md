# Como escrever comentários de revisão de código



## Resumo

-   Seja gentil.
-   Explique seu raciocínio.
-   Equilibre dar instruções explícitas com apenas apontar problemas e deixar o
    desenvolvedor decidir.
-   Incentive desenvolvedores a simplificar o código ou adicionar comentários ao
    código em vez de apenas explicar a complexidade para você.

## Cortesia

Em geral, é importante ser
[cortês e respeitoso](https://chromium.googlesource.com/chromium/src/+/master/docs/cr_respect.md)
enquanto também se é muito claro e útil para o desenvolvedor cujo código você
está revisando. Uma forma de fazer isso é garantir que você sempre faça
comentários sobre o *código* e nunca sobre o *desenvolvedor*. Você nem sempre
precisa seguir essa prática, mas definitivamente deve usá-la quando estiver
falando algo que poderia ser perturbador ou controverso. Por exemplo:

Ruim: "Por que **você** usou threads aqui quando claramente não há benefício a
obter com concorrência?"

Bom: "O modelo de concorrência aqui está adicionando complexidade ao sistema
sem nenhum benefício real de desempenho que eu consiga ver. Como não há
benefício de desempenho, é melhor que esse código seja de uma única thread em
vez de usar múltiplas threads."

## Explique O Porquê {#why}

Uma coisa que você perceberá no exemplo “bom” acima é que ele ajuda o
desenvolvedor a entender *por que* você está fazendo seu comentário. Você nem
sempre precisa incluir essa informação nos seus comentários de revisão, mas às
vezes é apropriado fornecer um pouco mais de explicação sobre sua intenção, a
melhor prática que você está seguindo ou como sua sugestão melhora a saúde do
código.

## Dando Orientação {#guidance}

**Em geral, é responsabilidade do desenvolvedor corrigir uma CL, não do
revisor.** Você não é obrigado a fazer o detalhamento do design de uma solução
ou escrever código para o desenvolvedor.

Isso não significa que o revisor deva ser inútil, porém. Em geral você deve
buscar o equilíbrio apropriado entre apontar problemas e fornecer orientação
direta. Apontar problemas e deixar o desenvolvedor tomar uma decisão muitas
vezes ajuda o desenvolvedor a aprender e facilita fazer revisões de código.
Também pode resultar em uma solução melhor, porque o desenvolvedor está mais
próximo do código do que o revisor.

No entanto, às vezes instruções diretas, sugestões ou até mesmo código são mais
úteis. O objetivo principal da revisão de código é obter a melhor CL possível.
Um objetivo secundário é melhorar as habilidades dos desenvolvedores para que,
com o tempo, eles precisem de cada vez menos revisão.

Lembre-se de que as pessoas aprendem tanto com o reforço do que estão fazendo
bem quanto com o que poderiam fazer melhor. Se você vir coisas de que gosta na
CL, comente sobre elas também! Exemplos: o desenvolvedor limpou um algoritmo
bagunçado, adicionou uma cobertura exemplar de testes, ou você, como revisor,
aprendeu algo com a CL. Assim como em todos os comentários, inclua o [por quê](#why)
do que você gostou, incentivando ainda mais o desenvolvedor a continuar com
boas práticas.

## Rotule a severidade dos comentários {#label-comment-severity}

Considere rotular a severidade dos seus comentários, diferenciando mudanças
obrigatórias de orientações ou sugestões.

Aqui estão alguns exemplos:

> Nit: Este é um detalhe menor. Tecnicamente você deveria fazer isso, mas isso
> não vai impactar muito as coisas.
>
> Opcional (ou Considere): Acho que isso pode ser uma boa ideia, mas não é
> estritamente obrigatório.
>
> FYI: Não espero que você faça isso nesta CL, mas talvez seja interessante
> pensar nisso para o futuro.

Isso torna a intenção da revisão explícita e ajuda os autores a priorizarem a
importância de vários comentários. Também ajuda a evitar mal-entendidos; por
exemplo, sem rótulos nos comentários, os autores podem interpretar todos os
comentários como obrigatórios, mesmo quando alguns são apenas informativos ou
opcionais.

## Aceitando Explicações {#explanations}

Se você pedir para um desenvolvedor explicar uma parte do código que você não
entende, isso geralmente deve resultar em ele **reescrever o código de forma
mais clara**. Ocasionalmente, adicionar um comentário no código também é uma
resposta apropriada, desde que não seja apenas uma explicação de um código
excessivamente complexo.

**Explicações escritas somente na ferramenta de revisão de código não ajudam
leitores futuros do código.** Elas são aceitáveis apenas em poucas situações,
como quando você está revisando uma área com a qual não está muito familiarizado
e o desenvolvedor explicou algo que leitores normais do código já saberiam.

Próximo: [Como lidar com resistência nas revisões de código](pushback.md)
