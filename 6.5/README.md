# Домашнее задание к занятию «Модули расширения»

### Цель задания

Модули расширения ПЛК позволяют расширить возможности ПЛК в части количества входов/выходов, обмена данными с использованием различных интерфейсов, выполнения специальных функций. Выполнив домашнее задание, вы получите опыт подбора модулей ПЛК по заданным требованиям проекта, а также создадите проект в TIA Portal 13 и научитесь выбирать и добавлять в проект аппаратные компоненты.

В результате выполнения этого задания вы сможете:

1. Создать из модулей конфигурацию, удовлетворяющую условиям проекта.
2. Получить опыт работы с системой TIA Portal в части аппаратной конфигурации.

------

### Чеклист готовности к домашнему заданию

1. Зарегистрируйтесь на [портале Siemens](https://mall.industry.siemens.com/goos/WelcomePage.aspx?regionUrl=/ru&language=ru) и получите персональный логин и пароль для входа в систему. Процесс регистрации описан в [соответствующей инструкции](https://docs.google.com/presentation/d/1RPHvCE2OxBbHRMWSAV2E-HxscZvR2nRIZVHCy8hvjJE/edit?usp=sharing).
2. Загрузите и установите программное обеспечение для создания проекта, входящее в состав пакета TIA Portal с [официального ресурса Siemens](https://support.industry.siemens.com/cs/document/78793685/simatic-step-7-(tia-portal)-v13-trial-download?dti=0&lc=en-DE):
- скачайте все файлы STEP 7 Professional V13 SP2 (DVD 1, DVD 2, SHA-256 checksum) по ссылке в отдельную папку
- запустите SIMATIC_STEP_7_Professional_V13_SP2_Upd4.exe
- пройдите стандартную процедуру установки

*ОБРАТИТЕ ВНИМАНИЕ! Устанавливается демо-версия программы. Её функционал будет ограничен спустя 21 день после установки. Рекомендуется установка софта на виртуальной машине. Как это сделать, описано в [инструкции](https://docs.google.com/presentation/d/1psnSlotXT7cr8ECnaZaTCDLnIyYOGUzCArLeydeRztY/edit?usp=sharing).*

------

### Инструкция к заданию

1. Сделайте копию [Шаблона для домашнего задания](https://docs.google.com/document/d/1JzKdVrCtsJI2SSeLnUb3qOxou1Ag39Umbd__BDpFP6o/edit?usp=sharing) себе на Google Диск.
2. В названии файла введите корректное название лекции и вашу фамилию и имя.
3. Зайдите в «Настройки доступа» и выберите доступ «Просматривать могут все в Интернете, у кого есть ссылка».
 Ссылка на инструкцию [Как предоставить доступ к файлам и папкам на Google Диске](https://support.google.com/docs/answer/2494822?hl=ru&co=GENIE.Platform%3DDesktop)
4. Скопируйте текст задания в свой документ.
5. Выполните домашнее задание, запишите ответы и приложите необходимые скриншоты в свой Google Doc.
6. Для проверки домашнего задания преподавателем отправьте ссылку на ваш документ в личном кабинете.
7. Любые вопросы по решению задач задавайте в чате учебной группы.

------

### Инструменты/ дополнительные материалы, которые пригодятся для выполнения задания

1. [TIA Portal 13](https://support.industry.siemens.com/cs/document/109745155/simatic-step-7-including-plcsim-v13-sp2-trial-download?dti=0&lc=en-WW)
2. [Инструкция по созданию виртуальной машины](https://docs.google.com/presentation/d/1psnSlotXT7cr8ECnaZaTCDLnIyYOGUzCArLeydeRztY/edit?usp=sharing)
3. [Шаблон для домашнего задания](https://docs.google.com/document/d/1JzKdVrCtsJI2SSeLnUb3qOxou1Ag39Umbd__BDpFP6o/edit?usp=sharing)

------

### Задание 1

Создайте аппаратную конфигурацию в программном проекте TIA Portal 13, удовлетворяющую изложенным ниже условиям.

Промышленная установка располагается в двух цехах.

1. В цехе 1 расположена ёмкость с сырьем, установлен тензодатчик для измерения веса продукта в ёмкости.

Предусмотрена подача сырья в цех 2, для чего на сливе происходит разделение на 4 потока по отдельным трубам. На каждом из трубопроводов установлен насос (1 дискретный входной сигнал - состояние «включён/отключён» + 1 дискретный выходной сигнал - команда «включить/отключить») - итого 4 насоса.

Дополнительно для каждого насоса предусмотрен мониторинг тока нагрузки (1 аналоговый входной сигнал, 4...20 mA) и управление частотой вращения (1 аналоговый выходной сигнал, ±10 V).

2. В цехе 2 расположены 4 ёмкости. Для каждой из них предусмотрены заливка и слив продукта. На трубах, ведущих к и от каждой ёмкости, установлены отсечные клапана (2 входных дискретных сигнала - концевые выключатели «открыт", «закрыт" + 2 выходных дискретных сигнала - команды «открыть», «закрыть») - итого 8 клапанов.

Система управления в части ПЛК должна состоять из двух стоек (rack):
- Стойка 1 предназначена для управления оборудованием в цехе 1. Она должна представлять из себя CPU с возможностью доустановки необходимых модулей расширения.
- Стойка 2 предназначена для управления оборудованием в цехе 2. Она должна представлять из себя стойку распределенной периферии с возможностью доустановки необходимых модулей расширения.

Соединение между стойками должно быть произведено по протоколу Profinet. 

При конфигурировании допускается использование следующих компонентов:
- CPU - 6ES7 217-1AG40-0XB0
- модуль приёма сигнала с весовой ячейки - 7MH4960-2AA01
- стойка распределённой периферии - 6ES7 155-6AU00-0BN0
- модуль дискретных входных сигналов (DI) - 6ES7 131-6BF00-0BA0 или 6ES7 221-1BF30-0XB0
- модуль дискретных выходных сигналов (DO) - 6ES7 132-6BF00-0CA0 или 6ES7 222-1BF30-0XB0
- модуль аналоговых входных сигналов (AI) - 6ES7 134-6HD00-0BA1 или 6ES7 231-4HF32-0XB0
- модуль аналоговых выходных сигналов (AO) - 6ES7 135-6HD00-0BA1 или 6ES7 232-4HD32-0XB0.

Произвести компиляцию Hardware, сохранить проект и сделать его архивную копию, ссылку на которую следует приложить к заданию.

------

### Правила приёма работы

1. Отправлена ссылка на документ (Google Doc) с выполненным заданием в личном кабинете.
2. Документ размещён на личном Google Диске.
3. К документу настроены права доступа «Просматривать могут все в Интернете, у кого есть ссылка».

------

### Критерии оценки

Задание считается выполненным, если в приложенном программном проекте TIA Portal 13 в разделе аппаратной конфигурации создана конфигурация, соответствующая заданию.
