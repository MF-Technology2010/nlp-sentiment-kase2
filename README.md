# NLP: Классификация тональности русскоязычных твитов (Кейс 2)

Финальное задание по курсу «Обработка естественного языка» (3 семестр).
Система классифицирует текстовые сообщения по тональности на 2 класса:
**негативный**, **позитивный**.

## 🎯 Что внутри

- Предобработка текста: очистка, лемматизация (pymorphy3), удаление стоп-слов
- Векторизация: TF-IDF (word n-grams 1-2 + char_wb n-grams 3-5)
- Классификация **без трансформеров**: Logistic Regression + Linear SVM
- **Ансамбль** двух моделей с весами (soft voting)
- Анализ ошибок: confusion matrix + разбор топ-20 misclassified примеров
- Отчёт: `REPORT.md`

## 📊 Результаты на тестовой выборке

| Модель              | Accuracy | F1-macro |
|---------------------|----------|----------|
| LogReg (TF-IDF)     | **0.7887** | **0.7787** |
| SVM (TF-IDF)        | 0.7781   | —        |
| Ансамбль 50/50      | 0.7834   | —        |

**Финальная модель: LogReg, accuracy 78.9%.**

Confusion matrix — в файле `confusion_matrix.png`.

## 🚀 Запуск в Google Colab

1. Откройте [Google Colab](https://colab.research.google.com/)
2. `File → Upload notebook` → выберите `nlp_sentiment_kase2.ipynb`
3. `Runtime → Run all` (или пошагово Shift+Enter)
4. Готово — в конце ноутбука метрики, confusion matrix и анализ ошибок

Ноутбук сам скачает датасет, обучит модели и сохранит артефакты.

## 📁 Файлы репозитория

```

.
├── README.md                    # этот файл
├── REQUIREMENTS.txt             # зависимости
├── nlp_sentiment_kase2.ipynb    # ноутбук с полным пайплайном
├── confusion_matrix.png         # матрица ошибок финальной модели
└── REPORT.md                    # текст отчёта для сдачи

```

## 📚 Датасет

**RuSentiTweet** (Smetanin, 2020) — русскоязычные твиты с разметкой тональности.

- Источник: https://huggingface.co/datasets/psytechlab/RuSentiTweet
- Загружается автоматически через `datasets.load_dataset('psytechlab/RuSentiTweet')`
- Исходный размер: 9 641 train / 1 072 val / 2 679 test
- Исходные классы: 5 (positive, negative, neutral, speech, skip)
- **Рабочие классы: 2** (negative, positive). Классы `neutral`, `speech`, `skip` исключены: `neutral` — из-за низкой разделимости в твитах (SOTA без трансформеров ≈ 70%), `speech` и `skip` — служебные, не относятся к тональности.
- Train после фильтрации: 4 091 пример, Val: 429, Test: 1 131

## 🔧 Локальный запуск (опционально)

```bash
pip install -r requirements.txt
jupyter notebook nlp_sentiment_kase2.ipynb
```

## 📝 Отчёт

Текст отчёта — в `REPORT.md`. Его можно сконвертировать в PDF (Google Docs)
для прикрепления в ЛМС.

## 👥 Авторы

- Диана Баширова (Кейс 2)
- Команда 14

## 📄 Лицензия

Учебный проект. Код — MIT.

