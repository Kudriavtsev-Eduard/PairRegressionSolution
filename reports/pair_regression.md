# Решение расчетно-графичкской работы №1 "Изучение парной регрессии"
### Студент: Кудрявцев Эдуард Сергеевич, M3335, 354409

## Задание 1
В качестве dataset'а были взяты погодные показания в венгерском городе Сегеде начала 2006 года

Ссылка на источник: https://www.kaggle.com/datasets/budincsevity/szeged-weather

Главным объектом анализа была зависимость показателя "Ощущаемая температура" от реальной температуры


    ---------------------------------------------------------------------------

    FileNotFoundError                         Traceback (most recent call last)

    Cell In[2], line 1
    ----> 1 df = pandas.read_csv('../data/weatherHistory.csv')
          2 print(len(df))
          3 x_title = 'Temperature (C)'


    File ~/PycharmProjects/PairRegressionSolution/.venv/lib/python3.13/site-packages/pandas/io/parsers/readers.py:1026, in read_csv(filepath_or_buffer, sep, delimiter, header, names, index_col, usecols, dtype, engine, converters, true_values, false_values, skipinitialspace, skiprows, skipfooter, nrows, na_values, keep_default_na, na_filter, verbose, skip_blank_lines, parse_dates, infer_datetime_format, keep_date_col, date_parser, date_format, dayfirst, cache_dates, iterator, chunksize, compression, thousands, decimal, lineterminator, quotechar, quoting, doublequote, escapechar, comment, encoding, encoding_errors, dialect, on_bad_lines, delim_whitespace, low_memory, memory_map, float_precision, storage_options, dtype_backend)
       1013 kwds_defaults = _refine_defaults_read(
       1014     dialect,
       1015     delimiter,
       (...)   1022     dtype_backend=dtype_backend,
       1023 )
       1024 kwds.update(kwds_defaults)
    -> 1026 return _read(filepath_or_buffer, kwds)


    File ~/PycharmProjects/PairRegressionSolution/.venv/lib/python3.13/site-packages/pandas/io/parsers/readers.py:620, in _read(filepath_or_buffer, kwds)
        617 _validate_names(kwds.get("names", None))
        619 # Create the parser.
    --> 620 parser = TextFileReader(filepath_or_buffer, **kwds)
        622 if chunksize or iterator:
        623     return parser


    File ~/PycharmProjects/PairRegressionSolution/.venv/lib/python3.13/site-packages/pandas/io/parsers/readers.py:1620, in TextFileReader.__init__(self, f, engine, **kwds)
       1617     self.options["has_index_names"] = kwds["has_index_names"]
       1619 self.handles: IOHandles | None = None
    -> 1620 self._engine = self._make_engine(f, self.engine)


    File ~/PycharmProjects/PairRegressionSolution/.venv/lib/python3.13/site-packages/pandas/io/parsers/readers.py:1880, in TextFileReader._make_engine(self, f, engine)
       1878     if "b" not in mode:
       1879         mode += "b"
    -> 1880 self.handles = get_handle(
       1881     f,
       1882     mode,
       1883     encoding=self.options.get("encoding", None),
       1884     compression=self.options.get("compression", None),
       1885     memory_map=self.options.get("memory_map", False),
       1886     is_text=is_text,
       1887     errors=self.options.get("encoding_errors", "strict"),
       1888     storage_options=self.options.get("storage_options", None),
       1889 )
       1890 assert self.handles is not None
       1891 f = self.handles.handle


    File ~/PycharmProjects/PairRegressionSolution/.venv/lib/python3.13/site-packages/pandas/io/common.py:873, in get_handle(path_or_buf, mode, encoding, compression, memory_map, is_text, errors, storage_options)
        868 elif isinstance(handle, str):
        869     # Check whether the filename is to be opened in binary mode.
        870     # Binary mode does not support 'encoding' and 'newline'.
        871     if ioargs.encoding and "b" not in ioargs.mode:
        872         # Encoding
    --> 873         handle = open(
        874             handle,
        875             ioargs.mode,
        876             encoding=ioargs.encoding,
        877             errors=errors,
        878             newline="",
        879         )
        880     else:
        881         # Binary mode
        882         handle = open(handle, ioargs.mode)


    FileNotFoundError: [Errno 2] No such file or directory: '../data/weatherHistory.csv'


