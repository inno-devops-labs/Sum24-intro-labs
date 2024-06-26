# DevOps Lab 4
## Task 1: Configure and Use a Local Package Repository
### The output:
```bash
roiven@roiven-MS-7C02:~/DEVOPS$ mkdir -p ~/local-apt-repo
roiven@roiven-MS-7C02:~/DEVOPS$ cp jdk-22_linux-x64_bin.deb ~/local-apt-repo/
roiven@roiven-MS-7C02:~/DEVOPS$ dpkg-scanpackages ~/local-apt-repo /dev/null | gzip -9c > ~/local-apt-repo/Packages

dpkg-scanpackages: предупреждение: Пакеты есть в архиве, но отсутствуют в файле переназначений:
dpkg-scanpackages: предупреждение:   gnome-calculator jdk-22
dpkg-scanpackages: инфо: Записано 2 записей в выходной файл Packages.

roiven@roiven-MS-7C02:~/DEVOPS$ cd ~/local-apt-repo/
roiven@roiven-MS-7C02:~/local-apt-repo$ echo "deb [trusted=yes] file:/home/roiven/local-apt-repo ./" | sudo tee /etc/apt/sources.list.d/local-apt-repo.list

deb [trusted=yes] file:/home/roiven/local-apt-repo ./

roiven@roiven-MS-7C02:~/local-apt-repo$ zcat Packages

Package: jdk-22
Version: 22.0.1-ga
Architecture: amd64
Maintainer: jdk-download-help_ww <jdk-download-help_ww@oracle.com>
Installed-Size: 335132
Provides: jdk-22
Filename: /home/roiven/local-apt-repo/jdk-22_linux-x64_bin.deb
Size: 167613956
MD5sum: 8a8b3c51a07a5aeda48bcef81a3526c1
SHA1: 91e17ae86ca6857f24a52d11be031fc8cdde39a8
SHA256: 9f206a5c6b139a9919b91d4ca36d68d7a17c571fde4a073601213854b3d6d02a
Section: java
Priority: optional
Description: Java Platform Standard Edition Development Kit
 The Java Platform Standard Edition Development Kit (JDK) includes both the runtime environment (Java virtual machine, the Java platform classes and supporting files) and development tools (compilers, debuggers, tool libraries and other tools). The JDK is a development environment for building applications, applets and components that can be deployed with the Java Platform Standard Edition Runtime Environment.

roiven@roiven-MS-7C02:~/local-apt-repo$ apt policy jdk-22

jdk-22:
  Установлен: (отсутствует)
  Кандидат:   22.0.1-ga
  Таблица версий:
     22.0.1-ga 500
        500 file:/home/roiven/local-apt-repo ./ Packages

roiven@roiven-MS-7C02:~/local-apt-repo$ sudo apt install jdk-22
Чтение списков пакетов… Готово
Построение дерева зависимостей… Готово
Чтение информации о состоянии… Готово         
Следующие НОВЫЕ пакеты будут установлены:
  jdk-22
Обновлено 0 пакетов, установлено 1 новых пакетов, для удаления отмечено 0 пакетов, и 35 пакетов не обновлено.
Необходимо скачать 0 B/168 MB архивов.
После данной операции объём занятого дискового пространства возрастёт на 343 MB.
Пол:1 file:/home/roiven/local-apt-repo ./ jdk-22 22.0.1-ga [168 MB]
Выбор ранее не выбранного пакета jdk-22.
(Чтение базы данных … на данный момент установлено 214918 файлов и каталогов.)
Подготовка к распаковке …/./jdk-22_linux-x64_bin.deb …
Распаковывается jdk-22 (22.0.1-ga) …
Настраивается пакет jdk-22 (22.0.1-ga) …
update-alternatives: используется /usr/lib/jvm/jdk-22-oracle-x64/bin/jar для предоставления /usr/bin/jar (jar) в автоматическом режиме
update-alternatives: используется /usr/lib/jvm/jdk-22-oracle-x64/bin/jarsigner для предоставления /usr/bin/jarsigner (jarsigner) в автоматическом режиме
update-alternatives: используется /usr/lib/jvm/jdk-22-oracle-x64/bin/java для предоставления /usr/bin/java (java) в автоматическом режиме
update-alternatives: используется /usr/lib/jvm/jdk-22-oracle-x64/bin/javac для предоставления /usr/bin/javac (javac) в автоматическом режиме
update-alternatives: используется /usr/lib/jvm/jdk-22-oracle-x64/bin/javadoc для предоставления /usr/bin/javadoc (javadoc) в автоматическом режиме
update-alternatives: используется /usr/lib/jvm/jdk-22-oracle-x64/bin/javap для предоставления /usr/bin/javap (javap) в автоматическом режиме
update-alternatives: используется /usr/lib/jvm/jdk-22-oracle-x64/bin/jcmd для предоставления /usr/bin/jcmd (jcmd) в автоматическом режиме
update-alternatives: используется /usr/lib/jvm/jdk-22-oracle-x64/bin/jconsole для предоставления /usr/bin/jconsole (jconsole) в автоматическом режиме
update-alternatives: используется /usr/lib/jvm/jdk-22-oracle-x64/bin/jdb для предоставления /usr/bin/jdb (jdb) в автоматическом режиме
update-alternatives: используется /usr/lib/jvm/jdk-22-oracle-x64/bin/jdeprscan для предоставления /usr/bin/jdeprscan (jdeprscan) в автоматическом режиме
update-alternatives: используется /usr/lib/jvm/jdk-22-oracle-x64/bin/jdeps для предоставления /usr/bin/jdeps (jdeps) в автоматическом режиме
update-alternatives: используется /usr/lib/jvm/jdk-22-oracle-x64/bin/jfr для предоставления /usr/bin/jfr (jfr) в автоматическом режиме
update-alternatives: используется /usr/lib/jvm/jdk-22-oracle-x64/bin/jhsdb для предоставления /usr/bin/jhsdb (jhsdb) в автоматическом режиме
update-alternatives: используется /usr/lib/jvm/jdk-22-oracle-x64/bin/jimage для предоставления /usr/bin/jimage (jimage) в автоматическом режиме
update-alternatives: используется /usr/lib/jvm/jdk-22-oracle-x64/bin/jinfo для предоставления /usr/bin/jinfo (jinfo) в автоматическом режиме
update-alternatives: используется /usr/lib/jvm/jdk-22-oracle-x64/bin/jlink для предоставления /usr/bin/jlink (jlink) в автоматическом режиме
update-alternatives: используется /usr/lib/jvm/jdk-22-oracle-x64/bin/jmap для предоставления /usr/bin/jmap (jmap) в автоматическом режиме
update-alternatives: используется /usr/lib/jvm/jdk-22-oracle-x64/bin/jmod для предоставления /usr/bin/jmod (jmod) в автоматическом режиме
update-alternatives: используется /usr/lib/jvm/jdk-22-oracle-x64/bin/jpackage для предоставления /usr/bin/jpackage (jpackage) в автоматическом режиме
update-alternatives: используется /usr/lib/jvm/jdk-22-oracle-x64/bin/jps для предоставления /usr/bin/jps (jps) в автоматическом режиме
update-alternatives: используется /usr/lib/jvm/jdk-22-oracle-x64/bin/jrunscript для предоставления /usr/bin/jrunscript (jrunscript) в автоматическом режиме
update-alternatives: используется /usr/lib/jvm/jdk-22-oracle-x64/bin/jshell для предоставления /usr/bin/jshell (jshell) в автоматическом режиме
update-alternatives: используется /usr/lib/jvm/jdk-22-oracle-x64/bin/jstack для предоставления /usr/bin/jstack (jstack) в автоматическом режиме
update-alternatives: используется /usr/lib/jvm/jdk-22-oracle-x64/bin/jstat для предоставления /usr/bin/jstat (jstat) в автоматическом режиме
update-alternatives: используется /usr/lib/jvm/jdk-22-oracle-x64/bin/jstatd для предоставления /usr/bin/jstatd (jstatd) в автоматическом режиме
update-alternatives: используется /usr/lib/jvm/jdk-22-oracle-x64/bin/jwebserver для предоставления /usr/bin/jwebserver (jwebserver) в автоматическом режиме
update-alternatives: используется /usr/lib/jvm/jdk-22-oracle-x64/bin/keytool для предоставления /usr/bin/keytool (keytool) в автоматическом режиме
update-alternatives: используется /usr/lib/jvm/jdk-22-oracle-x64/bin/rmiregistry для предоставления /usr/bin/rmiregistry (rmiregistry) в автоматическом режиме
update-alternatives: используется /usr/lib/jvm/jdk-22-oracle-x64/bin/serialver для предоставления /usr/bin/serialver (serialver) в автоматическом режиме
update-alternatives: используется /usr/lib/jvm/jdk-22-oracle-x64/lib/jexec для предоставления /usr/bin/jexec (jexec) в автоматическом режиме
N: Загрузка выполняется от лица суперпользователя без ограничений песочницы, так как файл «/home/roiven/local-apt-repo/./jdk-22_linux-x64_bin.deb» недоступен для пользователя «_apt». - pkgAcquire::Run (13: Отказано в доступе)
```

