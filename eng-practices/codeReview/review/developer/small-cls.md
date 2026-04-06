# CLs pequenas



## Por que escrever CLs pequenas? {#why}

CLs pequenas e simples são:

-   **Revisadas mais rapidamente.** É mais fácil para um revisor encontrar cinco
    minutos várias vezes para revisar CLs pequenas do que reservar um bloco de
    30 minutos para revisar uma CL grande.
-   **Revisadas com mais profundidade.** Com mudanças grandes, revisores e
    autores tendem a ficar frustrados com grandes volumes de comentários
    detalhados indo e voltando — às vezes até o ponto em que pontos importantes
    são perdidos ou deixados de lado.
-   **Menos propensas a introduzir bugs.** Como você está fazendo menos
    alterações, fica mais fácil para você e para o revisor raciocinarem de forma
    eficaz sobre o impacto da CL e verem se um bug foi introduzido.
-   **Menos trabalho desperdiçado se forem rejeitadas.** Se você escrever uma
    CL enorme e depois o revisor disser que a direção geral está errada, você
    desperdiçou muito trabalho.
-   **Mais fáceis de integrar.** Trabalhar em uma CL grande leva muito tempo,
    então você terá muitos conflitos ao integrar, e terá de integrar com mais
    frequência.
-   **Mais fáceis de projetar bem.** É muito mais fácil polir o design e a
    saúde do código de uma mudança pequena do que refinar todos os detalhes de
    uma mudança grande.
-   **Menos bloqueio por revisões.** Enviar partes autocontidas da sua mudança
    geral permite que você continue codando enquanto espera pela revisão da sua
    CL atual.
-   **Mais simples de reverter.** Uma CL grande tem maior chance de tocar em
    arquivos que serão atualizados entre o envio inicial da CL e uma CL de
    reversão, complicando a reversão (as CLs intermediárias provavelmente também
    precisarão ser revertidas).

Observe que **os revisores têm discrição para rejeitar sua mudança somente por
ela ser grande demais.** Normalmente eles agradecerão pela sua contribuição, mas
pedirão que você a transforme em uma série de mudanças menores. Pode dar muito
trabalho dividir uma mudança depois de já tê-la escrito, ou exigir muito tempo
argumentando por que o revisor deveria aceitar sua mudança grande. É mais fácil
simplesmente escrever CLs pequenas desde o começo.

## O que é pequeno? {#what-is-small}

<a id="what_is_small"></a> <!-- Keep previous permalink to avoid breaking old links. -->

Em geral, o tamanho certo para uma CL é **uma mudança autocontida**. Isso
significa que:

-   A CL faz uma mudança mínima que resolve **apenas uma coisa**. Isso normalmente
    é apenas uma parte de uma funcionalidade, e não a funcionalidade inteira de
    uma vez. Em geral, é melhor errar para o lado de escrever CLs pequenas demais
    do que CLs grandes demais. Trabalhe com o seu revisor para descobrir qual é
    um tamanho aceitável.
