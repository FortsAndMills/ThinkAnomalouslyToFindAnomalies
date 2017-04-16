"Хотите удивительную историю? Маленького Сашу отец часто посылал в магазин за мандаринами - давал ему пару сотен рублей, а маленький Саша возвращался с мандаринами и сдачей. Как-то раз отец что-то перепутал, и вместо ста рублей выдал сто индонезийских рупий. Ну всякое бывает, спросите вы, что ж тут удивительного. А вот что: маленький Саша сразу же понял, что тут что-то не так!!!"

13.02.17 - 18.02.17
[Статья по Isolation Forest](http://cs.nju.edu.cn/zhouzh/zhouzh.files/publication/icdm08b.pdf)
Isolation Forest круче всех. Основные соображения вынесены в работу. [Проведено знакомство с алгоритмом на уровне "аааа я хочу его повернуть!"](http://nbviewer.jupyter.org/github/FortsAndMills/ThinkAnomalouslyToFindAnomalies/blob/master/Isolation%20Forest%20First%20Look.ipynb)

21.02.17
Updated (постановка задачи)

25.02.17
Updated (постановка задачи и ещё пара меток)
Сразу по нескольким причинам заинтересовался решением этой задачи в одномерном случае, рассуждения вынесены в ноутбук.

26.02.17
Ноутбук [выложил](http://nbviewer.jupyter.org/github/FortsAndMills/ThinkAnomalouslyToFindAnomalies/blob/master/1D%20Anomaly%20Detection.ipynb). При прочтении желательно находиться подальше от автора и тяжёлых предметов, в конце концов, у меня были праздники.

05.03.17
Кое-кто спамил меня [интереснейшими ссылками](https://www.codingame.com/contests/ghost-in-the-cell), я не сдержался и неделю гамал.
Код не выкладываю, он всё равно не работает((((

Предстоящая задача - структурировать имеющуюся информацию...

11.03.17
Попытка структуризации проведена, текущая версия работы выложена. Кажется, я забыл выложить пару ссылок на пару страниц по теме, которые я надеюсь смочь прочитать, ну ладно. Из нового добавилось пара малосодержательных соображений по вероятностным методам и список интересных и не очень методов, первые из которых подлежат дальнейшему хотя бы краткому исследованию.

Дневник подвергнут стрижке.

19.03.17
Всё проапдейчено, основное изменение - немного мыслей про линейные методы в целом и PCA, ничего сильно интересного.
Начал структурировать имеющийся код в модуль для проведения экспериментов, чтоб функции ручками и классы полочками. Пока всё в ноутбуке, а не в пай-модуле (вопрос, как это правильно оформлять, я левой рукой отмахиваю на потом), ну да не суть. Для модифицированного iForest-а внедрил хитрость с QR-разложением, теперь его можно юзать в многомерных пространствах.

Для теста в том же файле решил загрузить один из датасетов, которые, как я понимаю, часто используются для этой задачи - [sattelite](https://archive.ics.uci.edu/ml/datasets/Statlog+(Landsat+Satellite)). iForest выдал мне некие скоры для теста. Теоретически самое максимальное, что можно получить по f-мере, двигая как-то порог классическим образом - 0.6212. Главное достижение - смог угадать правильный сплит в алгоритме деления в прорезях, причём с неожиданным результатом - 0.6231. Это он просто ещё объекты с очень хорошими скорами объявил аномалиями. "Слишком хорошими", видимо. Единственное, что использовалось - это информация о том, что аномалий примерно треть в датасете.

26.03.17 апдейтнул несколькими соображениями, рандомно посещавшими меня в течении недели... Про датасеты. Решил сразу их хоть как-то с применением того, что есть, описать и сразу же столкнулся с несколькими непредвиденными и интересными фактами, которые ещё предстоит разрешить. Также доделан до работоспособного вида экспериментальный модуль.

29.03.17 не зашло, поэтому даже код выкладывать не буду: попробовал свой этот "морфологический спектр" в нескольких разных видах. Заодно заценил, как не работают классические традиционные алгоритмы поиска аномалий - "пятый сосед!", "десятый сосед", "среднее по первым десяти соседям!", etc. Вариации вроде случайного выбора пар даже не стал пробовать.

01.04.17 Попробовал "умную проекцию" - так отобразить точки пространства на прямую, чтобы как можно лучше сохранялись расстояния между ними. Узнал много нового - оказывается, это такое зеркальное отражение PCA, только в PCA надо у ![](https://latex.codecogs.com/gif.latex?X%5E%7BT%7DX) искать собственные значения/вектора, а тут - у ![](https://latex.codecogs.com/gif.latex?1%20/_%7Bentrywise%7D%20X%5E%7BT%7DX). Нифига не работает. В общем, все старые затеи не работают, нужны новые. И тут на сцене появляется... ладно, пока не буду спойлерить.

02.04.17 Обновил датасеты и поигрался с имеющимися возможностями, в том числе проверил полиномиальный способ с сэмплированием (о\_o, нужно срочно придумывать красивое название). Он, кстати, даже работает. Обновил модуль для экспериментов новым способом.

09.04.17 Выложил опробованный на неделе мод леса с неравномерным выбором признаков. Пришлось копаться в скайлёрновском коде и своей лабе по машинному обучению за тот семестр (угадайте, в каком коде разбираться пришлось дольше...), но зато я убедился, что и эта штука не работает! Идея заключалась в том, чтобы выбирать с вероятностью, пропорциональной его потенциальной хорошести) не только разрез, но и признаки, а в качестве меры хорошести выступала дисперсия нормированных на единицу разниц отсортированного признака (так, признак, у которого все значения равны, будет иметь вероятность выбора 1, что логично). Возможно, ещё стоит проверить пару вариаций, но в целом работает не лучше оригинала, а линейность алгоритма теряется.

16.04.17 Убраться не получилось, поэтому помусорил: небольшие update-ы в виде заметок по ряду моментов и проверка пары идей в экспериментальном модуле.
