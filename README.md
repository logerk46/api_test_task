# api_test_task
Взять любой знающий фреймворк yii/laravel/symfony/silex и сделать простое приложение которое будет получить запросы по API и отправлять письмо на почту по шаблоны, так же сделать авторизацию по api токену. Почту, куда отправлять почту необходимо указать в конфигурационном файле фреймворка.


Есть  роут (url)
POST /api/v1/{event}

{event} - это название события, например new_order, new transaction, new_message возьмем пока-что только new_order

Входящие параметр только один, это номер заказа  ну и токен api_token, его можно передавать в теле запроса или же в Header как Bearer

Например:
{“order”: 1, “api_token”: “...”}

каждое событие имеет свой шаблон (простая кусок текста с переменными), в который подставляются данные из запроса, в нашем случае это значение order.

Шаблон
Поступил новый заказ №{$order}.
Ссылка на заказ http://example.com/order/view/{$order}

При запросе на URL
POST http://sender.example.com/api/v1/new_order

Тело запроса
{“order”: 258, “api_token”: “....”}

Письмо которое будет выслано на почту будет иметь вид
Поступил новый заказ №258.
Ссылка на заказ https://crm.example.com/order/view/258



но заложить механизм таким образом, что-бы мы могли создавать еще события которые нам будут нужны в будущем, и они также будут иметь свои шаблоны и свой набор обязательных данных. 



Например событие new_transaction
Должно иметь два параметра {card} и {amount}

Результат на почту не отправляем, а просто пишем в лог файл. 

Формат
To: email из конфига
Subject: Событие  {$event}
Body: текст сообщения


логи, что все работает
![Screenshot](Screenshot_1.png)