-   A CL deve [incluir o código de teste relacionado](#test_code).
-   Tudo o que o revisor precisa para entender a CL (exceto desenvolvimento
    futuro) está na CL, na descrição da CL, na base de código existente ou em
    uma CL que ele já revisou.
-   O sistema continuará funcionando bem para seus usuários e para os
    desenvolvedores depois que a CL for integrada.
-   A CL não é tão pequena que suas implicações fiquem difíceis de entender. Se
    você adicionar uma nova API, deve incluir um uso da API na mesma CL para que
    os revisores entendam melhor como a API será usada. Isso também evita
    integrar APIs sem uso.

Não existem regras rígidas sobre o que é grande demais. 100 linhas geralmente é
um tamanho razoável para uma CL, e 1000 linhas geralmente é grande demais, mas
isso fica a critério do seu revisor. O número de arquivos pelos quais a mudança
se espalha também afeta o seu “tamanho”. Uma mudança de 200 linhas em um único
arquivo pode ser aceitável, mas espalhada por 50 arquivos normalmente seria
grande demais.

Lembre-se de que, embora você tenha trabalhado de perto com o seu código desde o
momento em que começou a escrevê-lo, o revisor muitas vezes não tem contexto.
O que parece um tamanho aceitável de CL para você pode ser esmagador para o seu
revisor. Na dúvida, escreva CLs menores do que você acha que precisa escrever.
Revisores raramente reclamam de CLs pequenas demais.

## Quando CLs grandes são aceitáveis? {#large-okay}

<a id="large_okay"></a> <!-- Keep previous permalink to avoid breaking old links. -->

Há algumas situações em que mudanças grandes não são tão ruins:

-   Normalmente, excluir um arquivo inteiro pode ser contado como apenas uma
    linha de mudança, porque isso não leva muito tempo para o revisor analisar.
-   Às vezes uma CL grande foi gerada por uma ferramenta automática de
    refatoração em que você confia completamente, e a tarefa do revisor é apenas
    verificar e dizer que realmente quer essa mudança. Essas CLs podem ser
    maiores, embora algumas das ressalvas acima (como integração e testes)
    ainda se apliquem.

## Escrevendo CLs pequenas com eficiência {#efficiently}

Se você escreve uma CL pequena e depois espera que o revisor a aprove antes de
escrever a próxima, você vai desperdiçar muito tempo. Então você quer encontrar
alguma forma de trabalhar que não o bloqueie enquanto aguarda a revisão. Isso
pode envolver ter vários projetos para trabalhar simultaneamente, encontrar
revisores que concordem em estar imediatamente disponíveis, fazer revisões
presenciais, programação em par ou dividir suas CLs de modo que você possa
continuar trabalhando imediatamente.

## Dividindo CLs {#splitting}

Quando começar um trabalho que terá várias CLs com possíveis dependências entre
si, muitas vezes é útil pensar em como dividir e organizar essas CLs em um nível
alto antes de mergulhar na codificação.

Além de tornar as coisas mais fáceis para você como autor para gerenciar e
organizar suas CLs, isso também facilita a vida dos seus revisores de código, o
que por sua vez torna suas revisões mais eficientes.

Aqui estão algumas estratégias para dividir o trabalho em CLs diferentes.

### Empilhando várias mudanças uma sobre a outra {#stacking}

Uma forma de dividir uma CL sem se bloquear é escrever uma CL pequena, enviá-la
para revisão e então começar imediatamente a escrever outra CL *baseada* na
primeira CL. A maioria dos sistemas de controle de versão permite fazer isso de
alguma forma.

### Dividindo por arquivos {#splitting-files}

Outra forma de dividir uma CL é por agrupamentos de arquivos que exigirão
revisores diferentes, mas que, de resto, são mudanças autocontidas.

Por exemplo: você envia uma CL para modificações em um protocolo buffer e outra
CL para mudanças no código que usa esse proto. Você precisa integrar a CL do
proto antes da CL do código, mas ambas podem ser revisadas simultaneamente. Se
fizer isso, talvez queira informar aos dois grupos de revisores sobre a outra
CL que você escreveu, para que eles tenham contexto para suas mudanças.

Outro exemplo: você envia uma CL para uma mudança de código e outra para a
configuração ou experimento que usa esse código; isso também é mais fácil de
reverter, se necessário, já que arquivos de configuração/experimento às vezes
são enviados para produção mais rapidamente do que mudanças de código.

### Dividindo horizontalmente {#splitting-horizontally}

Considere criar código compartilhado ou stubs que ajudem a isolar mudanças entre
camadas da pilha de tecnologia. Isso não só ajuda a acelerar o desenvolvimento,
como também incentiva a abstração entre camadas.

Por exemplo: você criou um aplicativo de calculadora com camadas de cliente, API,
serviço e modelo de dados. Uma assinatura de proto compartilhada pode abstrair
as camadas de serviço e de modelo de dados uma da outra. Da mesma forma, um stub
de API pode separar a implementação do código do cliente do código do serviço e
permitir que ambos avancem de forma independente. Ideias semelhantes também
podem ser aplicadas a abstrações mais granulares no nível de função ou classe.

### Dividindo verticalmente {#splitting-vertically}

Em oposição à abordagem em camadas e horizontal, você pode quebrar seu código em
features verticais menores, de pilha completa. Cada uma dessas features pode ser
um fluxo de implementação paralelo independente. Isso permite que alguns fluxos
avancem enquanto outros aguardam revisão ou feedback.

Voltando ao nosso exemplo da calculadora, da seção
[Dividindo Horizontalmente](#splitting-horizontally). Agora você quer dar
suporte a novos operadores, como multiplicação e divisão. Você poderia dividir
isso implementando multiplicação e divisão como verticais ou sub-funcionalidades
separadas, mesmo que elas tenham alguma sobreposição, como estilo compartilhado
dos botões ou lógica compartilhada de validação.

### Dividindo horizontalmente e verticalmente {#splitting-grid}

Para dar um passo adiante, você pode combinar essas abordagens e montar um plano
de implementação como este, onde cada célula é sua própria CL independente.
Começando pelo modelo (na parte de baixo) e subindo até o cliente:

| Camada   | Funcionalidade: Multiplicação | Funcionalidade: Divisão        |
| ------- | ----------------------------- | ------------------------------ |
| Cliente | Adicionar botão               | Adicionar botão                |
| API     | Adicionar endpoint            | Adicionar endpoint             |
| Serviço | Implementar transformações    | Compartilhar lógica de         |
:         :                               : transformações com multiplicação:
| Modelo  | Adicionar definição de proto  | Adicionar definição de proto   |

## Separar as refatorações {#refactoring}

Em geral, é melhor fazer refatorações em uma CL separada das mudanças de
funcionalidade ou correções de bugs. Por exemplo, mover e renomear uma classe
deve estar em uma CL diferente da CL que corrige um bug nessa classe. É muito
mais fácil para os revisores entenderem as mudanças introduzidas por cada CL
quando elas estão separadas.

Pequenas limpezas, como corrigir o nome de uma variável local, podem ser
incluídas dentro de uma CL de mudança de funcionalidade ou correção de bug,
porém. Cabe ao julgamento de desenvolvedores e revisores decidir quando uma
refatoração é grande o suficiente para tornar a revisão mais difícil se for
incluída na CL atual.

## Mantenha o código de teste relacionado na mesma CL {#test-code}

<a id="test_code"></a> <!-- Keep previous permalink to avoid breaking old links. -->

CLs devem incluir o código de teste relacionado. Lembre-se de que
[pequenez](#what-is-small) aqui se refere à ideia conceitual de que a CL deve
ser focada, e não a uma função simplista baseada na contagem de linhas.

Testes são esperados para todas as mudanças do Google.

Uma CL que adiciona ou altera lógica deve ser acompanhada por testes novos ou
atualizados para o novo comportamento. CLs de refatoração pura (que não têm a
intenção de mudar comportamento) também devem ser cobertas por testes; de
preferência, esses testes já existem, mas, se não existirem, você deve adicioná-los.

Modificações de teste *independentes* podem ir para CLs separadas primeiro,
semelhante às [diretrizes de refatoração](#refactoring). Isso inclui:

*   Validar código já submetido com novos testes.
    *   Garante que a lógica importante esteja coberta por testes.
    *   Aumenta a confiança em refatorações subsequentes no código afetado. Por
        exemplo, se você quiser refatorar código que ainda não esteja coberto por
        testes, enviar CLs de teste *antes* de enviar CLs de refatoração pode
        validar que o comportamento testado continua igual antes e depois da
        refatoração.
*   Refatorar o código de teste (por exemplo, introduzir funções auxiliares).
*   Introduzir código maior de framework de testes (por exemplo, um teste de
    integração).

## Não Quebre a Build {#break}

Se você tiver várias CLs que dependem umas das outras, precisa encontrar uma
forma de garantir que o sistema inteiro continue funcionando depois que cada CL
for enviada. Caso contrário, você pode quebrar a build para todos os seus
colegas desenvolvedores por alguns minutos entre os envios das suas CLs (ou até
por mais tempo, se algo der errado inesperadamente com suas CLs posteriores).

## Não Consegue Torná-la Pequena O Suficiente {#cant}

Às vezes você encontrará situações em que parece que a sua CL *precisa* ser
grande. Isso raramente é verdade. Autores que praticam escrever CLs pequenas
quase sempre conseguem encontrar uma forma de decompor a funcionalidade em uma
série de mudanças pequenas.

Antes de escrever uma CL grande, considere se uma CL de refatoração somente,
antes dela, poderia preparar o terreno para uma implementação mais limpa. Fale
com seus colegas e veja se alguém tem ideias sobre como implementar a
funcionalidade em CLs pequenas em vez disso.

Se todas essas opções falharem (o que deve ser extremamente raro), então obtenha
antes o consentimento dos seus revisores para revisar uma CL grande, para que
ele saibam o que vem pela frente. Nessa situação, espere passar por um longo
processo de revisão, seja vigilante para não introduzir bugs e seja ainda mais
cuidadoso ao escrever testes.

Próximo: [Como lidar com comentários do revisor](handling-comments.md)
