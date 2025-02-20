 # Лабораторная работа №1 

# Целью данной лабораторной работы является изучение основных принципов протокола HTTP.

# Условие
## Задание №1. Анализ HTTP-запросов

 Зайдите на сайт http://sandbox.usm.md/login.
 Откройте вкладку Network в инструментах разработчика браузера.
 Введите неверные данные для входа (например, username: student, password: studentpass).
 Проанализируйте запросы, которые были отправлены на сервер.

 # Ответьте на следующие вопросы:
### Какой метод HTTP был использован для отправки запроса?
Был использован метод POST
### Какие заголовки были отправлены в запросе?
 ```
POST /login/process.php HTTP/1.1
Host: sandbox.usm.md
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:130.0) Gecko/20100101 Firefox/130.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 37
Origin: http://sandbox.usm.md
Connection: keep-alive
Referer: http://sandbox.usm.md/login/###
```
Какие параметры были отправлены в запросе?
username=student&password=studentpass
### Какой код состояния был возвращен сервером?
Код состояния 401 (Unauthorized); попытка авторизации не удалась из-за неверных данных.
### Какие заголовки были отправлены в ответе?
```
HTTP/1.1 401 Unauthorized
Server: nginx/1.24.0 (Ubuntu)
Date: Thu, 19 Sep 2024 09:14:38 GMT
Content-Type: text/plain;charset=UTF-8
Transfer-Encoding: chunked
Connection: keep-alive#
```
Повторите шаги 3-5, введя верные данные для входа (username: admin, password: password).
### Какой метод HTTP был использован для отправки запроса?
Был использован метод POST
### Какие параметры были отправлены в запросе?
username=admin&password=password
### Какой код состояния был возвращен сервером?
Код состояния 200 (OK)
### Какие заголовки были отправлены в ответе?
```
HTTP/1.1 200 OK
Server: nginx/1.24.0 (Ubuntu)
Date: Thu, 19 Sep 2024 09:28:02 GMT
Content-Type: text/plain;charset=UTF-8
Transfer-Encoding: chunked
Connection: keep-alive###
```
Задание №2. Составление HTTP-запросов
## Составьте GET-запрос к серверу по адресу http://sandbox.com, указав в заголовке User-Agent ваше имя и фамилию.
```
GET / HTTP/1.1
Host: sandbox.com
User-Agent: Ivan Razdorojnii
```

## Составьте POST-запрос к серверу по адресу http://sandbox.com/cars, указав в теле запроса следующие параметры:
```
POST /cars HTTP/1.1
Host: http://sandbox.com
model=Corolla&make=Toyota&year=2020
```
## Составьте PUT-запрос к серверу по адресу http://sandbox.com/cars/1, указав в заголовке User-Agent ваше имя и фамилию, в заголовке Content-Type значение application/json и в теле запроса следующие параметры: json { "make": "Toyota", "model": "Corolla", "year": 2021 }
```
PUT /cars/1 HTTP/1.1
Host: sandbox.com
User-Agent:Ivan Razdorojnii
Content-Type: application/json

{
    "make": "Toyota",
    "model": "Corolla",
    "year": 2021
}
```
### Напишите один из возможных вариантов ответа сервера следующий запрос. http POST /cars HTTP/1.1 Host: sandbox.com Content-Type: application/json User-Agent: John Doe model=Corolla&make=Toyota&year=2020 Предположите ситуации, когда сервер может вернуть HTTP-коды состояния 200, 201, 400, 401, 403, 404, 500.
### 200 OK: Запрос успешно выполнен и данные обновлены или возвращены.
```
{
    "status": "success",
    "message": "Vehicle information retrieved successfully",
    "data": {
        "make": "Toyota",
        "model": "Corolla",
        "year": 2020
    }
}
```
### 201 Created: Новый ресурс был успешно создан.
```
{
    "status": "success",
    "message": "New vehicle created successfully",
    "data": {
        "make": "Toyota",
        "model": "Corolla",
        "year": 2020,
        "id": 123
    }
}
```

### 400 Bad Request: Неверный формат данных или отсутствуют обязательные параметры.
```
{
    "status": "error",
    "message": "Invalid request format. Expected JSON."
}
```
### 401 Unauthorized: Необходима аутентификация, но она не предоставлена или неверна.
```
{
    "status": "error",
    "message": "Unauthorized. Please provide valid credentials."
}
```
### 403 Forbidden: Аутентификация прошла успешно, но доступ к ресурсу ограничен.
```
{
    "status": "error",
    "message": "Forbidden. You do not have permission to perform this action."
}
```
### 404 Not Found: Ресурс не найден по указанному адресу.
```
{
    "status": "error",
    "message": "Not Found. The requested resource does not exist."
}
```
### 500 Internal Server Error: Произошла внутренняя ошибка сервера во время обработки запроса.
```
{
    "status": "error",
    "message": "Internal Server Error. Please try again later."
}
```
