Altera-Test-System v.1.0.2
==================

Система предварительного тестирования правок на сайте

Задача использования ATS сводится к использованию флагов помещенных 
системой в соответствующую куку.

По умолчанию имя куки - "altera-test-system", но может быть изменено.

Если значение установлено в 'true' (интерпретируется как строка) - то при 
проверке на сайте должен выводиться тестовый контент/верстка/функционал.

Если значение куки не установлено или отлично от 'true' - то сайт 
выводится в обычном режиме.

Крайне рекомендуется в главный шаблон сайта и все шаблоны его страниц 
внедрять проверочный код, чтобы можно было сразу понять, мы работаем с 
сайтом в тестовом режиме или нет.

Самое обычное - вывод иконки система в шапке сайта. 

Для внедрения ATS на сайт клиента необходимо:
 - скопировать файл altera-test-system.html в корневой каталог сайта
 - внести изменения в шаблоны
 - далее вносить все правки в соответствующих условных конструкциях



Где взять иконку?
Уже есть готовый рабочий код для php, для внедрения на сайт с почти любой версткой


==================
Код в шапке сайта
```PHP+HTML
<?php if ( array_key_exists('altera-test-system', $_COOKIE) && ($_COOKIE['altera-test-system'] == 'true')): ?>
	<style>
		#altera-test-system {	
			background: url(data:image/png;base64,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);
			position: absolute;
			width: 50px;
			height: 50px;
			cursor: pointer;
		}
	</style>
	<div id="altera-test-system" onClick="location='/altera-test-system.html';return false;"></div>
<?php endif; ?>
```
==================
Функционаял системы:
 - При клилке на иконку в файле происходит смена состояния куки.
 - При двойном клике на тело файла - переход на основной домен.
 - При клике на иконку выводимую в шаблоне - быстрый переход на ATS.


Как проверить значение сессионной переменной?

Рассмотрим 4 варианта:

==================
1) PHP
```PHP
if ( array_key_exists('altera-test-system', $_COOKIE) && ($_COOKIE['altera-test-system'] == 'true')) {
	//новый функционал
} else {
	//старый функционал
}
```
==================
2) Smarty  
```Smarty
{if $smarty.cookies.altera-test-system eq 'true'}
	<!-- новый функционал -->
{else}
	<!-- старый функционал -->
{/if}
```
==================
3) JS

Самый простой способ, по первому варианту подключать разные JS файлы в шаблоне, 
если же мы немного меняем логику скрипта, то возможны варианты:

Объявляем функцию:
```JavaScript
function getCookie(c_name) {
    if (document.cookie.length > 0) {
        var c_start = document.cookie.indexOf(c_name + "=");
        if (c_start != -1) {
            c_start = c_start + c_name.length + 1;
            var c_end = document.cookie.indexOf(";", c_start);
            if (c_end == -1) {
                c_end = document.cookie.length;
            }
            return unescape(document.cookie.substring(c_start, c_end));
        }
    }
    return "";
}
```

Используем её:
```JavaScript
if (getCookie('altera-test-system') == 'true') {
	//новый функционал
} else {
	//старый функционал
}
```

==================
4) JS (jQuery)  

Вариант попроще (наличие jQuery обязательно):
Подключаем пагин куки к jQuery: https://github.com/carhartl/jquery-cookie
```JavaScript
if ($.cookie('altera-test-system') == 'true') {
	//новый функционал
} else {
	//старый функционал
}
```
