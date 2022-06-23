Инструкция к запуску файлов

1. Файл DatasetCreating для формирования датасета:

- скопировать/переместить 1 картинку (больше не позволяет объем ОЗУ в Collab) из папки DatasetCreating/all\_images и соответствующую ей маску из папки DatasetCreating/all\_masks в папки current\_image и current\_mask;
- в ячейке <span style="color:green">random choice of necessary amount of images</span> задать параметр <span style="color:red">len</span> как наибольшее возможное количество черно-белых изображений (см. вывод параметра <span style="color:red">wb</span> в ячейке <span style="color:green">class balancing</span> выше). Полученные картинки сохраняются в соответствующих папках в DatasetCreating/datasets;
- если будет необходимость раздробить несколько картинок, то нужно удалить картинку и маску из папок current\_, добавить новые, перезапустить код и в ячейках <span style="color:green">saving train images</span> и <span style="color:green">saving val images</span> поменять <span style="color:red">n</span> и <span style="color:red">m</span> с 0 на уже сохраненное количество картинок в соответствующих папках.

2. Файл Learning для обучения модели запускать с GPU:

- запустить весь файл, выставив количество эпох <span style="color:red">num\_epochs</span> в ячейке вызова модели (первая эпоха может обучаться до 1-1.5 часов из-за считывания файлов с гугл-диска, остальные эпохи проходят примерно за 2.5-3 минуты);
- сохраненные веса можно найти в папке TyurinaAV\_segmentation/Learning;

3. Файл Test для предсказания масок на тестовом датасете запускать с GPU:

- в ячейке <span style="color:green">loading images and masks</span> выбрать нужную тестовую картинку и маску с названиями \_A0, …, \_B3;
- в ячейке <span style="color:green">dataset creating</span> установить размер пакета <span style="color:red">batch\_size</span> в соответствии с таблицей:

|Имя файла|batch\_size|n\_crops|org\_img\_size|
| :-: | :-: | :-: | :-: |
|A0|35|1155|8558, 9163|
|A1|37|1221|8605, 9562|
|A2|35|1085|8099, 9163|
|B0|37|1258|8769, 9562|
|B1|34|1054|8004, 8764|
|B2|34|1054|8166, 8764|
|B3|34|1020|7758, 8764|

- в ячейке <span style="color:green">restoring predicted mask</span> установить <span style="color:red">n\_crops</span> в соответствии с таблицей;
- в ячейке <span style="color:green">saving predicted mask</span> установить <span style="color:red">org\_img\_size</span> в соответствии с таблицей;
- предсказанную маску можно увидеть в блокноте или в папке Test/.

