### Segementação de clientes - `df_customer_segmentation`



| Variável 	| Descrição 	|
|:-:	|:-	|
| customer_id 	| ID de identificação do usuário   (o mesmo usado na df_orders) 	|
| segmentation_month 	| mês da segmentação 	|
| ifood_status_last_month 	| Status   do usuário no mês passado:<br>     * **New**: realizou a sua primeira compra no mês de comparação.<br>     * **Active**: realizou pelo menos uma compra no mês anterior e no mês de   comparação.<br> * **Churn**: realizou pelo menos uma compra no mês passado e nenhuma no   mês de comparação.<br>     * **Inactive**: não realiza compras há 2 meses ou mais.<br>    * **Ressurected**: foi Churn ou Inactive no mês passado e voltou a comprar no mês   de comparação. 	|
| ifood_status 	| Status   do usuário no mês atual:<br>     * **New**: realizou a sua primeira compra no mês de comparação.<br>     * **Active**: realizou pelo menos uma compra no mês anterior e no mês   atual.<br>     * **Churn**: realizou pelo menos uma compra no mês passado e nenhuma no mês de   comparação.<br>     * **Inactive**: não realiza compras há 2 meses ou mais.<br>     * **Ressurected**: foi Churn ou Inactive no mês passado e voltou a comprar no mês   de comparação. 	|
| orders_last_91d 	| Contagem   de pedidos concluídos nos últimos 91 dias. 	|
| qtt_orders_last_year 	| Contagem   de pedidos concluídos no último ano. 	|
| qtt_valid_orders 	| Contagem   de pedidos validos na vida ( `last_status` != `'CANCELLED'` ). 	|
| last_valid_order_date 	| Data   do último pedido validos. 	|
| qtt_invalid_orders 	| Contagem   de pedidos inválidos na vida ( `last_status` = `'CONCLUDED'`). 	|
| last_invalid_order_date 	| Data   do último pedido inválido. 	|
| marlin_tag 	| Existem três tipos de clientes no mercado segundo o iFood, nesse caso classificados como peixe: <br>     * **Marlin** - aqueles que nadam perto da superfice, o melhor<br>     * **Tilapia** - aqueles que nadam no meio, a média<br>     * **Carp** - aqueles que nadam no fundo, o não tão bom<br>      	|
| recency_months 	| Meses   desde o último pedido. 	|
| last_nps 	| Última   avaliação de NPS (Net Promoter Score) no app. 	|
| registration_date 	| Data de registro do usuário. 	|
| customer_lifetime_days 	| Dias desde o primeiro pedido do usuário. 	|
| customer_lifetime_months 	| Meses desde o primeiro pedido do usuário. 	|
| top_3_merchants_code 	| `merchant_id` dos top 3 merchants em que o usuário mais pediu. 	|
| was_mub_last_month 	| `booleano` se o usuário foi mub (*monthly unique buyer*) no mês passado. 	|
| buyer_last_91d 	| `booleano` se o usuário fez pelo menos uma compra nos últimos 91 dias. 	|
| top_city 	| Cidade em que o usuário realizou mais pedidos. 	|
| top_district 	| Bairro em que o usuário realizou mais pedidos. 	|
| top_centroid_id 	| Top `centroid_id` em que o usuário realizou mais pedidos. |
| first_order_date 	| Data do primeiro pedido. 	|
| last_order_date 	| Data do último pedido. 	|
| days_to_reorder_at_datasource 	| Intervalo entre as compras at_datasource 	|
| days_to_reorder_at_concluded 	| Intervalo entre comprar considerando at_concluded 	|
| rfv_score 	| Score de recencia, frequência e valor. 	|
| recency_days 	| Diferença em dias entre hoje e a última compra do usuário. 	|
| recency_days_bucket 	| Bucket de `recency_days`. 	|
| recency_days_bucket_description 	| Explica as quebras do `recency_days_bucket`. 	|
| freq_last_91d 	| Frequência do usuário nos últimos 91 dias. 	|
| freq_last_91d_bucket 	| Bucket de frequência do usuário nos últimos 91 dias. 	|
| freq_last_91d_bucket_description 	| Explica as quebras do `freq_last_91d_bucket`. 	|
| avg_aov_last_91d 	| Média de `order_total` dos últimos 91 dias. 	|
| maturity_orders 	| Total de pedidos realizados pelo usuário. 	|
| maturity_orders_bucket 	| Bucket do total de pedidos realizados pelo usuário. 	|
| maturity_orders_bucket_description 	| Explica as quebras do `maturity_orders_bucket_description` . 	|
| benefits_sensitivity 	| Índice de sensibilidade a benefícios. 	|
| benefits_sensitivity_bucket 	| Bucket do índice de sensibilidade a beneficios. 	|
| preferred_shift_bucket 	| Bucket de turno preferido. 	|
| preferred_shift_bucket_description 	| Explica as quebras do `preferred_shift_bucket`. 	|
| merchant_variety 	| Índice de variedade de restaurantes nas compras do usuário. 	|
| merchant_variety_bucket 	| Bucket do índice de variedade de restaurantes nas compras do usuário. 	|
| merchant_offer 	| Cobertura de restaurantes no `centroid_id` do usuário. 	|
| merchant_offer_bucket 	| Bucket da cobertura de restaurantes no `centroid_id` do usuário. 	|
| merchant_offer_bucket_description 	| Explica as quebras do `merchant_offer_bucket` . 	|
| top_dish_bucket 	| Bucket da cozinha favorita do usuário. 	|
| top_dish_bucket_description 	| Explica as quebras do `top_dish_bucket`. 	|
| preferred_dishes 	| Array contém as cozinhas favoritas do usuário. 	|
| preferred_dishes_code 	| Array contém o código das cozinhas favoritas do usuário. 	|
"""

```python
import pandas as pd
df_customer_segmentation = pd.read_csv(f'{pasta_raiz}/df_customer_segmentation.csv', sep=';')

from pandas_profiling import ProfileReport
profile = ProfileReport(df_customer_segmentation, title='Costumer segmentation')
profile.to_file(f'{pasta_raiz}/df_customer_segmentation.html')

df_customer_segmentation = pd.read_csv(f'{pasta_raiz}/df_customer_segmentation.csv', sep=';')
df_customer_segmentation.head()


```

