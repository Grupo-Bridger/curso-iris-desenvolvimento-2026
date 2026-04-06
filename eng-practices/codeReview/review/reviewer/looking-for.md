# O que procurar numa revisão de código



Observação: sempre certifique-se de levar em conta
[O Padrão da Revisão de Código](standard.md) ao considerar cada um destes
pontos.

## Design

A coisa mais importante a cobrir em uma revisão é o design geral da CL. As
interações entre várias partes do código na CL fazem sentido? Essa mudança deve
ficar na sua base de código ou em uma biblioteca? Ela se integra bem ao resto
do sistema? É um bom momento para adicionar essa funcionalidade?

## Funcionalidade

Esta CL faz o que o desenvolvedor pretendia? O que o desenvolvedor pretendia é
bom para os usuários desse código? Os “usuários” geralmente são tanto os
usuários finais (quando são afetados pela mudança) quanto os desenvolvedores
(que terão que “usar” esse código no futuro).

Em geral, esperamos que os desenvolvedores testem as CLs bem o suficiente para
que elas funcionem corretamente quando chegarem à revisão de código. Ainda
assim, como revisor, você deve continuar pensando em casos de borda, procurando
problemas de concorrência, tentando pensar como um usuário e garantindo que não
haja bugs que você consiga perceber apenas lendo o código.

Você *pode* validar a CL se quiser — o momento em que é mais importante para um
revisor verificar o comportamento de uma CL é quando ela tem impacto visível ao
usuário, como uma **mudança de UI**. É difícil entender como algumas mudanças
impactarão um usuário quando você está apenas lendo o código. Para mudanças
assim, você pode pedir para o desenvolvedor fazer uma demonstração da
funcionalidade se for inconveniente demais aplicar a CL e testar você mesmo.

Outro momento em que é particularmente importante pensar na funcionalidade
durante uma revisão de código é se há algum tipo de **programação paralela**
acontecendo na CL que poderia teoricamente causar deadlocks ou condições de
corrida. Esse tipo de problema é muito difícil de detectar apenas executando o
código e geralmente precisa que alguém (tanto o desenvolvedor quanto o revisor)
pense cuidadosamente no fluxo para ter certeza de que problemas não estão sendo
introduzidos. (Observe que isso também é um bom motivo para não usar modelos de
concorrência em que condições de corrida ou deadlocks sejam possíveis — isso
pode tornar muito complexa a revisão de código ou o entendimento do código.)

## Complexidade

A CL é mais complexa do que deveria ser? Verifique isso em todos os níveis da
CL — linhas individuais são muito complexas? Funções são muito complexas?
Classes são muito complexas? “Complexo demais” normalmente significa **“não pode
ser entendido rapidamente por quem lê o código”**. Também pode significar que
**“os desenvolvedores provavelmente introduzirão bugs quando tentarem chamar ou
modificar esse código”**.

Um tipo particular de complexidade é a **superengenharia**, em que os
 desenvolvedores tornaram o código mais genérico do que ele precisa ser, ou
adicionaram funcionalidade que ainda não é necessária para o sistema. Revisores
devem estar especialmente atentos à superengenharia. Incentive os desenvolvedores
a resolverem o problema que eles sabem que precisa ser resolvido *agora*, e não
o problema que eles especulam que *talvez* precise ser resolvido no futuro. O
problema futuro deve ser resolvido quando ele realmente aparecer e quando você
puder ver sua forma e seus requisitos reais no universo físico.

## Testes

Peça testes unitários, de integração ou de ponta a ponta conforme apropriado
para a mudança. Em geral, os testes devem ser adicionados na mesma CL que o
código de produção, a menos que a CL esteja lidando com uma
[emergência](../emergencies.md).

Certifique-se de que os testes na CL sejam corretos, sensatos e úteis. Testes
não se testam sozinhos, e raramente escrevemos testes para os nossos testes —
um humano deve garantir que os testes sejam válidos.

