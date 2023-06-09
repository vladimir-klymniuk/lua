# Interpetator

Опция -l загружает библиотеку. Как мы уже видели ранее, -i переводит интерпретатор в интерактивный режим после обработки остальных аргументов. Таким образом, следующий вызов загрузит библиотку lib, затем выполнит присваивание x=10 и на конец прейдет в интерактивный режим.

```bash
    lua -i -llib -e "x = 10"
```

В интерактивном режиме вы можете напечатать значение выражения, 
просто набрав строку, начинающуюся со знака равенства, за которым следует выражение:

```lua
    = math.sin(3) --> 0.14112000805987
    a = 30
    = a --> 30
```

!!!  |
    \|/
     v
``` r
Эта особенность позволяет использовать Lua как калькулятор.
Перед выполнением своих аргументов интерпретатор ищет переменную окружения с именем `LUA_INIT_5_2` (или LUA_INIT)
определена, но не начинается с символа `@`, то интерпретатор предполагает, 
что она содержит выполнимый код на Lua и выполняет его. 
```

!!!  |
    \|/
     v
``` r
!!LUA_INIT даёт огромные возможности по конфигурированию интерпретатора, поскольку при конфигурировании нам доступна вся мощь Lua. Мы можем загрузить пакеты, изменить текущий путь, определить свои собственные функции, переименовать или уничтожить функции итд

Скрипт может получить свои аргументы в глобальной переменной arg. Если у нас есть вызов вида %lua script a b c, то интерпретатор создает таблицу arg со всеми аргументами командной строки перед выполнением скрипта. Имя скрипта расположено по индекусу 0, первый аргумент (в примере это "а") расположен по индексу 1 итд

Предшествующие опции располодены по негативным индексам, поскольку они расположены перед именем скрипта. Рассмотрим следующий вызов:
```

```lua
    % lua -e "sin=math.sin" script a b
```
Интерпретатор собирает аргументы следующим образом:
```lua
    arg[-3] = "lua"
    arg[-2] = "-e"
    arg[-1] = "sin=math.sib"
    arg[0]  = "script"
    arg[1]  = "a"
    arg[2]  = "b"
```

Чаще всего скрипт использует только положительные индексы (в примере это `arg[1]` и `arg[2]`). 
Начиная с Lua5.1 скрипт также может получить свои аргументы при помощи выражения ... (три точки). В главной части скрипта это выражение дает все аргументы скрипта.