## Задание 2


    
![png](/home/runner/work/PairRegressionSolution/PairRegressionSolution/reports/pair_regression_5_0.png)
    


По корреляционному облаку наблюдаем возможную тесную прямую линейную связь между показателями

## Задание 3

Для всех дальнейших вычислений Возьмем уровень значимости как $\alpha=0,05$

Нормальность температуры и ощутимой температуры проверяем с помощью теста Д'Агостино-Пирсона

Далее посчитаем коэффициент корреляции Пирсона и проверим его значимость по t-статистике $t_н = \dfrac{|r|*\sqrt{n-2}}{\sqrt{1-r^2}}$

Доверительный интервал для него будет вычисляться с помощью Z-преобразования Фишера: $(arcth r^{*} - \dfrac{u_{\gamma}}{n-3}, arcth r^{*} + \dfrac{u_{\gamma}}{n-3})$, где $u_{\gamma}$ - квантиль стандартного нормального распределения уровня $\gamma=1-\dfrac{\alpha}{2}$

    Нормальность X: True
    Нормальность Y: True
    
    Коэффициент корреляции Пирсона: 0.9806870859405218
    Значимость коэффициента корреляции Пирсона:
        Наблюдаемая статистика (модуль): 86.55790758983747
        Критическая статистика (модуль): 1.6499829759955271
        Значимость?: True
    Доверительный интервал: (0.9804330069494428, 0.980937897451177)


## Задание 4

    Уравнение регрессии: y = -2.911 + 1.187*x
    Коэффициент детерминации: 0.962
    F-статистика: 7492.271
    F-критическая: 0.004
    Значимоть уравнения (F-тест): True
    t-статистики: 
        a: -16.569
        b: 86.558
        Критическая: -1.650
    Значимость коэффициентов (t-тест)
        a: True
        b: True
    Средняя ошибка аппроксимации: 11.786%
    Средняя эластичность: 1.309


    График регрессии



    
![png](/home/runner/work/PairRegressionSolution/PairRegressionSolution/reports/pair_regression_11_1.png)
    


## Задание 5:

Условия Гаусса-Маркова:
1. $\sum \epsilon_i=0$
2. $cov(\epsilon_i, \epsilon_{i-1}) = 0$
3. $\sigma^2_{\epsilon} = const$
4. $\epsilon_i$ имеет нормальное распределение

    График остатков



    
![png](/home/runner/work/PairRegressionSolution/PairRegressionSolution/reports/pair_regression_13_1.png)
    


    Проверка условий Гаусса-Маркова
        1. Cумма остатков ~=0: True
        2. Отсутствие автокорреляции (тест Бройша-Годфрея): False
        3. Отсутствие гетероскедастичности (тест Уайта): False
        4. Нормальность остатков: True


## Задание 6

### Квадратичная модель

    Коэффициенты
    Intercept   -6.655228
    x            1.846937
    I(x ** 2)   -0.026277
    dtype: float64
    Можно ли заменить линейной?: True


### Кубическая модель

    Коэффициенты
    Intercept   -5.005055
    x            1.390192
    I(x ** 2)    0.012659
    I(x ** 3)   -0.001034
    dtype: float64
    Можно ли заменить линейной?: True



    
![png](/home/runner/work/PairRegressionSolution/PairRegressionSolution/reports/pair_regression_21_0.png)
    


j-тест Стьюдента показал, что обе нелинейные модели можно заменить линейными, поэтому в дальнейшем продолжим работать именно с линейными моделями

## Задание 7

Вывод: действительно, между величинами наблюдается тесная линейная связь, однако присутствие автокорреляции и гетероскедастичности скорее всего говорят о необходимости перехода к многофакторным моделям для получения более точной аппроксимации
