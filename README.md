# bacula_backup   
#### Описание   
[Bacula](https://www.bacula.org/) — кроссплатформенное клиент-серверное программное обеспечение, позволяющее управлять резервным копированием, восстановлением, и проверкой данных по сети для компьютеров и операционных систем различных типов.    
#### Компоненты
* Director (DIR) — осуществляет централизованный контроль и администрирование всего комплекса задач. Планирование и управление заданиями на резервное копирование (Job). Обслуживание Каталога (Catalog) — центральной БД для хранения метаданных.    
За настройку Bacula Director отвечает файл [/etc/bacula/bacula-dir.conf](https://github.com/Hanafeevrus/bacula_backup/blob/master/bacula-dir.conf)    
* File Daemon (FD) — сервис, выполняющий непосредственное копирование, восстановление и проверку данных по запросу Director. File Daemon должен быть установлен на каждой клиентской машине. File Daemon обменивается информацией с Director и Storage Daemon. За настройку отвечает файл [/etc/bacula/bacula-fd.conf](https://github.com/Hanafeevrus/bacula_backup/blob/master/bacula-fd.conf).   
* Storage Daemon (SD) — читает и пишет данные на физический носитель: диск, ленту, DVD, USB. За настройку отвечает файл [/etc/bacula/bacula-sd.conf](https://github.com/Hanafeevrus/bacula_backup/blob/master/bacula-sd.conf)   
* Console — управляющая консоль оператора или администратора. Поддерживаются ACL для разных пользователей консоли. Типы консолей: TTY, wxWidgets (GUI) для Linux, Unix, Win32, GNOME (GUI), несколько веб-интерфейсов, Qt4. За настройку отвечает файл [/etc/bacula/bconsole.conf](https://github.com/Hanafeevrus/bacula_backup/blob/master/bconsole.conf).    
* Catalog database — база данных SQL : MySQL, PostgreSQL, или SQLite для хранения метаданных.   
* Tray Monitor — апплет GNOME/KDE/Win32 GUI для показа активности Director, File daemons, Storage daemon в реальном времени.    
Все указанные компоненты могут находиться как на одном компьютере, так и на нескольких, объединённых в сеть.    
#### Задача
Настроить политику бэкапа директории /etc с клиента:    
1) Полный бэкап - раз в день    
2) Инкрементальный - каждые 10 минут    
3) Дифференциальный - каждые 30 минут   

#### Реализация   
fork git https://github.com/haf/vagrant-bacula    
отредактированы настройки в файле [/etc/bacula/bacula-dir.conf](https://github.com/Hanafeevrus/bacula_backup/blob/master/bacula-dir.conf)   
`vagrant up` поднимает сервер и 2 клиента. Все серверные компоненты настроены на одной машине server.   
#### Проверка   
`bconsole` - команды запускающая управляющаю консоль оператора или администратора.    
Подробнее о консоли [на офсайте](https://www.bacula.org/5.0.x-manuals/en/console/console/Bacula_Console.html).   
![list jobs](https://github.com/Hanafeevrus/bacula_backup/blob/master/list_jobs.png)   
![list files](https://github.com/Hanafeevrus/bacula_backup/blob/master/list_files.png)    
![status schedule](https://github.com/Hanafeevrus/bacula_backup/blob/master/status.png)    
