# Конспект

1 Прохожение всех кодовых заданий
2 Изучение алгоритмов 
3 aký je rozdiel medzi UCS a A* algoritmom. 

## Цвик 1 

svc = SVC(kernel='linear')
- Линейное ядро это хорошо подходит для упорядоченных данных когда нет отклонений больших от линии тренда

X_train, X_test, y_train, y_test = train_test_split(
        faces.data, faces.target, test_size=0.25, random_state=0)
- Разделение датасета на часть для обучения и часть для тестирования чтобы тестировать модель не на тех строках датасета на которых мы ее учили

### Общий алгоритм для всех моделей
1 Получить датасет
2 Разделить на часть обучения и часть для тестирования x_train, x_test, y_train, y_test = train_test_split(X, y, test_size=0.25, random_state=0)
3 Инициализировать модель model = DecisionTreeClassifier()
4 Запредиктить тестовые данные y_pred = model.predict(x_test)
5 Посчитать точность предикта accuracy_score(y_test, y_pred)

DecisionTreeClassifier — это алгоритм машинного обучения, который строит дерево решений, чтобы классифицировать объекты.
Параметры такого дерева:
1 max_depth - чем меньше тем глупее модель
2 min_samples_split - чем меньше тем дерево глубже уходит чем больше тем дерево решений шире соответственно стабильнее

----

## Цвик 2

Работа с масивом данных  
titanic_data = pd.read_csv('data/titanic.txt')  
titanic_y = np.array(titanic_data.survived)  
- Получи все данные и целевую колонку

titanic_reduced = titanic_data.drop(columns=["row.names","survived","name","embarked", "home.dest","room", "ticket", "boat"])  
- удаление не нужных колонок

ages=titanic_reduced.iloc[:, 1]   # get age column  
ages=np.array(ages)   
- берем из второй колонки возраст 

mean_age = np.mean(ages[~np.isnan(ages)])  
- находим среднее

ages[np.isnan(ages)]=mean_age  
- всем возрастам со значение nan проставим средний возраст

titanic_reduced["age"]=ages  
- вставляем в таблицу (грубо говоря)

enc = LabelEncoder()  
label_encoder = enc.fit(titanic_reduced["sex"])  
integer_classes = label_encoder.transform(label_encoder.classes_)  
titanic_reduced["sex"] = label_encoder.transform(titanic_reduced["sex"])  
- находим DISTRICT у этой колонки тоесть все разные стати и соортируем по алфавиту

### Проблема с классом
- Так как число класса может быть от 1 до 3 включительно это целые 3 опции которые не воспринимаються моделью поэтому нужно разбить их на 3 колонки

class 1 | class 2 | class 3  
1 0 0  
0 1 0  
0 0 1

### Финал 2 Цвика:
Мы очистили и привели к адекватно виду датасет и может загрузить его в модель.  
X_train, X_test, y_train, y_test = train_test_split(titanic_reduced, titanic_y, test_size=0.25, random_state=33)

Далее Создаем класификатор  
clf = tree.DecisionTreeClassifier(criterion='entropy', max_depth=6, min_samples_leaf=10)

Дальше как обычно с этими данными мы может предиктить смертность

ДЗ 2 цвика

## Кластеризация

K-Means - делит данные на K групп  
elbow method - для выбора K  
Distortion - сумма квадратов расстояний всех точек до центров

## Кросс валидация
Разделение на K частей, каждая становится тестовой один раз.

## Выборка данных

VarianceThreshold — удаляет колонки без изменчивости.  
SelectFromModel + RandomForest — выбор важных признаков.  
RFECV — рекурсивное удаление признаков.

----

## Цвик 5

X, y = make_regression(1000, shuffle=True, random_state=None)  
- создаёт искусственный набор данных для регрессии.

## Алгоритмы Number puzzle 

BFS - поиск в ширину  
DFS - поиск в глубину  
Greedy search - выбирает ближайший шаг  
A* - Greedy + расстояние от начала

## Судоку 

Домена - множество возможных значений клетки.  
FC - удаляет невозможные значения, откат если пусто.  
MRV - выбираем клетку с минимальным количеством вариантов.  
LCV - значение, ограничивающее соседей меньше всего.

## Преднашки

Преднашка 7:  
Agent je entita, ktorá vníma a reaguje na zmeny v priestore pomocou senzorov a ovlyvňuje prostredie prostredníctvom akcií.
