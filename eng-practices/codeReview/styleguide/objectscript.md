# Style Guide de ObjectScript

## Introdução

Este documento define os padrões internos para desenvolvimento de projetos em ObjectScript na empresa.

O objetivo é garantir que o código seja consistente, legível, previsível e adequado para operação em ambientes produtivos.

As regras utilizam, quando apropriado, a terminologia da RFC 2119:

- **PRECISA**: requisito obrigatório
- **NÃO PODE**: comportamento proibido
- **DEVE**: recomendação forte
- **NÃO DEVE**: recomendação forte contra
- **PODE**: opção permitida  

Este guia foi elaborado com base em boas práticas de mercado, nos Style Guides da Google e nos padrões observados nos projetos existentes da Bridger.

---

## Princípios gerais

1. O código PRECISA priorizar clareza em vez de concisão.  
2. O código PRECISA ser previsível do ponto de vista operacional.  
3. O código PRECISA refletir claramente a responsabilidade de cada componente.  
4. O código PRECISA evitar abstrações desnecessárias ou genéricas quando o contexto for específico.  
5. O código DEVE manter consistência de idioma dentro de um mesmo contexto.

---

## Convenções de nomenclatura

### Pacotes e diretórios

- Pacotes PRECISAM utilizar `camelCase`.
- NÃO DEVEM ser utilizadas abreviações.
- Cada pacote (pasta raiz) DEVE representar um sistema ou domínio.
- Os diretórios imediatamente abaixo do pacote DEVERIAM representar divisões de responsabilidades ou objetos específicos do domínio.
- O caminho PRECISA permitir identificar rapidamente a responsabilidade da classe.
- Abreviações NÃO PRECISAM ser usadas sem clareza.

Ex.:

```plaintext
src/
├── sapDominio/
│   ├── departamento/
│   │   │── pedidoVenda/
│   │   │   │── criacao/
│   │   │   │   │── model/
│   │   │   │   └── rest/
│   │   │   │── exclusao/
│   │   │   │   │── model/
│   │   │   │   └── rest/
│   ├── pedidoCompra/
│   │   │── model/
│   │   └── rest/
│   ├── notaFiscalEntrada/
│   │   │── model/
│   │   └── rest/
│   ├── notaFiscalSaida/
│   │   │── model/
│   │   └── rest/
├── sapResponsabilidade/
│   ├── model/
│   │   │── pedidoCompra/
│   │   │── notaFiscalEntrada/
│   │   │── notaFiscalSaida/
│   │   └── pedidoVenda/
│   ├── rest/
│   │   │── pedidoCompra/
│   │   │── notaFiscalEntrada/
│   │   │── notaFiscalSaida/
│   │   └── pedidoVenda/
```

---

### Classes

- Classes PRECISAM utilizar `PascalCase`.
- O nome da classe PRECISA refletir claramente sua responsabilidade.
- NÃO DEVEM ser utilizadas abreviações.
- O nome das classes de Interoperabilidade DEVERIAM ser o tipo da classe:
  - `Service`: Classes que extendem de Ens.BusinessService
  - `Process`: Classes que extendem de Ens.BusinessProcess
  - `Operation`: Classes que extendem de Ens.BusinessOperation

---

### Métodos

- Métodos PRECISAM utilizar `PascalCase`.
- NÃO DEVEM ser utilizadas abreviações.
- Métodos PRECISAM ter nomes verbais e descritivos.
- Nomes genéricos (ex: `Execute`, `Handle`, `OnRequest`) PRECISAM ser utilizados quando a responsabilidade da classe é realizar somente uma ação específica.
- Parâmetros PRECISAM utilizar `camelCase` (ex. request, initialDate).

---

### Propriedades

- Propriedades PRECISAM utilizar `PascalCase`.  
- NÃO DEVEM ser utilizadas abreviações.
- Nomes PRECISAM ser claros e representar corretamente seu propósito.  
- Configurações DEVERIAM ser expostas via parâmetros apropriados da plataforma.  

---

### Parâmetros (de classe)

- Parâmetros PRECISAM utilizar `UPPERCASE`.
- NÃO DEVEM ser utilizadas abreviações.
- Nomes PRECISAM ser claros e representar corretamente seu propósito.

---

### Variáveis locais

- Nomes PRECISAM ser claros e representar corretamente seu propósito.
- Abreviações PODEM ser utilizadas para não perder contexto de variáveis com nomes extensos
- Abreviações não evidentes PRECISAM ser evitadas.
- Uso de `#Dim` DEVE ser adotado quando aumentar a clareza.
- Em caso de inconsistência de padrão, utilizar `[PREENCHA AQUI]`.

```objectscript
// contexto
Set medianaAnaliseDadosPedidosVendaHistorico = "não funciona pelo número de caracteres"

// aceitáveis
Set medianaAnaliseDadosPevHistorico = "ideal"
Set medianaAnaliDadPevHistorico = "aceitável"

// inaceitável
Set medianaAnaliDadPevHist = "excessivamente abreviado"
Set medianaAnaliseDadosPedidosVenda = "perdeu contexto do histórico"
Set medianaAnaliseDados = "perdeu contexto do pedido de venda"
Set medianaPedidoHistorico = "perdeu contexto da análise de dados"
```

---

## Estrutura de classes e métodos

