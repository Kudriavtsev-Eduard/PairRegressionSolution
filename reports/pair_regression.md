# Решение расчетно-графичкской работы №1 "Изучение парной регрессии"
### Студент: Кудрявцев Эдуард Сергеевич, M3335, 354409

## Задание 1
В качестве dataset'а были взяты погодные показания в венгерском городе Сегеде начала 2006 года

Ссылка на источник: https://www.kaggle.com/datasets/budincsevity/szeged-weather

Главным объектом анализа была зависимость показателя "Ощущаемая температура" от реальной температуры

    96453





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Formatted Date</th>
      <th>Summary</th>
      <th>Precip Type</th>
      <th>Temperature (C)</th>
      <th>Apparent Temperature (C)</th>
      <th>Humidity</th>
      <th>Wind Speed (km/h)</th>
      <th>Wind Bearing (degrees)</th>
      <th>Visibility (km)</th>
      <th>Loud Cover</th>
      <th>Pressure (millibars)</th>
      <th>Daily Summary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2006-04-01 00:00:00.000 +0200</td>
      <td>Partly Cloudy</td>
      <td>rain</td>
      <td>9.472222</td>
      <td>7.388889</td>
      <td>0.89</td>
      <td>14.1197</td>
      <td>251.0</td>
      <td>15.8263</td>
      <td>0.0</td>
      <td>1015.13</td>
      <td>Partly cloudy throughout the day.</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2006-04-01 01:00:00.000 +0200</td>
      <td>Partly Cloudy</td>
      <td>rain</td>
      <td>9.355556</td>
      <td>7.227778</td>
      <td>0.86</td>
      <td>14.2646</td>
      <td>259.0</td>
      <td>15.8263</td>
      <td>0.0</td>
      <td>1015.63</td>
      <td>Partly cloudy throughout the day.</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2006-04-01 02:00:00.000 +0200</td>
      <td>Mostly Cloudy</td>
      <td>rain</td>
      <td>9.377778</td>
      <td>9.377778</td>
      <td>0.89</td>
      <td>3.9284</td>
      <td>204.0</td>
      <td>14.9569</td>
      <td>0.0</td>
      <td>1015.94</td>
      <td>Partly cloudy throughout the day.</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2006-04-01 03:00:00.000 +0200</td>
      <td>Partly Cloudy</td>
      <td>rain</td>
      <td>8.288889</td>
      <td>5.944444</td>
      <td>0.83</td>
      <td>14.1036</td>
      <td>269.0</td>
      <td>15.8263</td>
      <td>0.0</td>
      <td>1016.41</td>
      <td>Partly cloudy throughout the day.</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2006-04-01 04:00:00.000 +0200</td>
      <td>Mostly Cloudy</td>
      <td>rain</td>
      <td>8.755556</td>
      <td>6.977778</td>
      <td>0.83</td>
      <td>11.0446</td>
      <td>259.0</td>
      <td>15.8263</td>
      <td>0.0</td>
      <td>1016.51</td>
      <td>Partly cloudy throughout the day.</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>295</th>
      <td>2006-04-20 07:00:00.000 +0200</td>
      <td>Foggy</td>
      <td>rain</td>
      <td>10.161111</td>
      <td>10.161111</td>
      <td>0.99</td>
      <td>0.3381</td>
      <td>81.0</td>
      <td>0.4347</td>
      <td>0.0</td>
      <td>1013.61</td>
      <td>Foggy starting overnight continuing until morn...</td>
    </tr>
    <tr>
      <th>296</th>
      <td>2006-04-20 08:00:00.000 +0200</td>
      <td>Foggy</td>
      <td>rain</td>
      <td>11.244444</td>
      <td>11.244444</td>
      <td>0.98</td>
      <td>2.7531</td>
      <td>358.0</td>
      <td>0.6923</td>
      <td>0.0</td>
      <td>1013.90</td>
      <td>Foggy starting overnight continuing until morn...</td>
    </tr>
    <tr>
      <th>297</th>
      <td>2006-04-20 09:00:00.000 +0200</td>
      <td>Foggy</td>
      <td>rain</td>
      <td>12.244444</td>
      <td>12.244444</td>
      <td>0.99</td>
      <td>2.2540</td>
      <td>152.0</td>
      <td>2.2057</td>
      <td>0.0</td>
      <td>1014.31</td>
      <td>Foggy starting overnight continuing until morn...</td>
    </tr>
    <tr>
      <th>298</th>
      <td>2006-04-20 10:00:00.000 +0200</td>
      <td>Overcast</td>
      <td>rain</td>
      <td>13.911111</td>
      <td>13.911111</td>
      <td>0.92</td>
      <td>8.0983</td>
      <td>135.0</td>
      <td>4.2021</td>
      <td>0.0</td>
      <td>1014.43</td>
      <td>Foggy starting overnight continuing until morn...</td>
    </tr>
    <tr>
      <th>299</th>
      <td>2006-04-20 11:00:00.000 +0200</td>
      <td>Partly Cloudy</td>
      <td>rain</td>
      <td>15.616667</td>
      <td>15.616667</td>
      <td>0.82</td>
      <td>2.2862</td>
      <td>153.0</td>
      <td>6.3112</td>
      <td>0.0</td>
      <td>1014.73</td>
      <td>Foggy starting overnight continuing until morn...</td>
    </tr>
  </tbody>
</table>
<p>300 rows × 12 columns</p>
</div>



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
