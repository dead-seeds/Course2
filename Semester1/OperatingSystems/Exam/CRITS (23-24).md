1. **Понятие файла и файловой системы. Что такое каталог?**
   _Файл_ - совокупность данных, адресующаяся по имени, которую можно читать и писать.
   
   _Каталог, директория_ - таблица преобразований имен файлов в адреса.
   
   _Файловая система_ - программный комплекс, работающий с определенным форматом метаданных и совокупностью каталогов. (Также отслеживает расположение файлов и свободное дисковое пространство)


2. **Определение задачи реального времени.**
   _Задача реального времени_ - задача, которая реагирует на внешние события в течение гарантированного времени.


3. **Алгоритм работы библиотечных функций malloc/free языка C.**
   Выделение памяти происходит по стратегии first fit.
   Для освобождения используется алгоритм парных меток.


4. **Что такое системный и пользовательский режимы процессора?**
   _Системный режим (режим ядра)_ - режим, в котором исполняемый код имеет полный доступ ко всему аппаратному обеспечению и может задействовать любую инструкцию, которую машина в состоянии выполнить.

   _Пользовательский режим_ - режим, в котором программам запрещено использование инструкций, управляющих машиной или осуществляющих операции ввода-вывода.


5. **Что такое транзакция?**
   _Транзакция_ - группа операций модификации разделяемой структуры данных, которая происходит атомарно (неделимо) (не прерываясь никакими другими операциями с этой же структурой данных.


6. **Что такое семафоры Дийкстры?**
   _Семафор Дейкстры_ - целочисленная переменная, с которой ассоциирована очередь ожидающих нитей.  


7. **Что такое мертвая блокировка?**
    Мертвая блокировка - это проблема образования цикла в графе ожидающих друг друга задач.


8. **Что такое контекст процесса?**
    Полный набор регистров, которые нужно сохранить, чтобы нить не заметила переключения.


9. **Что такое гармонически взаимодействующие последовательные процессы?**
    _Гармонически взаимодействующие последовательные процессы_ - процессы, при взаимодействии между которыми глобальные переменные и разделяемая память не используются.

  Или более подробно (как дано в книге):  
  Концепция:  
  1) Каждый поток исполнения представляет собой независимый программный модуль.  
  2) Нити не имеют разделяемых данных.  
  3) Взаимодействие происходит с использованием специальных примитивов, которые одновременно выполняют передачу данных и синхронизацию.  


10. **Что такое селектор страницы (сегмента) в сегментных и страничных диспетчерах памяти?**
    _Селектор_ - индекс в таблице трансляции, определяет номер _дескриптора_ страницы/сегмента.

    Складывая его с указателем на таблицу трансляции, получаем адрес дескриптора данной страницы/сегмента.


11. **Что такое дескриптор страницы (сегмента) в сегментных и страничных диспетчерах памяти?**
    _Дескриптор_ - элемент таблицы трансляции. Дескриптор содержит права доступа к странице, признак присутствия этой страницы в памяти, и физический адрес страницы/сегмента. Для сегментов в дескрипторе также хранится его длина.

    Отличие сегмента от страницы: страница имеет _фиксированный размер_, сегменты могут в рамках работы иметь _разный размер_. 


12. **Что такое абсолютный и относительный загрузчики?**
    _Абсолютный загрузчик_: концепция состоит в том, что программа загружается с одного и того же адреса.

    _Относительный загрузчик_: программа может загружаться каждый раз с нового адреса. Адреса объектов хранятся в виде смещения друг относительно друга.


13. **Что является элементом таблицы перемещений в относительном (перемещаемом) загрузочном модуле?**
    Запись, которая хранит место ссылки на символ в коде или данных. (смещение от начала модуля)


14. **Что такое позиционно-независимый код?**
    _Позиционно-независимый код_ - код, использующий только относительную адресацию.

    Адрес получается сложением адреса команды (счетчик команд) и адресного поля.


15. **Что такое реентерабельная программа?**
    _Реентерабельная программа_ - программный модуль, который либо не содержит критических секций, либо сам обеспечивает взаимное исключение для них.


16. **Что такое критическая секция?**
    _Критическая секция_ – это участок кода программы, во время исполнения которого программа либо полагается на целостность разделяемой структуры данных, либо тем или иным образом нарушает эту целостность.


17. **Кольца доступа и списки контроля доступа.**
    _Список контроля доступа_ - таблица, ассоциированная с объектом или группой объектов, строки которой соответствуют учетным записям пользователей, а столбцы отдельным операциям, которые можно осуществлять над объектом.

    _Кольца защиты_ - организация доступа, при которой каждый более привилегированный режим всегда как минимум имеет те же права, которые имеют менее привилегированные режимы.


18. **Кооперативные многозадачные системы и вытесняющая (preemptive) многозадачность.**
    _Принцип кооперативной многозадачности_ - принцип переключения по инициативе активной нити.

    _Вытесняющая многозадачность_ - принцип переключения по инициативе системы.
