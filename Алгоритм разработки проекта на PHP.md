# Алгоритм разработки проекта на PHP
(решил создавать этот алгоритм одновременно с выполнением работы над этим проектом, чтобы не писать лишних инструкций - все по делу)
<a name="user-content-start"></a>

<!-- MarkdownTOC -->

- [Структура проекта на PHP](#user-content-Структура-проекта-на-php)
- [Название проекта директория проекта](#user-content-Название-проекта-директория-проекта)
- [Первый файл в проекте](#user-content-Первый-файл-в-проекте)
- [Первая фиксация коммит в .git и GitHub](#user-content-Первая-фиксация-коммит-в-git-и-github)
- [Создание локального виртуального хоста](#user-content-Создание-локального-виртуального-хоста)

<!-- /MarkdownTOC -->

<a id="user-content-Структура-проекта-на-php"></a>
## Структура проекта на PHP

    ProjectName/
        ../
            .logs/                  // Каталог логов
            .PROJECT/               // Каталог служебных файлов (скрытый)
            SANDBOX/                // Каталог "песочница"             
                public/             // Рабочий каталог, "точка входа" доступная из сети
                    .gitignore
                    .htaccess
                    index.html      // пробный index-файл html
                    index.php       // пробный index-файл php
                    README.md
                README
            .gitignore
            ThisProject.todo

[в начало](#user-content-start)

<a id="user-content-Название-проекта-директория-проекта"></a>
## Название проекта директория проекта
Название (директория проекта) указывается одним словом в Camel-стиле и описывает самые общие черты проекта.   
Например:

    LandingPageBS4PHP7
    (что делаем, на каком фреймворке, на каком языке)

[в начало](#user-content-start)

<a id="user-content-Первый-файл-в-проекте"></a>
## Первый файл в проекте
ThisProject.todo - это файл описания идей, реализаций и вообще всех текущих и будущих действий при работе над проектом.     
Файл создан в формате .todo для Sublime Text 3 (плагин Plain Tasks).  
Файл ThisProject.todo содержит следующие основные разделы:

    ThisProject.todo
    Файл служебного описания проекта и ToDo
    ========================================
        
    ОБЩИЕ ПРИНЦИПЫ данного WEB проекта:
    -----------------------------------
       
        - Проект построен на ...
        - В проекте используется отслеживание версий (локальный .git и GitHub)
        ... и т.д.
        ---- ✄ -----------------------
      
    ТАЙМИНГ проекта:
    ----------------
        
        ☐ Создан @created(xx-xxx-xxxx xx:xx) (дата создания проекта)
        ☐ Deadline @due(xx-xxx-xxxx xx:xx)   (предполагаемая дата окончания работы над проектом)
        ✔ Общая продолжительность: @started(xx-xxx-xxxx xx:xx) @done (xx-xxx-xxxx xx:xx) @lasted(x:xx) 
     
        Тайминг по дням:                              (работа над проектом по дням)
            ✔ xx.xx.xxxx -> @started(xx-xxx-xxxx xx:xx) @toggle(xx-xxx-xxxx xx:xx) @toggle(xx-xxx-xxxx xx:xx) @done(xx-xxx-xxxx xx:xx) @lasted(x:xx)
            ... и т.д.
            ---- ✄ -----------------------
     
    ГЛОБАЛЬНЫЕ ЦЕЛИ и ЗАДАЧИ проекта:
    ----------------------------------
      
        ... и т.д.
        ---- ✄ -----------------------
     
    ОСНОВНЫЕ ВЕХИ проекта:
    -----------------------
     
        ✔ Первичная установка, создание ThisProject.todo, первый коммит в .git и GitHub @started(xx-xxx-xxxx xx:xx)
        ... и т.д.
        ---- ✄ -----------------------
     
    ТЕКУЩИЕ ЗАДАЧИ:
    (выполненные задачи уходят вниз, в Архив)
    ------------------------------------------  
     
        ☐ Первый коммит в .git и GitHub @started(xx-xxx-xxxx xx:xx)
        ... и т.д 
        ---- ✄ -----------------------
      
    МЕЛОЧИ:
    -------
     
        ... и т.д 
        ---- ✄ -----------------------
      
    АРХИВ:
    ------
     
        ... и т.д 
        ---- ✄ -----------------------

[в начало](#user-content-start)

<a id="user-content-Первая-фиксация-коммит-в-git-и-github"></a>
## Первая фиксация коммит в .git и GitHub
Производится после создания файла ThisProject.todo и .gitignore.

    git init
    git status
    git add .

[в начало](#user-content-start)

<a id="user-content-Создание-локального-виртуального-хоста"></a>
## Создание локального виртуального хоста
* Настроить Apache для направления локального сайта `sand-ProjectName-v0.local` на рабочий каталог `..\public\`
Например:

        ## Вирт. хост http://sand-ProjectName-v0.local  
        ## Добавлено 26.10.2018 2:00
            <VirtualHost *:80 *:809[0,1 и т.д]>  
                ServerAdmin webmaster@sand-projectname-v0.local  
                DocumentRoot "e:\__MyDEV\www\2018\ProjectName\SANDBOX\public"  
                ServerName sand-projectname-v0.local  
                ErrorLog "e:\__MyDEV\www\2018\ProjectName\.logs\error.log"  
                CustomLog "e:\__MyDEV\www\2018\ProjectName\.logs\access.log" common  
            </VirtualHost>  
            <Directory "e:\__MyDEV\www\2018\ProjectName">  
                AllowOverride All  
                Require all granted  
            </Directory>

* Настроить файл hosts (под рутом).  
    `127.0.0.1                      sand-projectname-v0.local`   
    `192.168.0.[101]:809[0,1 и т.д]   sand-projectname-v0.local`

При настройке виртуального хоста необходимо:
* убедиться на каком именно IP находится данный компьютер (актуально для файла hosts)
* включить прослушивание необходимого порта в Apache (в файле httpd.conf)
* разрешить использование указанного порта в системном фаерволе.

При правильной настройке Apache по умолчанию:  
по адресу http://sand-projectname-v0.local виден index.php  
по адресу http://sand-projectname-v0.local/index.html виден index.html  
Оба адреса также должны быть видны со смартфона как:    
`http://192.168.0.[101]:809[0, 1 и т.д.]`  (файл php)  
`http://192.168.0.[101]:809[0, 1 и т.д.]/index.html`  (файл hlml)
