# bacula_backup   
#### Description   
[Bacula](https://www.bacula.org/) — cross-platform client-server software that allows you to manage backup, recovery, and data verification over the network for computers and operating systems of various types.    
#### Components   
* Director (DIR) — The Bacula Director service is the program that supervises all the backup, restore, verify and archive operations. The system administrator uses the Bacula Director to schedule backups and to recover files. For more details see the Director Services Daemon Design Document in the Bacula Developer's Guide. The Director runs as a daemon (or service) in the background.    
The Bacula Director is responsible for setting up the file[/etc/bacula/bacula-dir.conf](https://github.com/Hanafeevrus/bacula_backup/blob/master/bacula-dir.conf)    
* File Daemon (FD) - a service that performs direct copying, recovery and verification of data at the request of Director. File Daemon must be installed on each client machine. File Daemon communicates with Director and Storage Daemon. The file is responsible for the configuration [/etc/bacula/bacula-fd.conf](https://github.com/Hanafeevrus/bacula_backup/blob/master/bacula-fd.conf).   
* Storage Daemon (SD) - reads and writes data to physical media: disk, tape, DVD, USB. The file is responsible for the configuration[/etc/bacula/bacula-sd.conf](https://github.com/Hanafeevrus/bacula_backup/blob/master/bacula-sd.conf)   
* Console — The Bacula Console service is the program that allows the administrator or user to communicate with the Bacula Director Currently, the Bacula Console is available in three versions: text-based console interface, QT-based interface, and a wxWidgets graphical interface. The first and simplest is to run the Console program in a shell window (i.e. TTY interface). Most system administrators will find this completely adequate. The second version is a GNOME GUI interface that is far from complete, but quite functional as it has most the capabilities of the shell Console. The third version is a wxWidgets GUI with an interactive file restore. It also has most of the capabilities of the shell console, allows command completion with tabulation, and gives you instant help about the command you are typing. For more details see the Bacula Console Design DocumentTheConsoleChapterconsoleChapter. The file is responsible for the configuration [/etc/bacula/bconsole.conf](https://github.com/Hanafeevrus/bacula_backup/blob/master/bconsole.conf).    
* Catalog database — SQL database: MySQL, PostgreSQL, or SQLite for storing metadata.   
* Tray Monitor — A Bacula Monitor service is the program that allows the administrator or user to watch current status of Bacula Directors, Bacula File Daemons and Bacula Storage Daemons. Currently, only a GTK+ version is available, which works with GNOME, KDE, or any window manager that supports the FreeDesktop.org system tray standard.
To perform a successful save or restore, the following four daemons must be configured and running: the Director daemon, the File daemon, the Storage daemon, and the Catalog service (MySQL, or PostgreSQL).    
All of these components can be located on one computer or on several networked ones.    
#### Task
Configure a backup policy for the / etc directory from the client:    
1) Full backup - once a day   
2) Incremental - every 10 minutes   
3) Differential - every 30 minutes      

#### Solution   
fork git https://github.com/haf/vagrant-bacula    
edited settings in the file [/etc/bacula/bacula-dir.conf](https://github.com/Hanafeevrus/bacula_backup/blob/master/bacula-dir.conf)   
`vagrant up` raises the server and 2 clients. All server components are configured on the same server machine.   
#### Check   
`bconsole` - commands that launch the management console of the operator or administrator.    
More information about the console [on the offsite](https://www.bacula.org/5.0.x-manuals/en/console/console/Bacula_Console.html).   
![list jobs](https://github.com/Hanafeevrus/bacula_backup/blob/master/list_jobs.png)   
![list files](https://github.com/Hanafeevrus/bacula_backup/blob/master/list_files.png)    
![status schedule](https://github.com/Hanafeevrus/bacula_backup/blob/master/status.png)    
