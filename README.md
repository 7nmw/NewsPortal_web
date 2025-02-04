## Новостной портал
Была использована база данных db.sqlite3


## Инструкции по установке
Используется Python 3.10.6

Установим Django: pip install django

Установим все библиотеки для работы приложения pip install -r requirements.txt

Запускаем приложение:
python manage.py runserver


## На данном портале реализованно следующее:
:white_check_mark: На портале выводятся все статьи и новости, в виде: заголовка, даты публикации и первых 20 символов текста.

:white_check_mark: Новости выводяться в порядке от более свежей к самой старой. Добавлен постраничный вывод на /news/, чтобы на одной странице было не больше 10 новостей и видны номера ближайших страниц, а также возможность перехода к первой или последней странице. 

:white_check_mark: Сделана отдельная страница для полной информации о новости и статье /news/<id новости>. На этой странице показана вся информация о статье. Название, текст и дата загрузки в формате день.месяц.год.

:white_check_mark: Есть собственный фильтр censor, который заменяет буквы нежелательных слов в заголовках и текстах статей на символ «*»

:white_check_mark: На странице /news/search реализована возможность искать новости по определённым критериям.

#### Авторизация и регистрация
:white_check_mark: Реализована возможность регистрации пользователей через почту или через Google-аккаунт.

:white_check_mark:Реализовано автоматическое добавление новых пользователей в группу common. Создана возможность стать автором (быть добавленным в группу authors).
Для группы authors предоставлены права создания и редактирования, удаления объектов модели Post (новостей и статей).

:white_check_mark: В классах-представлениях добавления и редактирования новостей и статей добавлена проверку прав доступа

#### Работа с асинхронными задачами через Celery
:white_check_mark: Добавлена возможность авторизованным пользователям подписываться на рассылку новых статей/новостей

:white_check_mark: Рассылка уведомлений подписчикам после создания статей/новостей

:white_check_mark: Еженедельная рассылка с последними новостями с гипперссылкой на них

:white_check_mark: Приветственное письмо пользователю при регистрации в приложении.

#### Локализация
:white_check_mark: Добавлен перевод заголовков в приложении с русского на английский язык

:white_check_mark: Добавлено переключение языка в шапке сайта

#### Кэширование
:white_check_mark: В шаблонах кэшируется все навигационные элементы (меню, сайдбары и т. д.).

:white_check_mark: Добавлено кэширование для статей.

#### Выполнена настройка логирования:
:white_check_mark: В консоль выводиться все сообщения уровня DEBUG и выше, включающие время, уровень сообщения, сообщения. Для сообщений WARNING и выше дополнительно выводиться путь к источнику события (используется аргумент pathname в форматировании). А для сообщений ERROR и CRITICAL еще выводить стэк ошибки (аргумент exc_info). Сюда попадают все сообщения с основного логгера django.

:white_check_mark: В файл general.log выводиться сообщения уровня INFO и выше только с указанием времени, уровня логирования, модуля, в котором возникло сообщение (аргумент module) и само сообщение. Сюда также попадают сообщения с регистратора django.

:white_check_mark: В файл errors.log выводиться сообщения только уровня ERROR и CRITICAL. В сообщении указывается время, уровень логирования, само сообщение, путь к источнику сообщения и стэк ошибки. В этот файл попадают сообщения только из логгеров django.request, django.server, django.template, django.db.backends.

:white_check_mark: В файл security.log попадают только сообщения, связанные с безопасностью, а значит только из логгера django.security. Формат вывода предполагает время, уровень логирования, модуль и сообщение.

:white_check_mark: На почту отправляются сообщения уровней ERROR и выше из django.request и django.server по формату, как в errors.log, но без стэка ошибок. Более того, при помощи фильтров указано, что в консоль сообщения отправляются только при DEBUG = True, а на почту и в файл general.log — только при DEBUG = False.

## Навигация по приложению

для входа в суперпользователь
логин admin
Пароль admin

sign — приложение регистрации, аутентификации и авторизации;
protect — приложение, в котором создается лишь одно представление для аутентифицированных пользователей

## URL страницы:

http://127.0.0.1:8000/admin/login/ # страница для админа

Базовая страница Инднтификации, с возможностью регистрации через Google-аккаунт
http://127.0.0.1:8000/ или http://127.0.0.1:8000/accounts/login/

http://127.0.0.1:8000/accounts/signup/ # Страница Регистрации

http://127.0.0.1:8000/news/  # Страница вывода всех новостей и статей

http://127.0.0.1:8000/news/create/ # Страница создания новости

http://127.0.0.1:8000/article/create/  # Страница создания статьи

http://127.0.0.1:8000/news/search/ # Страница поиска

http://127.0.0.1:8000/subscribe/post/ # Страница подписки на категории

http://127.0.0.1:8000/sign/logout/ # Страница после вызода из системы

http://127.0.0.1:8000/news/1/  # Страница с полной информацией о статье или новости

http://127.0.0.1:8000/news/int:pk/edit/  # Страница редактирования статьи/новости

http://127.0.0.1:8000/news/int:pk/delete/ # Страница удаления статьи/новости

## HTML шаблоны

Все шаблоны лежат в папке \templates

базовый шаблон, который расширяет все остальные шаблоны лежит по адресу:
templates/flatpages/default.html

В по адресу /static/css лежит готовые шаблоны с CSS-файлами для упрощения работы с HTML- и CSS-кодом

та самая страница, которая будет показываться только авторизованному пользователю protect/index.html.

В папке templates/sign можно найти три шаблона. signup.html, login.html и logout.html - для регистрации, входа и выхода соответсвенно.



