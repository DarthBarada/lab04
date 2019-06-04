[![Build Status](https://travis-ci.org/DarthBarada/lab04.svg?branch=master)](https://travis-ci.org/DarthBarada/lab04)
## Laboratory work IV

Данная лабораторная работа посвещена изучению систем непрерывной интеграции на примере сервиса **Travis CI**

```ShellSession
$ open https://travis-ci.org
```

## Tasks

- [X] 1. Авторизоваться на сервисе **Travis CI** с использованием **GitHub** аккаунта
- [X] 2. Создать публичный репозиторий с названием **lab04** на сервисе **GitHub**
- [X] 3. Ознакомиться со ссылками учебного материала
- [X] 4. Включить интеграцию сервиса **Travis CI** с созданным репозиторием
- [X] 5. Получить токен для **Travis CLI** с правами **repo** и **user**
- [X] 6. Получить фрагмент вставки значка сервиса **Travis CI** в формате **Markdown**
- [X] 7. Выполнить инструкцию учебного материала
- [X] 8. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

Начало:
```ShellSession
# Устанавливаем параметры окружения 
$ export GITHUB_USERNAME=DarthBarada
$ export GITHUB_TOKEN=94f6b47430b12af896a72508a8272fc97d838b94
# входим в workspace и запускаем activate
$ cd ${GITHUB_USERNAME}/workspace
$ pushd .
~/DarthBarada/workspace ~/DarthBarada/workspace
$ source scripts/activate
```

```ShellSession
$ \curl -sSL https://get.rvm.io | bash -s -- --ignore-dotfiles    # Получение и исполнение установочного файла
Turning on ignore dotfiles mode.
Downloading https://github.com/rvm/rvm/archive/master.tar.gz
Installing RVM to /home/darthbarada/.rvm/
Installation of RVM in /home/darthbarada/.rvm/ is almost complete:

  * To start using RVM you need to run `source /home/toliak/.rvm/scripts/rvm`
    in all your open shell windows, in rare cases you need to reopen all shell windows.
  * WARNING: Found --user-install in /etc/gemrc, please remove it, as it will break rubygems in RVM.
    If it is intended or a mistake export rvm_ignore_gemrc_issues=1 to avoid this warning.

Thanks for installing RVM 🙏
Please consider donating to our open collective to help us maintain RVM.

👉  Donate: https://opencollective.com/rvm/donate
$ echo "source $HOME/.rvm/scripts/rvm" >> scripts/activate    # Дописывание в scripts/activate команду для выполнения скрипта запуска rvm
$ . scripts/activate
$ rvm autolibs disable    # Отключение установки зависимостей
# Устанавливаем ruby версии 2.4.2
$ rvm install ruby-2.4.2
Warning, new version of rvm available '1.29.7', you are using older version '1.29.7-next'.
You can disable this warning with:    echo rvm_autoupdate_flag=0 >> ~/.rvmrc
You can enable  auto-update  with:    echo rvm_autoupdate_flag=2 >> ~/.rvmrc
Searching for binary rubies, this might take some time.
No binary rubies available for: kali/kali-rolling/x86_64/ruby-2.4.2.
Continuing with compilation. Please read 'rvm help mount' to get more information on binary rubies.
Installing Ruby from source to: /home/darthbarada/.rvm/rubies/ruby-2.4.2, this may take a while depending on your cpu(s)...
ruby-2.4.2 - #downloading ruby-2.4.2, this may take a while depending on your connection...
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 12.0M  100 12.0M    0     0  4724k      0  0:00:02  0:00:02 --:--:-- 4722k
ruby-2.4.2 - #extracting ruby-2.4.2 to /home/darthbarada/.rvm/src/ruby-2.4.2.....
ruby-2.4.2 - #configuring........................................................-
ruby-2.4.2 - #post-configuration..
ruby-2.4.2 - #compiling..........................................................-
ruby-2.4.2 - #installing............
ruby-2.4.2 - #making binaries executable..
ruby-2.4.2 - #downloading rubygems-3.0.3
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  882k  100  882k    0     0  1459k      0 --:--:-- --:--:-- --:--:-- 1459k
No checksum for downloaded archive, recording checksum in user configuration.
ruby-2.4.2 - #extracting rubygems-3.0.3.....
ruby-2.4.2 - #removing old rubygems........
ruby-2.4.2 - #installing rubygems-3.0.3...................................
ruby-2.4.2 - #gemset created /home/darthbarada/.rvm/gems/ruby-2.4.2@global
ruby-2.4.2 - #importing gemset /home/darthbarada/.rvm/gemsets/global.gems.............-
ruby-2.4.2 - #generating global wrappers.......
ruby-2.4.2 - #gemset created /home/darthbarada/.rvm/gems/ruby-2.4.2
ruby-2.4.2 - #importing gemsetfile /home/darthbarada/.rvm/gemsets/default.gems evaluated to empty gem list
ruby-2.4.2 - #generating default wrappers.......
ruby-2.4.2 - #adjusting #shebangs for (gem irb erb ri rdoc testrb rake).
Install of ruby-2.4.2 - #complete 
Ruby was built without documentation, to build it run: rvm docs generate-ri
$ rvm use 2.4.2 --default     # Установка установленной версии как основной
Using /home/darthbarada/.rvm/gems/ruby-2.4.2
//Устанавливаем travis
$ gem install travis
Fetching multipart-post-2.0.0.gem
Fetching faraday-0.15.4.gem
Fetching faraday_middleware-0.13.1.gem
Fetching highline-1.7.10.gem
Fetching backports-3.13.0.gem
Fetching multi_json-1.13.1.gem
Fetching addressable-2.4.0.gem
Fetching net-http-persistent-2.9.4.gem
Fetching net-http-pipeline-1.0.1.gem
Fetching gh-0.15.1.gem
Fetching launchy-2.4.3.gem
Fetching ffi-1.10.0.gem
Fetching ethon-0.12.0.gem
Fetching typhoeus-0.8.0.gem
Fetching websocket-1.2.8.gem
Fetching pusher-client-0.6.2.gem
Fetching travis-1.8.9.gem
Successfully installed multipart-post-2.0.0
Successfully installed faraday-0.15.4
Successfully installed faraday_middleware-0.13.1
Successfully installed highline-1.7.10
Successfully installed backports-3.13.0
Successfully installed multi_json-1.13.1
Successfully installed addressable-2.4.0
Successfully installed net-http-persistent-2.9.4
Successfully installed net-http-pipeline-1.0.1
Successfully installed gh-0.15.1
Successfully installed launchy-2.4.3
Building native extensions. This could take a while...
Successfully installed ffi-1.10.0
Successfully installed ethon-0.12.0
Successfully installed typhoeus-0.8.0
Successfully installed websocket-1.2.8
Successfully installed pusher-client-0.6.2
Successfully installed travis-1.8.9
invalid options: -SHN
(invalid options are ignored)
Parsing documentation for multipart-post-2.0.0
Installing ri documentation for multipart-post-2.0.0
Parsing documentation for faraday-0.15.4
Installing ri documentation for faraday-0.15.4
Parsing documentation for faraday_middleware-0.13.1
Installing ri documentation for faraday_middleware-0.13.1
Parsing documentation for highline-1.7.10
Installing ri documentation for highline-1.7.10
Parsing documentation for backports-3.13.0
Installing ri documentation for backports-3.13.0
Parsing documentation for multi_json-1.13.1
Installing ri documentation for multi_json-1.13.1
Parsing documentation for addressable-2.4.0
Installing ri documentation for addressable-2.4.0
Parsing documentation for net-http-persistent-2.9.4
Installing ri documentation for net-http-persistent-2.9.4
Parsing documentation for net-http-pipeline-1.0.1
Installing ri documentation for net-http-pipeline-1.0.1
Parsing documentation for gh-0.15.1
Installing ri documentation for gh-0.15.1
Parsing documentation for launchy-2.4.3
Installing ri documentation for launchy-2.4.3
Parsing documentation for ffi-1.10.0
Installing ri documentation for ffi-1.10.0
Parsing documentation for ethon-0.12.0
Installing ri documentation for ethon-0.12.0
Parsing documentation for typhoeus-0.8.0
Installing ri documentation for typhoeus-0.8.0
Parsing documentation for websocket-1.2.8
Installing ri documentation for websocket-1.2.8
Parsing documentation for pusher-client-0.6.2
Installing ri documentation for pusher-client-0.6.2
Parsing documentation for travis-1.8.9
Installing ri documentation for travis-1.8.9
Done installing documentation for multipart-post, faraday, faraday_middleware, highline, backports, multi_json, addressable, net-http-persistent, net-http-pipeline, gh, launchy, ffi, ethon, typhoeus, websocket, pusher-client, travis after 21 seconds
17 gems installed
```

```ShellSession
# Копируем свою lab03 из github в lab04  
$ git clone https://github.com/${GITHUB_USERNAME}/lab03 projects/lab04
loning into 'projects/lab04'...
remote: Enumerating objects: 22, done.
remote: Counting objects: 100% (22/22), done.
remote: Compressing objects: 100% (15/15), done.
remote: Total 22 (delta 2), reused 22 (delta 2), pack-reused 0
Unpacking objects: 100% (22/22), done.
$ cd projects/lab04   # Переход в папку с репозиторием
$ git remote remove origin     # Удаление связки с удаленным репозиторием
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab04      # Добавление связки с новым удаленным репозиторием
```
Настраиваем travis
```ShellSession
$ cat > .travis.yml <<EOF
language: cpp
EOF

$ cat >> .travis.yml <<EOF
script:
- cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install
- cmake --build _build
- cmake --build _build --target install
EOF

$ cat >> .travis.yml <<EOF

addons:
  apt:
    sources:
      - george-edison55-precise-backports
    packages:
      - cmake
      - cmake-data
EOF
```

```
Заходим в travis под своим токеном
$ travis login --github-token ${GITHUB_TOKEN}  
Shell completion not installed. Would you like to install it now? |y| y
Successfully logged in as DarthBarada!
$ travis lint // Проверяем .travis.yml
Warnings for .travis.yml:
[x] value for addons section is empty, dropping
[x] in addons section: unexpected key apt, dropping
```

```ShellSession
$ ex -sc '1i|<фрагмент_вставки_значка>' -cx README.md
```

```ShellSession
$ git add .travis.yml
$ git add README.md
$ git commit -m"added CI"
[master 856d19c] added CI
 2 files changed, 15 insertions(+)
 create mode 100644 .travis.yml
$ git push origin master
Username for 'https://github.com': DarthBarada
Password for 'https://DarthBarada@github.com': 
Enumerating objects: 26, done.
Counting objects: 100% (26/26), done.
Delta compression using up to 4 threads
Compressing objects: 100% (21/21), done.
Writing objects: 100% (26/26), 8.13 KiB | 4.53 MiB/s, done.
Total 26 (delta 4), reused 0 (delta 0)
remote: Resolving deltas: 100% (4/4), done.
To https://github.com/DarthBarada/lab04
 * [new branch]      master -> master
```
Используем команды travis
```ShellSession
$ travis lint
Warnings for .travis.yml:
[x] value for addons section is empty, dropping
[x] in addons section: unexpected key apt, dropping
$ travis accounts
DarthBarada (MIB): subscribed, 10 repositories
$ travis sync
synchronizing: .. done
$ travis repos
DarthBarada/BD (active: no, admin: yes, push: yes, pull: yes)
Description: ???

DarthBarada/Homework02 (active: no, admin: yes, push: yes, pull: yes)
Description: ???

DarthBarada/RK02_TiMP (active: no, admin: yes, push: yes, pull: yes)
Description: Рубежный контроль по ТиМП

DarthBarada/Test-fronts (active: no, admin: yes, push: yes, pull: yes)
Description: Тест шрифтов

DarthBarada/lab00 (active: no, admin: yes, push: yes, pull: yes)
Description: Изучение систем обмена данными

DarthBarada/lab01 (active: no, admin: yes, push: yes, pull: yes)
Description: Изучение утилит для разработки проектов

DarthBarada/lab02 (active: no, admin: yes, push: yes, pull: yes)
Description: ???

DarthBarada/lab03 (active: no, admin: yes, push: yes, pull: yes)
Description: ???

DarthBarada/lab04 (active: yes, admin: yes, push: yes, pull: yes)
Description: ???

DarthBarada/lab05 (active: no, admin: yes, push: yes, pull: yes)
Description: ???

$ travis enable
DarthBarada/lab04: enabled :)
$ travis whatsup
DarthBarada/lab04 passed: #1
$ travis branches
master:  #1    passed     added CI
$ travis history
#1 passed:       master added CI
$ travis show
Job #1.1:  added CI
State:         passed
Type:          push
Branch:        master
Compare URL:   https://github.com/DarthBarada/lab04/compare/67440a2822c9...acc58939d023
Duration:      53 sec
Started:       2019-05-27 17:18:28
Finished:      2019-05-27 17:19:21
Allow Failure: false
Config:        os: linux
```

## Report
Создаем отчёт и отправляем его на github
```ShellSession
$ popd
$ export LAB_NUMBER=04
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gistup -m "lab${LAB_NUMBER}"
```
