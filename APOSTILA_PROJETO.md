# Projeto de desenvolvimento com Intersystems Interoperability

## Enunciado

Você vai desenvolver um **fluxo periódico** que busca **pedidos** novos em um banco de dados externo via **JDBC**, e envia estes pedidos para uma **API REST**.

## Definições

### A tabela JDBC a ser buscada terá as colunas seguintes:

- id
- id_produto
- nome_produto
- quant_produto
- preco_produto
- id_cliente
- nome_cliente
- cpf_cliente
- rua_entrega
- numero_entrega
- bairro_entrega
- uf_entrega
- data_criacao

### O JSON de pedido esperado pela API terá o formato seguinte

```json
{
    "id": "",
    "total": 0,
    "product": {
        "id": "",
        "name": "",
        "quantity": 0,
        "price": 0,
    },
    "customer": {
        "key": "",
        "name": "",
    },
    "delivery": {
        "street": "",
        "number": "",
        "neighborhood": "",
        "state": "",
        "zipCode": "*",
    }
}
```

> *Opcional, dependendo do tempo de desenvolvimento do projeto

### Conceitos chave

- Inbound Adapter
- Outbound Adapter
- Tabelas de Lookup
- Credenciais

