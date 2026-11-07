---
name: emitir-nfe-bling
description: Emite NF-e de saída no Bling a partir dos pedidos de venda vindos da Shopify, sob demanda e com confirmação. Use quando eu pedir para emitir, gerar ou autorizar notas fiscais de saída / NF-e dos pedidos no Bling.
user-invokable: true
risk: high
---

# Emitir NF-e de saída no Bling

Requer o conector **Bling MCP** ativo na sessão. Se as ferramentas do Bling não
estiverem disponíveis, avise que é preciso conectar em
https://claude.ai/customize/connectors e abrir uma sessão nova. Não simule a emissão.

## Fluxo (sempre sob demanda)
1. Listar os pedidos de venda do Bling que ainda não têm nota (as vendas vêm da Shopify).
2. Mostrar a lista (nº do pedido, cliente, valor, itens e o NCM que será aplicado em cada item)
   e **aguardar minha confirmação** antes de emitir qualquer nota.
3. Para cada pedido aprovado: gerar a NF-e a partir do pedido, aplicar as regras abaixo
   e enviar para autorização na SEFAZ.
4. Resumir no final: notas autorizadas (número e chave de acesso) e rejeitadas (com o motivo
   da SEFAZ). Não reenviar uma nota rejeitada sem me consultar.

## Cabeçalho (de "Tipo de saída" até "Itens da nota fiscal")
- Não alterar nada. Manter exatamente como veio do pedido.

## Itens da nota
- Editar **somente o NCM** de cada item, conforme a tabela abaixo.
- Não alterar nenhum outro campo do item. O que estiver vazio continua vazio.
- Regra: sempre a categoria do produto, **masculina, de algodão**.

| Produto (identificado pelo nome) | NCM |
|---|---|
| Camisa (tecido plano: social, botão, manga curta/longa) | 6205.20.00 |
| Camisa polo | 6105.10.00 |
| Camiseta / T-shirt / regata | 6109.10.00 |
| Calça / bermuda / short | 6203.42.00 |
| Moletom / blusa de malha / suéter | 6110.20.00 |
| Jaqueta / casaco | 6201.30.00 |
| Cueca | 6107.11.00 |
| Meia | 6115.95.00 |

Obs.: "camisa" nesta loja é sempre de tecido plano (6205.20.00).
Se o nome do produto não se encaixar claramente em nenhuma linha, **não emitir aquela nota**:
listar o produto e perguntar qual NCM usar.

## Demais campos da nota
- **Cálculo automático de impostos:** ligado.
- **Categoria:** Venda de mercadorias.
- **Condição de pagamento:** cartão de crédito, boleto ou pix (conforme o pedido), sempre com condição **0**.
- **Transportador/volumes:** não haverá transporte.
- **Frete por conta:** contratação do frete por conta do remetente.
- **Dados da transportadora:** não preencher nada.
- **Dados do volume:** não preencher nada.
- **Intermediador:** Não.
- **Pessoas autorizadas a acessar o XML:** EDC Contabilidade (já cadastrada como contato no Bling).
- **Informações adicionais:** copiar exatamente como aparecem no pedido de venda
  (nº do pedido na loja virtual, canal de venda "Outros", loja virtual "Shopify").
  O número muda a cada pedido.
