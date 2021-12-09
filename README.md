# Desafio de Analytics Engineer
## Considerações sobre o desafio
* O prazo padrão para entrega da solução é de 7 dias corridos, contados a partir da data de recebimento do desafio. Caso você precise de mais tempo, entre em contato conosco e fechamos uma nova data para a entrega. Não se preocupe, somos super flexíveis ;)
- Não se preocupe em responder todos os pontos do desafio. Queremos ver até que ponto você consegue se aprofundar :)
 
## Case Study
### Contexto Geral
Nós, da empresa **Tupi Livre**, somos um marketplace, ou seja, temos como objetivo conectar consumidores e vendedores em todo território Tupiniquins. Atualmente na nossa plataforma possui desde itens eletrônicos, esporte e lazer até ferramentas de jardinagem. Nos últimos 3 meses a empresa vem crescendo exponencialmente a uma taxa maior do que 150% ao mês e com isso existem diversos projetos e iniciativas nascendo por toda a companhia.

E você é o novo integrante do time de Dados da empresa e como primeiro desafio foi convocado pelo líder do time de Analytics para ajudar a coletar dados da empresa para a construção de importantes tabelas para suportar os relatórios solicitados pelos times internos.

##### Data Stack

Na **Tupi Livre** organizamos a nossa [estrutura de dados](https://www.trifacta.com/blog/data-stack/) seguindo o conceito de [Modern Data Stack](https://towardsdatascience.com/the-building-blocks-of-a-modern-data-platform-92e46061165) e nesse [link](https://towardsdatascience.com/the-beginners-guide-to-the-modern-data-stack-d1c54bd1793e) você consegue mais informações sobre. Desse modo separamos o nosso pipeline em basicamente em duas etapas:

* **Ingestão**
Nessa etapa garantimos que todas as fontes de dados estão sendo inseridas no nosso Banco de Dados (BigQuery) no formato Raw Data, ou seja, no formato mais cru possível sem nenhuma transformação. Nessa camada os dados podem estar duplicados, não formatados e até desorganizados. 

* **Transformação**
Já nessa etapa ocorre as transformações, ou seja, agrupamentos, aplicações de regras de negócio e normatizações. Desse modo, conseguimos obter dados documentados, curados e prontos para os times de negócio utilizá-los com maior facilidade e segurança em suas análises/decisões de negócio. 

Com isso em mente, construimos a nossa estrutura, segue o desenho: ![Data Stack](https://assets.dataform.co/updated-landing/datastack_horizontal.png)

### Desafio

##### Projeto: Placar do Cliente
Com o crescimento exponencial da nossa empresa, o time de CRM, responsável pelas comunicações de relação com o cliente, resolveu realizar um estudo para entender melhor cada cliente na nossa plataforma e assim conseguir se posicionar melhor nas nossas comunicações. Para isso o time de CRM solicitou as seguinte tabelas a serem construídas pelo time de dados:

##### *customer_metrics*
   - **customer_id**Esse é o id do customer da tabela customers, usamos para identificar cada usuário.
   - **customer_city**: Cidade do nosso cliente.
   - **customer_state**: Estado do nosso cliente.
   - **recency**: Recência é definida da diferença de dias da última compra do cliente com a data atual. Ex: Hoje é dia 2021-12-10 e o cliente fez o seu último pedido no dia 2021-12-01, portanto recência é 9 (dias). 
   - **frequency**: Frequência é definida como a quantidade total de pedidos entregues do cliente.
   - **monetary_value**: Monetary Value é definido como a soma total do preço e frete de todos os pedidos entregues do cliente.
   - **qty_items_delivered**: Soma total de todos os itens que foram entregues ao cliente. 
   - **basket_size**: Divisão entre  qty_items_delivered/frequency, como resultado é quantidade média de itens por pedido.
   - **avg_reviews_score**: É a média dos review score de cada cliente.

##### *customer_cohort*
   - **month**: Esse é o mês do primeiro pedido entregue do cliente.
   - **M0**: Esse valor sempre vai ser 100%.
   - **M1**: Percentual de clientes que realizaram mais um pedido no mês seguinte (M+1) comparado com M0.
   - **M2**:  Percentual de clientes que realizaram mais um pedido a 2 meses após a primeira compra (M+2).
   - **M3**:  Percentual de clientes que realizaram mais um pedido a 3 meses após a primeira compra (M+3).
   - **M4**:  Percentual de clientes que realizaram mais um pedido a 4 meses após a primeira compra (M+4).
   - **M5**:  Percentual de clientes que realizaram mais um pedido a 5 meses após a primeira compra (M+5).
   - **M6**:  Percentual de clientes que realizaram mais um pedido a 6 meses após a primeira compra (M+6).
   - **M7**:  Percentual de clientes que realizaram mais um pedido a 7 meses após a primeira compra (M+7).
   - **M8**:  Percentual de clientes que realizaram mais um pedido a 8 meses após a primeira compra (M+8).
   - **M9**:  Percentual de clientes que realizaram mais um pedido a 9 meses após a primeira compra (M+9).
   - **M10**:  Percentual de clientes que realizaram mais um pedido a 10 meses após a primeira compra (M+10).
   - **M11**:  Percentual de clientes que realizaram mais um pedido a 11 meses após a primeira compra (M+11).
   - **M12**:  Percentual de clientes que realizaram mais um pedido a 12 meses após a primeira compra (M+12).

Este [link](https://medium.com/cargox-tecnologia/an%C3%A1lise-de-cohort-em-python-9766948f9af) tem mais detalhes de como é um gráfico de cohort. 

##### 1ª Entrega: Construir as queries em SQL 
Nessa primeira entrega você deve construir uma query para cada tabela que no final vai gerar a tabela requisitada pelo time de CRM. Os dados estão disponíveis no BigQuery no projeto [data-case-study-322621](https://console.cloud.google.com/bigquery?project=data-case-study-322621). Iremos criar um usuário para você realizar consultas no próprio BigQuery via interface, esse usuário será criado com o email fornecido por você.
Para facilitar o entendimento das tabelas raw do dataset estamos disponibilizando as relações entre elas e as chaves. Atenção, como os dados são raw podem haver inconsistências nos dados.

![image](.img/model.png)