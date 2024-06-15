# Репозиторий команды BitVision в задаче нахождения дефектов сварных швов

В рамках данного решения представлены несколько моделей поколения Yolov8 с функционалом SAHI, обученных на выданном в
рамках хакатона AtomicHack'24 датасете.

## Обученные модели представлены в папке /models:

- Модель Yolov8n, обученная на 150 эпохах с аугментацией.
- Модель Yolov8s, обученная на 150 эпохах с аугментацией.
- Модель Yolov8m, обученная на 100 эпохах с аугментацией.
- Модель Yolov8l, обученная на 150 эпохах с аугментацией.
  Подробнее с метриками можно познакомиться в папках данных моделей, либо в презентации команды.

## Особенности обучения моделей Yolov8 для данной задачи

- Ввиду дисбаланса классов датасета необходимо было обеспечить равномерное попадание всех видов картинок и классов в
  тренировочную и валидационную выборку.
  Для этого применялось разбиение на основе выделенных сеткой VGG классов картинок. Подробнее с алгоритмом разбиения
  можно ознакомиться в /utils/stratify_object_detection_dataset.ipynb
- Датасет нельзя назвать большим и достаточным для обеспечения обобщения нейронной сети на всей выборки изображений. Для
  улучшения точности детектирования модели были обучены с применением аугментации.
  Подробнее с типами применяемых аугментаций можно ознакомиться в файле /models/construction_defects_aug.yaml.

## Также в алгоритм была интегрирована библиотека SAHI (Slicing Aided Hyper Inference) для увеличения точности детекции сварных швов.

Интегрирование данного функционала позволило увеличить точность обнаружения мелких дефектов швов, а также находить с
большей уверенностью дефекты, пересекающие другие дефекты.
Подробно про улучшение модели с помощью SAHI можно увидеть в презентации команды.

# В рамках хакатона также было разработано фронтенд-решение на базе библиотеки Streamlit, позволяющее достаточно быстро развернуть и протестировать модель.

В дефолтной конфигурации сервиса можно попробовать протестировать модели как вместе с алгоритмом SAHI, так и без него.

# Для деплоя фронтенд-решения необходимо выполнить следующие шаги

## Запуск через Docker

- Спулить гит-репозиторий проекта
- Скачать git-lfs файлы командой `git lfs pull`
- Собрать Docker образ командой `docker build -t bitvision .`
- Запустить Docker контейнер командой `docker run -p 8501:8501 bitvision`
- Перейти по адресу http://localhost:8501

Disclaimer: для работы необходим скаченный git lfs и запущенный docker daemon

## Локальный запуск

- Спулить гит-репозиторий проекта
- Скачать git-lfs файлы командой `git lfs pull`
- Установить зависимости командой `pip install -e .`
- Запустить Streamlit приложение командой `streamlit run bin.py`
- Перейти по адресу http://localhost:8501

Disclaimer: для работы необходим скаченный git lfs

# Материалы, использованные для разработки решения:

- https://github.com/ultralytics/ultralytics
- https://github.com/obss/sahi
- https://github.com/streamlit/streamlit
- https://git-lfs.com/
- https://www.docker.com/get-started/
