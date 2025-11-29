# Учебные заметки

## 1. Прохождение всех кодовых заданий

## 2. Изучение алгоритмов

## 3. Aký je rozdiel medzi UCS a A\* algoritmom?

------------------------------------------------------------------------

# Цвик 1

``` python
svc = SVC(kernel='linear')
```

**Комментарий:** линейное ядро хорошо подходит для данных, которые
примерно разделимы прямой линией и не имеют сильных отклонений от
линейного тренда.

``` python
X_train, X_test, y_train, y_test = train_test_split(
    faces.data, faces.target, test_size=0.25, random_state=0
)
```

**Комментарий:** датасет делится на обучающую и тестовую части, чтобы
модель проверялась не на тех данных, на которых обучалась.

------------------------------------------------------------------------

## Общий алгоритм для всех моделей

1.  Получить датасет.\

2.  Разделить данные на обучающую и тестовую выборки

    ``` python
    X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.25, random_state=0)
    ```

3.  Инициализировать модель

    ``` python
    model = DecisionTreeClassifier()
    ```

4.  Выполнить предсказание

    ``` python
    y_pred = model.predict(X_test)
    ```

5.  Посчитать точность

    ``` python
    accuracy_score(y_test, y_pred)
    ```

------------------------------------------------------------------------

## DecisionTreeClassifier

Алгоритм машинного обучения, который строит дерево решений для
классификации объектов.

Основные параметры:

-   **max_depth** --- максимальная глубина дерева. Чем меньше глубина,
    тем проще модель.\
-   **min_samples_split** --- минимальное количество образцов для
    разбиения. Чем больше значение, тем шире и стабильнее дерево.

------------------------------------------------------------------------

# Цвик 2

Работа с массивом данных:

``` python
titanic_data = pd.read_csv('data/titanic.txt')
titanic_y = np.array(titanic_data.survived)
```

--- получаем таблицу и целевую колонку.

``` python
titanic_reduced = titanic_data.drop(columns=[
    "row.names","survived","name","embarked",
    "home.dest","room", "ticket", "boat"
])
```

--- удаляем ненужные колонки.

``` python
ages = titanic_reduced.iloc[:, 1]
ages = np.array(ages)
```

--- берём колонку возраста.

``` python
mean_age = np.mean(ages[~np.isnan(ages)])
```

--- находим средний возраст среди существующих значений.

``` python
ages[np.isnan(ages)] = mean_age
```

--- заменяем пропущенные значения средним возрастом.

``` python
titanic_reduced["age"] = ages
```

--- вставляем обновлённый столбец обратно в таблицу.

------------------------------------------------------------------------

### Кодировка категориальных признаков

``` python
enc = LabelEncoder()
label_encoder = enc.fit(titanic_reduced["sex"])
integer_classes = label_encoder.transform(label_encoder.classes_)
titanic_reduced["sex"] = label_encoder.transform(titanic_reduced["sex"])
```

--- находим все уникальные категории пола, сортируем их и заменяем
строковые значения числовыми метками.
