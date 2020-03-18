# Пример использования API календаря в PHP #

[日本 (日本語)](https://github.com/jasonjoh/php-calendar/blob/master/loc/readme-ja.md) (японский)

Использование [API календаря](https://msdn.microsoft.com/office/office365/APi/calendar-rest-operations) из PHP показано на примере приложения с ближайшими показами шекспировского фестиваля вымышленного театра. Пользователь может подключить свою учетную запись Office 365 и добавлять в свой календарь показы, которые планирует посетить. Пользователь может приглашать друзей. При этом им будут отправляться приглашения на собрание. 

## Используемые функции API ##

- Создание событий в календаре пользователя по умолчанию
- Добавление вложений
- Добавление участников
- Использование [представления календаря](https://msdn.microsoft.com/office/office365/APi/calendar-rest-operations#GetCalendarView) для развертывания повторяющихся событий и отображения всех встреч для одного дня.

## Необходимое программное обеспечение ##

- [PHP 5.6](http://php.net/downloads.php)
- Веб-сервер, способный обслуживать PHP.

В ходе тестирования я использовал IIS 8, установленный на ноутбуке с Windows 8.1. Я установил PHP 5.6.0, используя [ установщик веб-платформы](http://www.microsoft.com/web/downloads/platform.aspx) (только для Windows/IIS).

## Запуск приложения ##

Предполагается, что перед запуском вы установили PHP, и ваш веб-сервер настроен на обработку и обслуживание PHP-файлов. 

1. Скачайте проект приложения или создайте вилку.
1. Создайте каталог в корневом каталоге документов с именем `php-calendar`. Скопируйте файлы из репозитория в этот каталог.
1. [Зарегистрируйте приложение в Azure Active Directory](https://github.com/jasonjoh/office365-azure-guides/blob/master/RegisterAnAppInAzure.md). Зарегистрируйте приложение как веб-приложение с URL-адресом входа `http://localhost/php-calendar` и предоставьте ему разрешение "Полный доступ к календарям пользователей", которое доступно в раскрывающемся списке "Делегированные разрешения".
1. Измените файл `.\o365\ClientReg.php`. 
	1. Скопируйте идентификатор клиента, полученный при регистрации приложения, и вставьте его в качестве значения переменной `$clientId`. 
	1. Скопируйте ключ, созданный во время регистрации приложения, и вставьте его в качестве значения переменной `$clientSecret`.
	1. Сохраните файл.
1. Если установка PHP не использует обновленные сертификаты ЦС для проверки SSL, запросы не будут выполняться, если вы не запустите Fiddler на сервере и не присвоите переменной `$enableFiddler` значение `true` в `Office365Service.php`. Кроме того, вы можете вставить следующую строку перед всеми вызовами `curl_exec`. **Однако** помните, что при этом отключается проверка SSL, что НЕДОПУСТИМО в промышленном коде.

    curl\_setopt($curl, CURLOPT\_SSL\_VERIFYPEER, 0);
1. Откройте веб-браузер и перейдите в `http://localhost/php-calendar/home.php`.
1. Вы увидите список предстоящих показов различных пьес Шекспира. Нажмите любую кнопку "Подключить мой календарь", чтобы войти в Office 365.
1. После входа вы будете перенаправлены на домашнюю страницу, и теперь кнопки будут иметь надпись "Добавить в календарь". Нажмите кнопку рядом с показом, чтобы добавить его в свой календарь. К событиям со значением "Да" в поле "Ваучер обязателен" будет прикреплен ваучер.

## Авторское право ##

(c) Корпорация Майкрософт (Microsoft Corporation). Все права защищены.

----------
Работайте со мной на сайте Twitter [@JasonJohMSFT](https://twitter.com/JasonJohMSFT)

Следуйте инструкциям в [блоге разработчиков Exchange](http://blogs.msdn.com/b/exchangedev/)