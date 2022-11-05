# Startup WriteUp (Easy)✅

Перейдя по ip адресу, мы обнаруживаем страницу с текстом без каких-либо вкладок

&#x20;

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

Проверка текстового файла **robots.txt** и кода сайта не дала особых подсказок, поэтому используя сканер **nmap** с помощью команды `nmap -sC -sV <ip>` сканируем порты нашей машины

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption><p>📌Добавив в папку <strong>/etc/hosts</strong> ip адрес машины можно присвоить ему название для удобства обращения к нему </p></figcaption></figure>

Благодаря сканеру мы узнаём, что можем подключиться по протоколу **ftp** под именем пользователя **Anonymous**

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption><p>📌В качестве пароля я так же указал слово <strong>Anonymous</strong></p></figcaption></figure>

В данном каталоге мы имеем пустую директорию **/ftp** ( к ней мы вернемся позже), текстовый файл **notice.txt** и **мем**😐

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

Далее, используя инструмент **gobuster** (`gobuster dir -u <ip> -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 100 -x .php)` находим скрытый каталог **/files**

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

Перейдя по нему, можем заметить, что данный каталог мы уже видели&#x20;

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

Используя ftp подключение, попробуем прокинуть в директорию **/ftp** [php\_reverse\_shell](https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php), заранее изменив в нем параметры **$ip** и **$port**

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption><p>📌 <strong></strong> Узнать свой tun0 ip можно, используя команду i<strong>fconfig</strong> в терминале Linux</p></figcaption></figure>

С помощью команды cd переходим в директорию **/ftp** и далее используя команду `put <shell_name.php>` загружаем наш шелл

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

Запустив слушатель в терминале Linux, нажимаем на **.php** файл во вкладке **machine\_ip/files** и затем получаем реверс шелл от лица пользователя **www-data**

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

Выведем с помощью команды `cat` содержимое файла **recipe.txt**, который находится в начальном каталоге и получим первый флаг данной машины 🚩

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>
