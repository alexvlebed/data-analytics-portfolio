# Olist E-Commerce: анализ сроков доставки

## О проекте
Аналитический проект на данных [Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce). Проверка статистической гипотезы о влиянии рассрочки на срок фактической доставки заказа.

## Бизнес-вопрос
Отличается ли средний срок фактической доставки у заказов с рассрочкой и без неё?

**Гипотезы:**
- H0: среднее время доставки заказов с рассрочкой (`payment_installments > 1`) равно среднему времени доставки заказов без рассрочки (`payment_installments = 1`).
- H1: среднее время доставки различается.
Уровень значимости: α = 0.05. Тест: двухвыборочный t-тест (`scipy.stats.ttest_ind`).

## Данные
Использованы две таблицы датасета:
| Таблица | Строк | Столбцов |
|---|---:|---:|
| `olist_orders_dataset` | 99 441 | 8 |
| `olist_order_payments_dataset` | 103 886 | 5 |

Ключевые поля: `order_id`, `order_status`, `order_purchase_timestamp`, `order_delivered_customer_date`, `payment_installments`, `payment_value`.
## Ход работы:
**Предобработка**
- Явных дубликатов не обнаружено, категориальные значения проверены.
- Пять временных столбцов приведены к типу `datetime64[ns]`.

**Формирование выборки**
- Отфильтрованы только завершённые заказы (`order_status == 'delivered'`) — 96 478 строк.
- Удалены 8 строк с пропусками в рассчитанном признаке `delivery_days` (0.008%).
- Отрицательных значений `delivery_days` не обнаружено.

**Инженерия признаков**
- `delivery_days` = `order_delivered_customer_date` − `order_purchase_timestamp` (в днях). В качестве точки отсчёта выбран момент покупки, поскольку анализ ведётся с позиции клиента.
- Платежи агрегированы по `order_id`: `payment_installments` через `max`, `payment_value` через `sum`.
- `has_installments` = `payment_installments > 1`.

**Проверка гипотезы**
- Сформированы две независимые выборки: с рассрочкой и без.
- Проведён двухвыборочный t-тест для сравнения средних значений `delivery_days`, результат сопоставлен с α = 0.05.

## Стек
Python, pandas, numpy, scipy, matplotlib, seaborn, kagglehub. Работа выполнена в Google Colab.

## Структура репозитория
```
olist-delivery-analysis/
└── Olist_Analysis.ipynb
```
## Запуск
```bash
pip install pandas numpy scipy matplotlib seaborn kagglehub
jupyter notebook Olist_Analysis.ipynb
```
Датасет загружается автоматически через `kagglehub.dataset_download('olistbr/brazilian-ecommerce')`.
