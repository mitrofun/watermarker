Watermarker
==========
Watermarker - это тулза для легкого, почти ванильного создания водяных знаков на картинках. Вносит в проект одну модель и шаблонный тег  

## Подключение к проекту
Как сабмодуль:    
```git submodule add https://bitbucket.org/dvebukvy/watermarker```
  
## Настройка  
Добавляем приложение в `INSTALLED_APPS`:  

    INSTALLED_APPS = (
        ...
        'watermarker',
        ...
    )

Для создания таблицы в БД выполняем команду `./manage.py syncdb`

## WorkFlow  
В панели администратора появляется модель Watermrks. Заходим создаем новый объект, заполняем.  
Маленькие особенности:  
    1. Заголовок (Title) набираем по-английски, он нам понадобится позже.  
    2. Если в графе Позиция (Position) выбрать кастомные координаты и не ввести их, то водяной знак появится в точке (0,0)  
    3. В штатном режиме либа не перерисовывает уже созданные ватермарки. Но если очень хочется или поменялись настройки отображения знака, то
        пункт Update hard вам поможет. Если он установлен в True, то при рендеринге страницы будут всегда перерисовываться ватермарки.
        Не забудьте снять флаг после применнеия изменений, ибо производительность.
    4. Графа Is active работает как обычно. Это способ в один клин отключить ватермарку

Водяные знаки накладываются в шаблонах. 
Импортируем:  
    ```{% load watermarks %}```  
B в нужном мете пользуемся фильтром:  
    ````<img src="{{ house.image.url|watermark:'wm_title' }}" alt="{{ house }}"/>```
    `wm_title` - имя для ватермарка, которое писали в графу Заголоваок в админке.
Должно работать с различными обрезалками:  
    ``` <img src="{% thumbnail image.image|watermark:'wm_title' 160 110 crop=1 %}" alt=""/></a>```

## Требования
Для нормального функционирования требуется PIL и вся толпа пакетов для него. 

## Косяк
По неведомым причинам пока не ставятся ватермарки на изображения с кириллическими именами, sorry :(
