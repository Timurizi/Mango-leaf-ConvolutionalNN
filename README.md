# Mango-leaf-ConvolutionalNN (ссылка на датасет - https://www.kaggle.com/datasets/warcoder/mango-leaf-disease-dataset)
В рамках проекта по теории нейросетевых обучений я выбрал конструирование свёрточной нейронной сети и ее использование. Задача: по фотографии листочка дерева манго определить болезнь дерева 
В данном Notebook я использовал Keras в качестве основного инструмента. Сначала я разделил наш датасет на train-test-val в пропорции 3-1-1 - это базовый первый шаг, затем создаем с этими папками объекты типа image_dataset_from_directory из кераса и очень важно присвоить  метку label_mode='categorical' тк мы решаем задачу не бинарной классификации.
Далее шёл долгий подбор самой структуры нейронки и спустя большое колличество тестов я пришёл к выводу, что следующая структура является наиболее оптимальной
![image](https://github.com/Timurizi/Mango-leaf-ConvolutionalNN/assets/75172935/94882045-6903-4740-886c-fbb0a2c21ce0)

Приступим к обучению в 30 эпох. 
![image](https://github.com/Timurizi/Mango-leaf-ConvolutionalNN/assets/75172935/e9877c22-5f7b-46ff-a0dd-ce5eb8d63895)

По результатам мы имеем достаточно неплохую точность модели. Отследим как она менялась с каждой эпохой на графике matplotlib
![image](https://github.com/Timurizi/Mango-leaf-ConvolutionalNN/assets/75172935/2afa107c-2c4d-432c-a7a8-81d3629413aa)

У нас не возникло переобучения , что уже хорошо и итоговая точность +- 95% всего за 30 эпох. Попробуем её увеличить посредством аугментации данных.
![image](https://github.com/Timurizi/Mango-leaf-ConvolutionalNN/assets/75172935/13ea15c2-5069-4b57-a191-32270d6d492f)

Добавляем к нашей обучающей выборке определенным образом видоизменённые картинки (рандомный угол поворота, рандомное значение мультипликатора приближения картинки)
И пробуем её обучить c нуля и посмотреть на точность за то же колличество эпох.

![image](https://github.com/Timurizi/Mango-leaf-ConvolutionalNN/assets/75172935/9f9f1f4f-f4f9-4a61-a14f-b8223a4db70a)

Как можно заметить мы выиграли аж 2 %. Конечно в идеале было бы запустить 100 эпох обучения и посмотреть на общий вывод, но я не обладаю такими производственными мощностями и моя сессия collab просто обнуляется :(

А как будет работать уже  модель VGG16 ? Попробуем её обучить и посмотреть на результат
![image](https://github.com/Timurizi/Mango-leaf-ConvolutionalNN/assets/75172935/1864ade3-5dd0-4ac2-b947-c27adb28a95f)

![image](https://github.com/Timurizi/Mango-leaf-ConvolutionalNN/assets/75172935/5f1e1db0-9ab3-469d-8a89-1af648e5b4fa)

Посмотрим на результат нашей нейронки на этих эпохах:
![image](https://github.com/Timurizi/Mango-leaf-ConvolutionalNN/assets/75172935/68767f90-5b15-4fd9-b705-5b811b076fb3)


По сравнению с индивидуально подобранной моделью результат у вгг16  проигрывает аж на 10 %.
Итог: С помощью сверточных нейронных сетей была с неплохой точностью, с учетом производственных мощностей решена задача классификации листочков манго. Также для чистоты эксперимента была взята уже сконструированная модель VGG16 , которая проигрывает в точности на 10%
Также были использованы методы аугментации данных для улучшения точности , подборка гиперпараметров(как размер ядра у макспулинга и тд)  дефолтный параметр learning_rate у Adam достаточно неплохо справлялся, поэтому я решил его оставитью