## Task 2: Simulate Package Installation and Identify Dependencies
### The output:
```bash
roiven@roiven-MS-7C02:~/local-apt-repo$ apt-cache showpkg jdk-22

Package: jdk-22
Versions: 
22.0.1-ga (/var/lib/apt/lists/_home_roiven_local-apt-repo_._Packages) (/var/lib/dpkg/status)
 Description Language: 
                 File: /var/lib/apt/lists/_home_roiven_local-apt-repo_._Packages
                  MD5: 0bfa4e99c13846f7377c9011c1c238c1


Reverse Depends: 
Dependencies: 
22.0.1-ga - 
Provides: 
22.0.1-ga - 
Reverse Provides: 

roiven@roiven-MS-7C02:~/local-apt-repo$ sudo apt-get install -s jdk-22

Чтение списков пакетов… Готово
Построение дерева зависимостей… Готово
Чтение информации о состоянии… Готово         
Уже установлен пакет jdk-22 самой новой версии (22.0.1-ga).
Обновлено 0 пакетов, установлено 0 новых пакетов, для удаления отмечено 0 пакетов, и 35 пакетов не обновлено.
```
no dependecies, no packages to be installed

## Task 3: Hold and Unhold Package Versions
### The output:
```bash
roiven@roiven-MS-7C02:~/local-apt-repo$ sudo apt-mark hold jdk-22

jdk-22 помечен как зафиксированный.

roiven@roiven-MS-7C02:~/local-apt-repo$ apt-mark showhold

jdk-22

roiven@roiven-MS-7C02:~/local-apt-repo$ sudo apt-mark unhold jdk-22

Отмена фиксации для jdk-22.

roiven@roiven-MS-7C02:~/local-apt-repo$ apt-mark showhold
```

### The late subimission is approved:

