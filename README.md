# Учебный проект, посвященный сжатию текста при помощи авторегрессионной модели

## Описание работы 
Данный проект реализует сжатие текста с использованием LSTM модели и адаптивного арифметического кодирования (ААК). 
В папке ./data/ находится текстовый файл enwik5 для сжатия, являющийся первыми 10^5 байтами enwiki-20060303-pages-articles.xml.

Kодировщик использует LSTM для вычисления вектора вероятностей следующего символа на основе предыдущих. Фактическое значение символа далее кодируется с помощью ААК. Затем веса модели обновляются. Это повторяется для всех символов файла.

Во время декодирования происходит симметричный процесс, декодирование с помощью ААК, предсказание символа при помощи LSTM, обновление модели и т.д.
Декодер работает симметрично, поэтому нет необходимости передавать параметры модели.

В качестве ААК используется реализация из https://github.com/nayuki/Reference-arithmetic-coding 

Параметры бейзлайна:
| Версия | Исходный размер, байты | Размер после сжатия, байты | Коэффициент сжатия | Затраченное время, с |
|:------:|:----------------------:|:--------------------------:|:------------------:|:------------------:  |
| Baseline | 100000 | 47150 | 2.12 | 783 |
| Modified | 100000 | 57709 | 1.75 | 201 |


## Описание задания к лабораторной работе
Улучшить код так, чтобы он:
- либо на том же сжатии показывал уменьшение времени кодирования и декодирования на 100%; 
- либо обеспечивал улучшение коэффициента сжатия на 100% при тех же временных затратах.

Можно улучшать следующие модули:
- Предобработка: заменять слова из предварительно созданного словаря уникальным кодом, использовать идею из Byte-Pair Encoding токенизации и т.д.;
- Нейронная сеть: использование другой архитектуры (GRU, Transformer и др.), изменить количество слоёв, функции активации, связи между слоями и т.д.;
- Арифметический кодер: учесть возможную память источника, оценка вероятностей и т.д.

Требования к реализации:
- Результаты должны быть продемонстрированы на enwik5 из папки ./data/;
- Восстановленый после сжатия файл должен полностью совпадать с оригинальным;
- В результатах приложить таблицу выше, обновив значения базового решения для вашего устройства и добавив строчку с улучшенным решением.

На почту eabelyaev@itmo.ru прислать отчет в виде презентации в pdf формате, который включает в себя:
- ФИО студента, номер группы.
- Описание предложенной модификации и результаты.
- Ссылку на репозиторий с исходным кодом проекта и инструкцию по запуску.

## Описание задания к лабораторной работе
- Increased batch size
- Reduced units per layer for speed
- Reduced layers
- Reduced embedding size

## Литература
Подробнее про принцип работы можно прочитать в https://bellard.org/nncp/nncp.pdf или https://arxiv.org/pdf/2407.07723 (здесь тот же принцип, но в качестве модели используется LLM и кроме текста сжимают другие типы данных)