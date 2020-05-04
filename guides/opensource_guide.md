# Правила создания и поддержки opensource-проектов в BestDoctor

## Мотиваций

Сейчас на <https://github.com/best-doctor/> 20+ проектов в разной
стадии разработки. Мы хотим поддерживать их в нормальном состоянии, чтобы
приносить больше пользы сообществу и самим себе.

В этом гайде собраны правила, которых мы стараемся придерживаться при разработке
и сопровождении наших opensource-проектов и процесс этого сопровождения.

## Процесс сопровождения

Основной элемент сопровождения – еженедельный чек проектов по этому гайду.
На это выделяется 1-2 часа в неделю, чтобы найти новые поломки, ответить на
вопросы в issues, сделать ревью пул-реквестов, обновить зависимости,
зачинить билды. Этот процесс нужен не для развития проектов, а для их
поддержки. Основных целей у этого процесса две: минимизировать количество
критичных нарушений этого гайда и максимизировать количество проектов,
которые полностью ему соответствуют.

Проверять проекты на соответствие гайду руками – муторное и неблагодарное
занятие, поэтому в наших кузницах уже разрабатывается `opensource_watchman`
– скрипт, который делает всё сам и показывает список нарушений по каждому
проекту. Скоро он будет готов и ссылка на него будет тут.

Развитие проектов – то, к чему может присоединиться кто угодно, в том числе мы.
Для этого у нас есть открытые задачи, понятные гайды, CI и правила участия
в проектах.

## Язык проекта

Основной язык всех проектов – английский. Он используется везде: в текстах
коммитов, комментариях, задачах, при общении в пул-реквестах и в документации.

Это нужно, чтобы наши проекты могли принести пользу максимальному
количеству людей.

Исключений может быть два. Первое – репозитории с текстовой информацией, а не
кодом (например, этот репо). Такие проекты могут быть на русском. Второе –
проекты, актуальные только для русского языка. Пример такого проекта
(извне BestDoctor, правда) – это
<https://github.com/Melevir/rozental_as_a_service>. Он работает только с русским
языком и его основной язык – русский.

Если проект на русском, стоит подумать о его переезда на английский полностью
или поддержки нескольких языков с процессом актуализации переводов.

## Ридми и документация

У каждого проекта должен быть ридми с исчерпывающей информацией: что это,
зачем оно нужно, как работает, как установить, как запустить,
что для этого нужно, пример использования, как сделать вклад в проект.

Для унификации основной ридми должен лежать в корне проекта и
называться `README.md`.

Ридми и другая документация должна валидироваться с помощью `mdl`.

В ридми должны быть бейджики со статусом билда и процентом покрытия
кода тестами. Остальные бейджики можно не добавлять.

## Поддерживаемые версии языков

Мы стараемся использовать в opensource-проектах те же технологии, которые
используем в бою.

Вне зависимости от выбранного языка, наши проекты должны поддерживать
минимум две последние минорные версии языка.

## CI и сторонние сервисы

Для унификации мы используем Travis CI для, собственно, CI и Codeclimate
для дополнительного статического анализа и подсчёта покрытия тестами.

В Тревисе должна быть настроена основная таска, которая запускается на пуш
и прогоняет все проверки (стиль кода, типизация, тесты, mdl,
safety и все-все-все) и тесты. Если билд зелёный – значит, все
проверки проходят.

Кроме этого в Тревисе стоит настроить еженедельную крон-джобу, которая делает
всё то же, но без коммита. Это позволяет вовремя отловить обратно несовместимые
обновления незамороженных зависимостей, найденные новые CVE и прочие ништяки,
о которых хорошо бы знать как можно раньше.

## Безопасность и зависимости

Мы заботимся о том, чтобы наш код не наносил вреда и чтобы с его помощью
нельзя было нанести вред. Для этого мы действуем по двум направлениям:
следим за нашим кодом и за нашими зависимостями.

В нашем коде мы стараемся не допускать распространённых ошибок, связанных с
безопасностью. Для хоть какой-то автоматической проверки этого в коде на
Python мы используем dlint.

Для мониторинга обновлений безопасности в наших зависимостях на Python
мы используем safety. Он должен быть в билде на пуш и, что самое важное,
еженедельном билде. Если найдётся уязвимость в одной из зависимостей,
сломается еженедельный билд и мы об этом узнаем.

## Версионирование

Во всех проектах используем
[семантическое версионирование](https://semver.org/lang/ru/).

## Политика релизов

Код может лежать на Гитхабе, но не быть зарелижен, не больше 2 недель.

Важно понимать, что 2 недели – это допустимый, но не желательный срок.
В идеале код отправляется в релиз сразу после пуша. У нас тут ZDD или как?

## Правило последнего коммита

Последний коммит в любой проект должен быть меньше, чем 6 месяцев назад.
За это время точно что-то произошло даже если проекта не дорабатывается:
приехала новая версия языка, обновились зависимости или наши требования
к нашим проектам.

Если мы не планируем дорабатывать проект, это нужно сделать явным:
написать дисклеймер в ридми и заархивировать проекта на Гитхабе.

## Покрытие кода тестами

Минимальное покрытие кода тестами должно составлять 80%.

Это важно не только для устойчивой дальнейшей разработки проекта, но и для
уверенности в проекте тех, кто только решает, использовать ли его.

Тесты должны гоняться в билде, иначе от них почти нет смысла.

Для достижения этой цели мы используем и юнит-тесты и интеграционные.

## Работа с задачами

У каждого проекта должно быть 3+ открытых актуальных задачи.
Это нужно, чтобы помочь сделать вклад в проект тем, кто этого хочет.

На свежесозданные задачи мы отвечаем в течение 14 дней.
Нет ничего хуже проекта, мейнтейнер которого не обрабатывает задачи.

## Работа с пул-реквестами

Все входящие пул-реквесты обрабатываем за 7 дней: делаем ревью и просим
доработать или мерджим. Желательно быстрее: если кто-то сделал пул-реквест,
нам важно сделать его опыт взаимодействия с мейнтейнером как можно более
быстрым.