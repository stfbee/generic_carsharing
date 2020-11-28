## Как заставить проект собираться?

1. Создай акк на мапбоксе и сгенерируй секретный токен
2. В `~/.gradle/gradle.properties` (если его нет, то создай) добавь строку `MAPBOX_DOWNLOADS_TOKEN="sk......"` с твоим секретным токеном
3. Поскольку описанный выше принцип не работает, то просто скопипасть твой ключ в корневой `build.gradle`, найдешь куда. Только не коммить (как я, кек)! 

Фотки машин ~~берутся~~ брались отсюда: `https://loremflickr.com/300/200/car`

## Заметки

Выкачать рекомендованную версию `5.9.0` не вышло "просто потому что", хз. Видимо, она либо в другом мавен-репозитории, либо вообще удалена оттуда

Потратил некоторое время на попытки кластеризации, но чот оно начало падать с `A/libc: Fatal signal 6 (SIGABRT), code -1 (SI_QUEUE)`, да и не надо оно по тз

Так же пробовал сделать маркеры через плагин, так как `IconFactory` задеприкейчен с `7.0.0`, но раз уж в рекомендациях было использование `5.9.0`, то я и забил. 
Я не понял, как там брать иконки из ресурсов, да и вообще там похоже большие ограничения на работу с маркерами, раз в примере юзается класс прослойка для добавления
и убирания с карты маркеров с кастомной иконкой (которые на самом деле `ImageView`)
 
Еще в приложении можно включить поворот машин, я нашел 3 способа:
 - рисовать иконки через стили и слои (см заметку №1)
 - задать угол в плагине (см заметку №2)
 - генерить битмапы из ресурсов и вращать их (с кешем)
Сделал третий способ, но т.к. это битмапы, там жрется память (ну хоть не течет). Можно включить в App.kt и посмотреть в профайлере

Кеш сделан чисто средствами хттп-клиента и глайда, можно было бы запилить лру (который и так юзается в OkHttp, это же поделия Вортона) или даже бд, но это долго, да и не надо
Из-за того, что адрес у фоток был одинаков, глайд (и пикассо тоже, я тестил) с разными политиками кеша либо кешируют одну и ту же фотку, либо не кешируют их вообще, поэтому
я пришел к использованию фоток с сайта белки. Но там белый фон и все ломается в ночной теме :(