### Business Process

- PRECISA orquestrar o fluxo.
- PRECISA delegar responsabilidades para outras camadas.
- PRECISA tratar erros e retornar status apropriado.
- NÃO PODE comunicar com sistemas externos.
- NÃO DEVE receber e retornar dados não estruturados

---

### Request e Response

- PRECISAM representar contratos de entrada e saída.  
- NÃO PRECISAM conter lógica de negócio.  
- PRECISAM ser simples e objetivos.  

---

### Business Operation

- PRECISA encapsular integrações externas.
- PRECISA centralizar configurações técnicas (host, porta, SSL, etc).
- NÃO PODE conter transformação de dados complexa.
- NÃO PODE tomar decisões de negócio.

---

### Business Service

- PRECISA ser responsável por entrada ou aquisição de dados.
- DEVE iniciar fluxos de processamento.
- NÃO PODE tomar decisões de negócio.

---

### Data Transform

- PRECISA realizar apenas transformação de dados.
- NÃO PODE executar integração ou persistência.
- PRECISA manter conversões explícitas e previsíveis.

---

### Persistência

- Classes PRECISAM representar estado durável.
- Métodos PRECISAM ser simples e objetivos.
- Operações de escrita PRECISAM ser explícitas.

---

## Formatação de código

- A indentação PRECISA ser feita utilizando tabs.
- Linhas muito longas DEVERIAM ser evitadas (evitar passar da coluna 80).
- Comentários PRECISAM explicar o “porquê”, não o “o quê”.

---

### Chaves

O uso de chaves PRECISA seguir o padrão `K&R`.
Ex.

```objectscript
If (idade >= 18) {
    Write “Maior de idade”, !
} Else {
    Write “Menor de idade”, !
}
```

---

### Linter

- PRECISA ser utilizado o linter padrão da Intersystems no VsCode (intersystems.language-server)

O linter PRECISA estar configurado conforme JSON abaixo:

```json
{
    // Intersystem auto-formatter
    "intersystems.language-server.formatting.commands.case": "word",
    "intersystems.language-server.formatting.commands.length": "long",
    "intersystems.language-server.formatting.expandClassNames": true,
    "intersystems.language-server.formatting.system.case": "upper",
    "intersystems.language-server.formatting.system.length": "long",
}
```

Caso não seja possível o uso do linter, os padrões abaixo PRECISAM ser seguidos manualmente:

- Comandos PRECISAM estar no seu formato não abreviado (`Set` e não `S`).
- Comandos PRECISAM estar em PascalCase (`Set` e não `set` ou `SET`).
- Nomes de classe PRECISAM estar em sua versão mais estendida, sem abreviações (`%Library.String` ao invés de `%String`)
- Funções de sistema PRECISAM estar em UPPERCASE ($PIECE e não $Piece ou $piece)
- Funções de sistema PRECISAM estar no seu formato não abreviado.($PIECE e não $P, $LENGTH e não $L)

```plaintext
....model/
    ├── Pedido/
    ├── Cliente/
    ├── Fornecedor/
    ├── auxiliares/
        ├── Endereco/
```

```
Class xpto.model.Pedido

Property Id As %Library.Integer

Property Cliente As xpto.model.Cliente

Property Endereco As ?
```

---

## Tratamento de erros

- NÃO PODE ser reutilizada ou re-atribuída uma mesma variável de status no mesmo método.
- Os erros PRECISAM ser validados e retornados rápidamente, evitando validações de sucesso que englobam o restante do código.
- Métodos a serem convocados via Production PRECISAM retornar `%Library.Status` (`OnProcessInput` dos BusinessServices, `OnRequest` dos BusinessProcesses e métodos do BusinessOperation).
- Métodos públicos PRECISAM conter um Try Catch para realizar a tratativa dos erros antes de fazer qualquer retorno.
- Métodos privados DEVERIAM não retornar `%Library.Status` e sim uma exception, para mais fácil tratativa no Try Catch do método público que o chama.
- DEVE ser utilizada a `%Exception.General` sempre que possível, para gerar erros customizados.

```objectscript
// correto
If (erro = true)
{
    Throw erro
}

// errado
If (erro = false)
{
    // continua o código
}
Else
{
    Throw erro
}

// errado, else desnecessário
If (erro = true)
{
    Throw error
}
Else
{
    // continua o código
}
```

---

## Logging e observabilidade

- Logs PRECISAM ser claros e úteis para operação.
- Logs NÃO PODEM expor dados sensíveis.
- Logs PODEM ser opcionais através de um parâmetro num método, ou uma propriedade na classe para configuração na Production.

---

## Testes

- Projetos DEVERIAM possuir testes automatizados.
- PODEM ser criados testes automatizados com objetivo de validar se sistemas externos estão no ar e respondendo como esperado.
- Data Transformations DEVERIAM ter testes automatizados simulando um JSON/Objeto de entrada e os valores esperados no objeto de saída.
- Business Operations PODEM ter lógica de “mock”, retornando um valor fixo ao invés de comunicar com o sistema externo.
- Mocks PRECISAM ser claramente identificados.

---

## Boas práticas gerais

1. Variáveis NÃO DEVERIAM ser reatribuídas.
2. O código NÃO DEVERIA ter mais que 3 níveis de indentação.
