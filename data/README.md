# 📁 Данные

## Файл: `depression_treatment_efficiency.csv`

Датасет содержит анонимизированные данные о пациентах, проходящих когнитивно-поведенческую терапию (КПТ) при депрессии.

### Описание признаков

| Столбец             | Тип данных | Диапазон  | Описание                                              |
|---------------------|------------|-----------|-------------------------------------------------------|
| `age`               | int        | 18–70     | Возраст пациента (лет)                                |
| `symptom_duration`  | int        | 1–12      | Длительность симптомов депрессии до начала терапии (месяцев) |
| `sleep_quality`     | int        | 1–10      | Субъективная оценка качества сна (1 — очень плохо, 10 — отлично) |
| `anxiety_level`     | int        | 1–10      | Уровень тревожности (1 — минимальный, 10 — максимальный) |
| `life_events`       | int        | 0–10      | Количество стрессовых жизненных событий за последний год |
| `treatment_success` | int        | 0 или 1   | **Целевая переменная**: 1 — КПТ была эффективна, 0 — нет |

### Характеристики датасета

- **Строк**: 1000
- **Столбцов**: 6
- **Пропущенных значений**: нет
- **Распределение классов**: несбалансированное (≈66% класс 0 / ≈34% класс 1)

### Как добавить датасет

Поместите файл `depression_treatment_efficiency.csv` в эту папку (`data/`).

Если у вас нет файла, вы можете сгенерировать синтетический датасет:

```python
import pandas as pd
import numpy as np

np.random.seed(42)
n = 1000

data = pd.DataFrame({
    'age': np.random.randint(18, 71, n),
    'symptom_duration': np.random.randint(1, 13, n),
    'sleep_quality': np.random.randint(1, 11, n),
    'anxiety_level': np.random.randint(1, 11, n),
    'life_events': np.random.randint(0, 11, n),
})

# Логика целевой переменной (пример)
score = (
    - 0.5 * data['symptom_duration']
    - 0.4 * data['anxiety_level']
    - 0.3 * data['life_events']
    + 0.3 * data['sleep_quality']
    + np.random.normal(0, 1, n)
)
data['treatment_success'] = (score > score.median()).astype(int)

data.to_csv('data/depression_treatment_efficiency.csv', index=False)
print("Датасет создан:", data.shape)
```

> **Примечание**: Данный датасет является учебным/синтетическим и не предназначен для клинического применения.
