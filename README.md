# 🧠 Прогноз эффективности когнитивно-поведенческой терапии (КПТ)

Машинное обучение для предсказания успешности лечения депрессии методом КПТ.

---

## 📋 О проекте

Проект решает задачу **бинарной классификации**: по характеристикам пациента предсказывается, будет ли когнитивно-поведенческая терапия эффективной (`treatment_success = 1`) или нет (`treatment_success = 0`).

Применяются три подхода:
1. **Единая логистическая регрессия** — базовая модель
2. **Кластерный подход** — пациенты разбиваются на группы (KMeans), для каждой обучается своя модель
3. **Настроенные модели** — логистическая регрессия и случайный лес с подбором гиперпараметров через GridSearchCV

---

## 📂 Структура проекта

```
depression-treatment-efficiency/
├── Прогноз_эффективности_КПТ.ipynb   # Основной ноутбук
├── data/
│   └── README.md                      # Описание датасета
├── requirements.txt                   # Зависимости
└── README.md                          # Этот файл
```

---

## 📊 Датасет

| Признак            | Тип       | Описание                                |
|--------------------|-----------|------------------------------------------|
| `age`              | int       | Возраст пациента                         |
| `symptom_duration` | int       | Длительность симптомов (в месяцах)       |
| `sleep_quality`    | int (1–10)| Качество сна                             |
| `anxiety_level`    | int (1–10)| Уровень тревожности                      |
| `life_events`      | int       | Количество стрессовых жизненных событий  |
| `treatment_success`| int (0/1) | **Целевая переменная**: успех КПТ        |

- **Размер**: 1000 строк × 6 столбцов
- **Разбивка**: 70% обучение / 30% тест

> Датасет находится в папке `data/`. Подробнее — в [`data/README.md`](data/README.md).

---

## 🔬 Методы и инструменты

### Предобработка
- Нормализация признаков: `StandardScaler`
- Стратифицированное разбиение: `train_test_split`

### Визуализация и снижение размерности
| Метод   | Описание                                        |
|---------|-------------------------------------------------|
| PCA     | Линейное снижение размерности                   |
| t-SNE   | Нелинейное, несколько значений perplexity        |
| PaCMAP  | Современный метод, сохраняющий глобальную структуру |

### Кластеризация
- **KMeans** с выбором числа кластеров по методу локтя → **3 кластера**

### Классификация
| Модель                               | Метрики (тест)                        |
|--------------------------------------|---------------------------------------|
| Baseline LogisticRegression          | Accuracy: 0.793                       |
| Tuned LogisticRegression (Pipeline)  | CV F1: 0.657                          |
| **RandomForest (Tuned)**             | **CV F1: 0.850** ✅                   |
| Cluster-based LogisticRegression     | F1: 0.789, ROC-AUC: 0.881            |

### Оценка качества
- Accuracy, Precision, Recall, F1, ROC-AUC
- Матрица ошибок
- Кросс-валидация: `StratifiedKFold` (5 фолдов)
- Подбор гиперпараметров: `GridSearchCV`

### Интерпретация
- Коэффициенты логистической регрессии
- Топ факторов влияния:
  - 🔴 Отрицательные: `symptom_duration`, `life_events`, `anxiety_level`
  - 🟢 Положительные: `sleep_quality`

---

## 🚀 Запуск

### 1. Клонировать репозиторий

```bash
git clone https://github.com/<ваш-username>/depression-treatment-efficiency.git
cd depression-treatment-efficiency
```

### 2. Установить зависимости

```bash
pip install -r requirements.txt
```

### 3. Добавить датасет

Поместите файл `depression_treatment_efficiency.csv` в папку `data/`.

### 4. Запустить ноутбук

```bash
jupyter notebook "Прогноз_эффективности_КПТ.ipynb"
```

Или открыть через Google Colab:

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/<ваш-username>/depression-treatment-efficiency/blob/main/Прогноз_эффективности_КПТ.ipynb)

---

## 📈 Ключевые результаты

- **Random Forest** показал лучший результат: CV F1 = **0.850**
- Кластерный подход даёт хорошую интерпретируемость: ROC-AUC = **0.881**
- Наиболее значимый негативный предиктор — `symptom_duration` (длительность симптомов)

---

## 🛠 Технологический стек

![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter)
![scikit-learn](https://img.shields.io/badge/scikit--learn-1.x-f7931e?logo=scikit-learn)
![pandas](https://img.shields.io/badge/pandas-2.x-150458?logo=pandas)

- `pandas`, `numpy` — работа с данными
- `matplotlib`, `seaborn` — визуализация
- `scikit-learn` — ML модели, метрики, пайплайны
- `pacmap` — снижение размерности

---

## 👤 SenoritaLiza

**[Ныркова Елизавета]**  
[GitHub](https://github.com/SenoritaLiza) · [LinkedIn](https://linkedin.com/in/SenoritaLiza)