Os testes realmente falharão quando o código estiver quebrado? Se o código mudar
abaixo deles, eles começarão a produzir falsos positivos? Cada teste faz
assertivas simples e úteis? Os testes estão separados de forma apropriada entre
diferentes métodos de teste?

Lembre-se de que testes também são código que precisa ser mantido. Não aceite
complexidade nos testes só porque eles não fazem parte do binário principal.

## Nomenclatura

O desenvolvedor escolheu bons nomes para tudo? Um bom nome é longo o suficiente
para comunicar totalmente o que o item é ou faz, sem ser tão longo que fique
difícil de ler.

## Comentários

O desenvolvedor escreveu comentários claros em inglês compreensível? Todos os
comentários são realmente necessários? Em geral, comentários são úteis quando
**explicam por que** algum código existe, e não deveriam estar explicando **o
que** algum código está fazendo. Se o código não estiver claro o suficiente para
se explicar sozinho, então ele deveria ser simplificado. Há algumas exceções
(expressões regulares e algoritmos complexos muitas vezes se beneficiam muito de
comentários que explicam o que estão fazendo, por exemplo), mas, na maior parte
das vezes, comentários servem para informações que o próprio código não pode
conter, como o raciocínio por trás de uma decisão.

Também pode ser útil olhar os comentários que já estavam ali antes desta CL.
Talvez exista um TODO que agora pode ser removido, um comentário aconselhando
contra essa mudança sendo feita etc.

Observe que comentários são diferentes de *documentação* de classes, módulos ou
funções, que devem expressar o propósito de uma parte do código, como ela deve
ser usada e como ela se comporta quando usada.

## Estilo

