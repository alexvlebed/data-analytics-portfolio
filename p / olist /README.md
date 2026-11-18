# Olist Analysis — отличается ли средний срок фактической доставки у заказов с рассрочкой и без рассрочки?
Ad-hoc аналитический запрос от команды роста Olist: понять, влияет ли рассрочка на срок доставки.

---
## Контекст
[Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) — бразильский маркетплейс. 
Цель — исследование и выводы.

---
## Бизнес-вопрос
Отличается ли средний срок фактической доставки у заказов с рассрочкой и без рассрочки?

---
## Данные
Датасет: [Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)
Объём: ~100k заказов, 9 CSV-таблиц, ~120 МБ.

Используемые таблицы:
| Файл | Содержание |
|---|---|
| `olist_orders_dataset.csv` | Заказы, статусы, таймстемпы |
| `olist_order_payments_dataset.csv` | Платежи |

---
## 🛠 Стек
- **Python 3.10+**
- `pandas`, `numpy` — обработка данных
- `matplotlib`, `seaborn` — визуализации
- `scipy.stats` — статистические тесты
- **Jupyter Notebook** (локально или Google Colab)

---
