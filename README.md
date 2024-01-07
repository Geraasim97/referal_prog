# referral_prog
Дипломный проект курса

Сервис авторизации по номеру телефона(TB4)


Проект представляет собой DRF систему авторизации по номеру телефона, 
дополненную функциональностью реферальной программы. 
Он включает в себя отправку и проверку смс-кодов, создание и использование реферальных кодов, 
начисление бонусных баллов, а также работу с пользовательскими профилями.


Функционал

- генерация и отправка смс-кода авторизации на номер телефона пользователя
- авторизация пользователя по номеру телефона
- регистрация новых пользователей в базе данных
- генерация уникального реферального кода для каждого нового пользователя
- возможность активировать чужой реферальный код в профиле пользователя
- просмотр профиля пользователя со списка его рефералов
- редактирование профиля пользователя
- начисление бонусных баллов участникам реферальной программы:
  - приглашенный - активировал "Реферальный код пригласителя" в своем профиле +100 баллов
  - пригласитель - за каждого приглашенного по его коду +200 баллов
-  web-интерфейс для тестирования приложения: http://185.173.162.105:8000/users/web/auth/send_sms/


Стек Технологий:

- Python
- Django, Django REST Framework (DRF)
- PostgreSQL
- Twilio
- Docker


Установка и Запуск

1. Заполнить файл .env своими данными (на примере файла .env.sample)
2. Установить Docker и Docker compose
3. Запустить команду: docker-compose up -d --build


Использование API проекта

Авторизация:
1. Отправка смс-кода на указанный пользователем номер телефона

Endpoint: POST http://185.173.162.105:8000/users/auth/send_sms/

Body: json
{
  "phone_number": "+71234567890"
}

2. Подтверждение полученного SMS-кода для завершения процесса авторизации

Endpoint: POST http://185.173.162.105:8000/users/auth/verify_sms/

Body: json
{
  "phone_number": "+71234567890",
  "sms_code": "1234"
}


Работа с Профилем:
1. Получение профиля авторизованного пользователя(со всеми данными реферальной программы)

Endpoint: GET http://185.173.162.105:8000/users/profile/

Headers: Authorization: Bearer <access_token>

2. Активация реферального кода пригласителя (и одновременное начисление реф. баллов приглашенному и пригласителю)

Endpoint: PATCH http://185.173.162.105:8000/users/profile/update/

Headers: Authorization: Bearer <access_token>

Body:
{
  "inviter_referral_code": "ABcDeF"
}

3. Обновление профиля пользователя

Endpoint: PATCH http://185.173.162.105:8000/users/profile/update/

Headers: Authorization: Bearer <access_token>

Body:
{
  "first_name": "Test",
  "last_name": "Testov",
  "email": "testov@gmail.com",
}


Документация API

http://185.173.162.105:8000/docs/  - Swagger

http://185.173.162.105:8000/redoc/  - Redoc