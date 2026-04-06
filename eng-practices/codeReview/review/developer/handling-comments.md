# Como lidar com comentários do revisor



Quando você envia uma CL para revisão, é provável que o revisor responda com
vários comentários sobre a sua CL. Aqui estão algumas coisas úteis para saber
sobre como lidar com comentários do revisor.

## Não Leve Para O Lado Pessoal {#personal}

O objetivo da revisão é manter a qualidade da nossa base de código e dos nossos
produtos. Quando um revisor critica o seu código, pense nisso como uma tentativa
de ajudar você, a base de código e o Google, e não como um ataque pessoal a
você ou às suas capacidades.

Às vezes os revisores se sentem frustrados e expressam essa frustração nos seus
comentários. Isso não é uma boa prática para revisores, mas, como desenvolvedor,
você deve estar preparado para isso. Pergunte a si mesmo: "O que é construtivo
que o revisor está tentando me comunicar?" e então aja como se fosse isso que
ele realmente disse.

**Nunca responda com raiva a comentários de revisão de código.** Isso é uma
violação séria da etiqueta profissional que ficará para sempre na ferramenta de
revisão de código. Se você estiver com raiva ou irritado demais para responder
com gentileza, então afaste-se do computador por um tempo ou trabalhe em outra
coisa até se acalmar o suficiente para responder educadamente.

Em geral, se um revisor não estiver fornecendo feedback de forma construtiva e
educada, explique isso a ele pessoalmente. Se você não puder conversar com ele
pessoalmente ou por videochamada, então envie um e-mail privado. Explique de
maneira gentil o que você não gostou e o que gostaria que ele fizesse de forma
diferente. Se ele também responder de forma não construtiva a essa conversa
privada, ou se isso não tiver o efeito pretendido, então
escalone para o seu gerente, conforme apropriado.

## Corrija o Código {#code}

Se um revisor disser que não entende algo no seu código, sua primeira resposta
deve ser esclarecer o próprio código. Se o código não puder ser esclarecido,
adicione um comentário no código que explique por que aquilo está ali. Se um
comentário parecer inútil, só então sua resposta deve ser uma explicação na
ferramenta de revisão de código.

Se um revisor não entendeu alguma parte do seu código, é provável que outros
leitores futuros também não entendam. Escrever uma resposta na ferramenta de
revisão de código não ajuda leitores futuros, mas esclarecer seu código ou
adicionar comentários ajuda.

## Pense de Forma Colaborativa {#think}

Escrever uma CL pode dar muito trabalho. Muitas vezes é muito satisfatório
finalmente enviá-la para revisão, sentir que terminou e ter quase certeza de que
não é preciso mais trabalho. Pode ser frustrante receber comentários pedindo
mudanças, especialmente se você não concorda com eles.

Nesses momentos, pare por um instante e considere se o revisor está fornecendo
feedback valioso que ajudará a base de código e o Google. Sua primeira pergunta
para si mesmo deve ser sempre: "Eu entendi o que o revisor está pedindo?"

Se você não puder responder a essa pergunta, peça esclarecimentos ao revisor.

E então, se você entender os comentários, mas discordar deles, é importante
pensar de forma colaborativa, e não combativa ou defensiva:

```txt {.bad}
Ruim: "Não, eu não vou fazer isso."
```

```txt {.good}
Bom: "Escolhi X por causa de [estes prós/contras] e de [estes trade-offs]
Minha compreensão é que usar Y seria pior por [estas razões].
Você está sugerindo que Y atende melhor aos trade-offs originais, que devemos
pesar os trade-offs de forma diferente, ou outra coisa?"
```

Lembre-se de que
**[cortesia e respeito](https://chromium.googlesource.com/chromium/src/+/master/docs/cr_respect.md)**
deve sempre ser prioridade máxima. Se você discordar do revisor, encontre formas
de colaborar: peça esclarecimentos, discuta prós e contras e explique por que
seu método é melhor para a base de código, para os usuários e/ou para o Google.

Às vezes, você pode saber algo sobre os usuários, a base de código ou a CL que
o revisor não sabe. [Corrija o código](#code) quando apropriado e envolva o
revisor na discussão, inclusive oferecendo mais contexto. Normalmente é possível
chegar a um consenso entre você e o revisor com base em fatos técnicos.

## Resolvendo Conflitos {#conflicts}

Seu primeiro passo para resolver conflitos deve ser sempre tentar chegar a um
consenso com o revisor. Se você não conseguir chegar a um consenso, veja
[O Padrão da Revisão de Código](../reviewer/standard.md), que traz princípios a
seguir nessa situação.