Temos [guias de estilo](http://google.github.io/styleguide/) no Google para
todas as nossas principais linguagens e até para a maioria das linguagens
menores. Certifique-se de que a CL segue os guias de estilo apropriados.

Se você quiser melhorar algum ponto de estilo que não esteja no guia, prefixe
seu comentário com "Nit:" para deixar claro ao desenvolvedor que é um detalhe
e que você acha que melhoraria o código, mas não é obrigatório.
Não bloqueie CLs de serem enviadas apenas com base em preferências pessoais de
estilo.

O autor da CL não deve incluir grandes mudanças de estilo combinadas com outras
mudanças. Isso dificulta ver o que está sendo alterado na CL, torna merges e
reversões mais complexos e causa outros problemas. Por exemplo, se o autor
quiser reformatar o arquivo inteiro, peça para ele enviar apenas a reformatação
como uma CL e, depois, enviar outra CL com as mudanças funcionais.

## Consistência

E se o código existente for inconsistente com o guia de estilo? De acordo com
nossos [princípios de revisão de código](standard.md#principles), o guia de
estilo é a autoridade absoluta: se algo for exigido pelo guia de estilo, a CL
deve seguir as orientações.

Em alguns casos, o guia de estilo faz recomendações em vez de declarar
requisitos. Nesses casos, cabe julgamento se o novo código deve ser consistente
com as recomendações ou com o código ao redor. Tente seguir o guia de estilo,
a menos que a inconsistência local fique confusa demais.

Se nenhuma outra regra se aplicar, o autor deve manter consistência com o
código existente.

De qualquer forma, incentive o autor a abrir um bug e adicionar um TODO para
limpar o código existente.

## Documentação

Se uma CL mudar a forma como os usuários constroem, testam, interagem com ou
lançam o código, verifique se ela também atualiza a documentação associada,
incluindo READMEs, páginas g3doc e quaisquer documentos de referência gerados.
Se a CL apagar ou descontinuar código, considere se a documentação também deve
ser apagada.
Se a documentação estiver ausente, peça por ela.

## Cada Linha {#every-line}

No caso geral, examine *cada* linha de código que lhe foi atribuída para
revisar. Algumas coisas, como arquivos de dados, código gerado ou grandes
estruturas de dados, você pode percorrer rapidamente às vezes, mas não passe por
cima de uma classe, função ou bloco de código escritos por humanos e assuma que
o que está dentro está correto.
Obviamente, alguns códigos merecem mais escrutínio do que outros — isso é uma
decisão de julgamento —, mas você deve pelo menos ter certeza de que *entende*
o que todo o código está fazendo.

Se estiver difícil demais para você ler o código e isso estiver tornando a
revisão lenta, então você deve avisar o desenvolvedor disso e esperar que ele
esclareça antes de tentar revisar. No Google, contratamos excelentes engenheiros
de software, e você é um deles. Se você não conseguir entender o código, é
muito provável que outros desenvolvedores também não consigam. Então você
também está ajudando futuros desenvolvedores a entender esse código quando pede
que o desenvolvedor o esclareça.

Se você entender o código, mas não se sentir qualificado para revisar alguma
parte, certifique-se de que haja um revisor na CL [qualificado](#every-line-exceptions),
especialmente para questões complexas como privacidade, segurança, concorrência,
acessibilidade, internacionalização etc.

### Exceções {#every-line-exceptions}

E se não fizer sentido para você revisar cada linha? Por exemplo, você é um dos
vários revisores de uma CL e pode ser solicitado a:

*   Revisar apenas certos arquivos que fazem parte de uma mudança maior.
*   Revisar apenas certos aspectos da CL, como o design de alto nível,
    implicações de privacidade ou segurança etc.

Nesses casos, observe em um comentário quais partes você revisou. Prefira dar
[LGTM com comentários](speed.md#lgtm-with-comments).

Se você quiser, em vez disso, conceder LGTM depois de confirmar que outros
revisores examinaram outras partes da CL, registre isso explicitamente em um
comentário para alinhar expectativas. Tente [responder rapidamente](speed.md#responses)
assim que a CL atingir o estado desejado.

## Contexto

Muitas vezes é útil olhar a CL em um contexto mais amplo. Normalmente a
ferramenta de revisão de código mostrará apenas algumas linhas de código ao
redor das partes que estão sendo alteradas. Às vezes você precisa olhar o arquivo
inteiro para ter certeza de que a mudança realmente faz sentido. Por exemplo,
você pode ver apenas quatro novas linhas sendo adicionadas, mas, quando olha o
arquivo inteiro, percebe que essas quatro linhas estão em um método de 50 linhas
que agora realmente precisa ser dividido em métodos menores.

Também é útil pensar na CL no contexto do sistema como um todo. Essa CL está
melhorando a saúde do código do sistema ou está tornando o sistema inteiro mais
complexo, menos testado etc.? **Não aceite CLs que degradam a saúde do código do
sistema.** A maioria dos sistemas se torna complexa por causa de muitas pequenas
mudanças que se acumulam, então é importante evitar até pequenas complexidades
em novas mudanças.

## Coisas Boas {#good-things}

Se você vir algo bom na CL, diga ao desenvolvedor, especialmente quando ele
resolver um dos seus comentários de uma forma excelente. Revisões de código
muitas vezes se concentram apenas em erros, mas também devem oferecer incentivo
e reconhecimento por boas práticas.

## Resumo

Ao fazer uma revisão de código, você deve garantir que:

-   O código está bem projetado.
-   A funcionalidade é boa para os usuários do código.
-   Quaisquer mudanças de UI são sensatas e têm boa aparência.
-   Qualquer programação paralela é feita com segurança.
-   O código não é mais complexo do que precisa ser.
-   O desenvolvedor não está implementando coisas de que *talvez* precise no
    futuro, mas que não sabe que precisa agora.
-   O código tem testes unitários apropriados.
-   Os testes são bem projetados.
-   O desenvolvedor usou nomes claros para tudo.
-   Os comentários são claros e úteis, e explicam principalmente o **porquê**
    em vez do **quê**.
-   O código está devidamente documentado (geralmente em g3doc).
-   O código segue nossos guias de estilo.

Certifique-se de revisar **cada linha** de código que lhe foi pedido para
revisar, olhar o **contexto**, garantir que você está **melhorando a saúde do
código** e elogiar os desenvolvedores pelas **coisas boas** que eles fazem.

Próximo: [Navegando em uma CL em revisão](navigate.md)
