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
```
"""### Pedidos - `df_orders`

| Variável 	| Descrição 	|
|:-:	|:-	|
| session_id 	| id da sessão do usuário 	|
| order_id 	| `uuid` do pedido utilizado no service-order (pedidos de outros datasources e antigos não possuem esse id) 	|
| order_number 	| número (id) do pedido único por `datasource` 	|
| order_timestamp_local 	| data do pedido no horário local 	|
| order_shift 	| Período em que foi feito a `order` segundo os horários estabelecidos pelas métricas do iFood.<br>     * **0 - 4:59h** - dawn - alvorecer<br>     * **5 - 9:59h** - café da manhã<br>     * **10 - 14:59h** - lunch - almoço<br>     * **15 - 16:59h** - snack - lanche<br>     * **17 - 23:59h** - dinner - jantar 	|
| last_status_date_local 	| data do último status do pedido no timezone do pedido 	|
| order_total 	| valor total do pedido (`order_items_total` + `delivery_fee`) 	|
| credit 	| valor total de desconto no pedido 	|
| paid_amount 	| valor pago no pedido pelo usuário 	|
| delivery_type 	| tipo de entrega (`delivery` ou `takeout`) 	|
| scheduled 	| `booleano` que indica que houve agendamento do pedido 	|
| scheduled_creation_date_local | data de criação do agendamento do pedido (horário local) 	|
| device_app_version 	| versão do app utilizado no pedido 	|
| device_type 	| tipo de ambiente utilizado no pedido (Mobile/Site) 	|
| device_platform 	| plataforma do device (iOS/Android/Desktop) 	|
| payment_method 	| método de pagamento (Online/Offline) 	|
| customer_state_label 	| estado de entrega do usuário 	|
| customer_city 	| cidade de entrega do usuário 	|
| customer_district 	| bairro de entrega do usuário 	|
| customer_centroid_id 	| representação do centroide do usuário (concatenado do lat/long do usuário, com duas casas decimais) 	|
| customer_has_plus 	| se o usuários tinha serviço de assinatura ativo no momento da compra 	|
| customer_seg_status_last_month 	| status do usuário referente ao mês anterior:<br>    * **NA** - Não se Aplica à Tabela de Segmentação<br>     * **New** - Primeira compra no datasource iFood no mês anterior<br>     * **Ressurected** - Comprou mês anterior, não comprou no retrasado, mas já foi   comprador antes<br>     * **Ativo** - Comprou no mês anterior e no retrasado<br>     * **Churn** - Comprou mês retrasado, mas não comprou no anterior<br>     * **Inactive** - Não compou no mês anterior nem no retrasado, mas já foi   comprador antes 	|
| customer_seg_recency_bucket 	| bucket   referente a quão próximo foi feita a última compra:<br>     * **5** - Último pedido em menos de 7 dias<br>     * **4** - Último pedido entre 7 e 14 dias atrás<br>     * **3** - Último pedido entre 14 e 28 dias atrás<br>     * **2** - Último pedido entre 28 e 91 dias atrás<br>     * **1** - Último pedido há mais de 91 dias 	|
| customer_seg_frequency_bucket 	| bucket   referente a frequência de compra do usuário:<br>     * **5** - Mais que 10 pedidos/mês<br>     * **4** - Entre 4 e 10 pedidos/mês<br>     * **3** - Entre 2 e 4 pedidos/mês<br>     * **2** - Entre 1 e 2 pedidos/mês<br>     * **1** - Menos que 1 pedido/mês 	|
| customer_seg_merchant_offer_bucket 	| bucket   referente à cobertura de restaurantes no endereço do usuário:<br>     * **5** - Mais que 500 restaurantes<br>     * **4** - Entre 150 e 500 restaurantes<br>     * **3** - Entre 90 e 150 restaurantes<br>     * **2** - Entre 30 e 90 restaurantes<br>     * **1** - Até 30 restaurantes 	|
| customer_seg_benefits_sensitivity_bucket 	| * **Alta**   - Acima de 66% das compras usando promoçoes<br>     * **Media** - entre 33% a 66%<br>     * **Baixa** - < 33% 	|
| customer_seg_marlin_tag 	| régua   de classificação Marlin:<br>     * **1** - Marlin<br>     * **2** - Tilapia<br>     * **3** - Retention Carp<br>     * **4** - Subsidy Carp 	|
| customer_seg_gross_income_bucket 	| segmentação   de usuário de acordo com a renda estimada pelo ibge para sua   localização:<br>     * **1** - Acima de 20 Salários mínimos<br>     * **2** - Entre 10 e 20 Salários mínimos<br>     * **3** - Entre 4 e 10 Salários mínimos<br>     * **4** - Entre 2 e 4 Salários Mínimos<br>     * **5** - Abaixo de 2 Salários Mínimos<br>     * **6** - Sem informação 	|
| customer_seg_preffered_shift 	| segmentação do usuário de acordo com o shift com maior número de pedidos. 	|
| frn_id 	| short id do restaurante  	|
| merchant_city 	| cidade do restaurante 	|
| merchant_district 	| bairro do restaurante 	|
| merchant_centroid_id 	| `centroid_id` do merchant 	|
| merchant_dish_type 	| tipo de cozinha do restaurante (Mercado é identificado com   `merchant_dish_type='Mercado'`) 	|
| distance_merchant_customer 	| distancia entre o endereço do usuário e o restaurante em metros 	|
| promo_is_promotion 	| pedido com promoção 	|
| normal_items_quantity 	| quantidade dos itens não promocionados (`promo_is_promotion = 0`) 	|
| promo_items_quantity 	| quantidade dos itens promocionados (`promo_is_promotion = 1`) 	|
| order_lag_at_login 	| diferença entre o dia do pedido e o dia do pedido anterior 	|
| order_lead_at_login 	| diferença entre o dia do pedido e o dia do próximo pedido 	|
| order_monthly_lead 	| diferença entre o mês do pedido e o mês do próximo pedido 	|
| order_monthly_lag 	| diferença entre o mês do pedido e o mês do pedido anterior 	|
| order_date_local 	| data do pedido 	|
| valid_order 	| pedido válido (isso é utilizado para identificar pedidos que não são teste de outros datasources ou informações mais antigas) 	|
| customer_id 	| id do usuário basedo no hash do email do usuário 	|

"""python
df_orders = pd.read_csv(f'{pasta_raiz}/df_orders.csv', sep=',')
"""
### Sessões das visitas realizadas - `df_sessions_visits`


| Variável 	| Descrição 	|
|:-:	|:-	|
| session_id 	| ID universal da   sessão 	|
| dau 	| Usuário   distinto no dia 	|
| platform 	| Plataforma do dispositivo,sendo<br>  * **Android**<br> * **IOS**<br> * **Desktop** se existir. 	|
| user_identifier 	| Identificação do usuário (quando disponivel) 	|
| user_account_uuid 	| Conversa com o dataset account quando houver esse dado 	|
| session_started_at_amsp 	| Data e hora de início da sessão no fuso América/São Paulo 	|
| session_ended_at_amsp 	| Data e hora de término da sessão no fuso América/São Paulo 	|
| session_started_at_utc0 	| Data e hora de início da sessão dentro do UTC0 	|
| session_ended_at_utc0 	| Data e hora de término da sessão dentro do UTC0 	|
| session_duration_seconds 	| Duração da sessão em segundos. Definido pela diferença dos<br>     campos `entity_started_at` e `entity_last_event_at` convertido no formato utc 	|
| device_model 	| Modelo do dispositivo, definido pelo campo `entity_device_model` 	|
| device_manufacturer 	| Fabricante do dispositivo, definido pelo campo `entity_manufacturer` 	|
| sum_event_open 	| Quantidade de eventos de abertura do Aplicativo durante a sessão. 	|
| sum_view_restaurant_screen 	| Quantidade de eventos de visualizações da tela do restaurante 	|
| sum_view_dish_screen 	| Quantidade de eventos de visualizações da tela de pratos 	|
| sum_click_add_item 	| Quantidade de eventos de click do botão Add itens 	|
| sum_view_checkout 	| Quantidade de eventos de visualizações do checkout 	|
| sum_callback_purchase 	| Quantidade de eventos de Callback de pedidos 	|
| order_session_quantity 	| Quantidade de pedidos com sucesso por sessão 	|
| first_order_origin_feature 	| De qual feature veio a compra. Se foi de uma lista, de uma busca, ou outro. 	|
| media_network 	| De mídia veio a sessão Google Adwords, Facebook Ads, Twitter 	|

'''python
df_session_visits = pd.read_csv(f'{pasta_raiz}/df_sessions_visits.csv', sep=',')
'''










