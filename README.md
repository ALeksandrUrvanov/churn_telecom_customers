# Прогнозирование оттока клиентов из компании "Теледом"

Оператор связи «ТелеДом» хочет бороться с оттоком клиентов. Для этого будет предлагать промокоды и специальные условия всем, кто планирует отказаться от услуг связи. Чтобы заранее находить таких пользователей, «ТелеДому» нужна модель, которая будет предсказывать, разорвёт ли абонент договор. Команда оператора собрала персональные данные о некоторых клиентах, информацию об их тарифах и услугах.

## Задача:

Обучить на этих данных модель для прогноза оттока клиентов.

## Используемые библиотеки
- pandas
- numpy
- scipy
- sklearn
- matplotlib

## Отработанные методы и навыки:<br>

 - сгрузили таблицы с базы PostgreSQL; <br>
 - разобрали и проанализировали каждый столбец, имеющихся таблиц, поменяли названия согласно PEP-8;<br>
 - объединили таблицы в единий датафрейм;<br>
 - заполнили пропуски;<br>
 - удалили дубликаты;<br>
 - извлекли целевой признак;<br>
 - выбрали наиболее коррелируемые признаки;<br>
 - разделили данные на обучающую и тестовую, согласно заданию;<br>
 - провели кодирование категориальных признаков;<br>
 - масштабировали числовые признаки.<br>

 Во второй части обучили 7 моделей: LogisticRegression, RandomForestClassifier, LightGBM, CatBoostClassifier, AdaBoostClassifier, XGBClassifier, NeuralNetwork. Получили следующие показания метрики на обучающей выборке ROC-AUC:<br>
 
 - NeuralNetwork	        0.852864<br>
 - CatBoostClassifier	    0.848276<br>
 - LightGBM	              0.847483<br>
 - XGBClassifier	        0.846769<br>
 - AdaBoostClassifier	    0.846620<br>
 - RandomForestClassifier	0.839790<br>
 - LogisticRegression	    0.8362<br>

## Итоги проекта

NeuralNetwork опередила остальные модели. На тестовой выборке NeuralNetwork показала ROC-AUC: 0.85. Что удовлетворяет поставленным требованиям компании оператора связи. 

По полученному дополнительному анализу наблюдаем значительное увеличение новых абонентов, среди которых и идёт "текучка" абонентов. Самое большее количество, ушедших абонентов, это абоненты с общими раходами за весь период пользования услуг до 200 единиц с помесячной оплатой от 70 до 100 единиц. Т.е. в среднем 2 месяца пользования. У большинства из них была подключена услуга интернета по оптико-волокну. Можно предположить, что новые клиенты после подключения не довольны ценой или качеством интернета за данную сумму, при этом месячные платежи не минимальны, т.е клиенты с набором услуг.

Для оператора связи рекомендуется использовать модель NeuralNetwork для рассылки промокодов и специальных условий всем, кто планирует отказаться от услуг связи в течение 2 месяцев от заключения абонентского договора (True Positive, False Negative). Отправлять специальные предложения и промокоды целесообразно на электронный почтовый ящик, так как большинство ушедших получали электронные счета. Также рекомендуется добавить в таблицы данные о тарифах, что могло бы яснее понять причину оттока абонентов.


```python
