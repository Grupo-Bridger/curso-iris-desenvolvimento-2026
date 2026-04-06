# Style Guide de ObjectScript

## Introdução

Este documento define os padrões internos para desenvolvimento de projetos em ObjectScript na empresa.

O objetivo é garantir que o código seja consistente, legível, previsível e adequado para operação em ambientes produtivos.

As regras utilizam, quando apropriado, a terminologia da RFC 2119:

- **DEVE**: requisito obrigatório  
- **NÃO DEVE**: comportamento proibido  
- **DEVERIA**: recomendação forte  
- **PODE**: opção permitida  

Este guia foi elaborado com base em boas práticas de mercado, nos Style Guides da Google e nos padrões observados nos projetos existentes da Bridger.

---

## Princípios gerais

1. O código DEVE priorizar clareza em vez de concisão.  
2. O código DEVE ser previsível do ponto de vista operacional.  
3. O código DEVE refletir claramente a responsabilidade de cada componente.  
4. O código DEVE evitar abstrações desnecessárias ou genéricas quando o contexto for específico.  
5. O código DEVERIA manter consistência de idioma dentro de um mesmo contexto.  

---

## Convenções de nomenclatura

### Pacotes e diretórios

- Pacotes DEVEM utilizar `camelCase`.
- Cada pacote (pasta raiz) DEVERIA representar um sistema ou domínio.
- Os diretórios imediatamente abaixo do pacote DEVERIAM representar divisões de responsabilidades ou objetos específicos do domínio.
- O caminho DEVE permitir identificar rapidamente a responsabilidade da classe.
- Abreviações NÃO DEVEM ser usadas sem clareza.

---

### Classes

- Classes DEVEM utilizar `PascalCase`.
- O nome da classe DEVE refletir claramente sua responsabilidade.
- O nome das classes de Interoperabilidade DEVERIAM ser o tipo da classe:
  - `Process`: Classes que extendem de Ens.BusinessProcess
  - `Operation`: Classes que extendem de Ens.BusinessOperation
  - `Service`: Classes que extendem de Ens.BusinessService

---

### Métodos

- Métodos DEVEM utilizar `PascalCase`.
- Métodos DEVEM ter nomes verbais e descritivos.
- Nomes genéricos (ex: `Execute`, `Handle`, ‘OnRequest’) DEVEM ser utilizados quando a responsabilidade da classe é realizar somente uma ação específica.
- Parâmetros DEVEM utilizar o prefixo “p” seguido da descrição do mesmo em PascalCase (ex. pRequest, pInitialDate).

---

### Propriedades

- Propriedades DEVEM utilizar `PascalCase`.  
- Nomes DEVEM ser claros e representar corretamente seu propósito.  
- Configurações DEVERIAM ser expostas via parâmetros apropriados da plataforma.  

---

### Variáveis locais

- Variáveis DEVEM ser curtas, porém descritivas.  
- Abreviações não evidentes DEVEM ser evitadas.  
- Uso de `#Dim` DEVERIA ser adotado quando aumentar a clareza.  
- Em caso de inconsistência de padrão, utilizar `[PREENCHA AQUI]`.  

---

## Estrutura de classes e métodos

### Business Process

- DEVE orquestrar o fluxo.
- DEVE delegar responsabilidades para outras camadas.
- DEVE tratar erros e retornar status apropriado.
- NÃO DEVE comunicar com sistemas externos.
- NÃO DEVERIA receber e retornar dados não estruturados

---

### Request e Response

- DEVEM representar contratos de entrada e saída.  
- NÃO DEVEM conter lógica de negócio.  
- DEVEM ser simples e objetivos.  

---

### Business Operation

- DEVE encapsular integrações externas.
- DEVE centralizar configurações técnicas (host, porta, SSL, etc).
- NÃO DEVE conter transformação de dados complexa.
- NÃO DEVE tomar decisões de negócio.

---

### Business Service

- DEVE ser responsável por entrada ou aquisição de dados.
- DEVE iniciar fluxos de processamento.
- NÃO DEVE tomar decisões de negócio.

---

### Data Transform

- DEVE realizar apenas transformação de dados.
- NÃO DEVE executar integração ou persistência.
- DEVE manter conversões explícitas e previsíveis.

---

### Persistência

- Classes DEVEM representar estado durável.
- Métodos DEVEM ser simples e objetivos.
- Operações de escrita DEVEM ser explícitas.

---

## Formatação de código

- A indentação DEVE ser feita utilizando tabs.
- Linhas muito longas DEVERIAM ser evitadas.
- Comentários DEVEM explicar o “porquê”, não o “o quê”.
- Refatorações puramente estéticas NÃO DEVEM ser feitas sem justificativa.

---

### Chaves

O uso de chaves deve seguir o padrão `Allman`.
Ex.

```objectscript
If (idade >= 18)
{
    Write “Maior de idade”, !
}
Else
{
    Write “Menor de idade”, !
}
```

---

### Linter

- Deve ser utilizado o linter padrão da Intersystems no VsCode (intersystems.language-server)

O linter deve estar configurado conforme JSON abaixo:

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

Caso não seja possível o uso do linter, os padrões abaixo devem ser seguidos manualmente:

- Comandos DEVEM estar no seu formato não abreviado (`Set` e não `S`).
- Comandos DEVEM estar em PascalCase (`Set` e não `set` ou `SET`).
- Nomes de classe DEVEM estar em sua versão mais estendida, sem abreviações (%Library.String ao invés de %String)
- Funções de sistema DEVEM estar em UPPERCASE ($PIECE e não $Piece ou $piece)
- Funções de sistema DEVEM estar no seu formato não abreviado.($PIECE e não $P, $LENGTH e não $L)

---

## Tratamento de erros

- NÃO DEVE ser reutilizada ou re-atribuída uma mesma variável de status no mesmo método.
- Métodos a serem convocados via Production DEVEM retornar `%Library.Status` (`OnProcessInput` dos BusinessServices, `OnRequest` dos BusinessProcesses e métodos do BusinessOperation).
- Métodos públicos DEVEM conter um Try Catch para realizar a tratativa dos erros antes de fazer qualquer retorno.
- Métodos privados DEVERIAM não retornar %Library.Status e sim uma exception, para mais fácil tratativa no Try Catch do método público que o chama.
- DEVERIA ser utilizada a `%Exception.General` sempre que possível, para gerar erros customizados.

---

## Logging e observabilidade

- Logs DEVEM ser claros e úteis para operação.
- Logs NÃO DEVEM expor dados sensíveis.
- Logs PODEM ser opcionais através de um parâmetro num método, ou uma propriedade na classe para configuração na Production.

---

## Testes

- Projetos DEVERIAM possuir testes automatizados.
- PODEM ser criados testes automatizados com objetivo de validar se sistemas externos estão no ar e respondendo como esperado.
- Data Transformations DEVERIAM ter testes automatizados simulando um JSON/Objeto de entrada e os valores esperados no objeto de saída.
- Business Operations PODEM ter lógica de “mock”, retornando um valor fixo ao invés de comunicar com o sistema externo.
- Mocks DEVEM ser claramente identificados.

---

