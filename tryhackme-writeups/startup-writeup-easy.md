# Startup WriteUp (Easy)✅

Перейдя по ip адресу, мы обнаруживаем страницу с текстом без каких-либо вкладок

&#x20;

<figure><img src="../.gitbook/assets/image (4) (2).png" alt=""><figcaption></figcaption></figure>

Проверка текстового файла **robots.txt** и кода сайта не дала особых подсказок, поэтому используя сканер **nmap** с помощью команды `nmap -sC -sV <ip>` сканируем порты нашей машины

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption><p>📌Добавив в папку <strong>/etc/hosts</strong> ip адрес машины можно присвоить ему название для удобства обращения к нему </p></figcaption></figure>

Благодаря сканеру мы узнаём, что можем подключиться по протоколу **ftp** под именем пользователя **Anonymous**

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption><p>📌В качестве пароля я так же указал слово <strong>Anonymous</strong></p></figcaption></figure>

В данном каталоге мы имеем пустую директорию **/ftp** (к ней мы вернемся позже), текстовый файл **notice.txt** и **мем**😐

<figure><img src="../.gitbook/assets/image (2) (3).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (3) (3).png" alt=""><figcaption></figcaption></figure>

Далее, используя инструмент **gobuster** (`gobuster dir -u <ip> -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 100 -x .php)` находим скрытый каталог **/files**

<figure><img src="../.gitbook/assets/image (5) (3).png" alt=""><figcaption></figcaption></figure>

Перейдя по нему, можем заметить, что данный каталог мы уже видели&#x20;

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

Используя ftp подключение, попробуем прокинуть в директорию **/ftp** [php\_reverse\_shell](https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php), заранее изменив в нем параметры **$ip** и **$port**

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption><p>📌 <strong></strong> Узнать свой tun0 ip можно, используя команду i<strong>fconfig</strong> в терминале Linux</p></figcaption></figure>

С помощью команды cd переходим в директорию **/ftp** и далее используя команду `put <shell_name.php>` загружаем наш шелл

<figure><img src="../.gitbook/assets/image (9) (1).png" alt=""><figcaption></figcaption></figure>

Запустив слушатель в терминале Linux, нажимаем на **.php** файл во вкладке **machine\_ip/files** и затем получаем реверс шелл от лица пользователя **www-data**

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

Выведем с помощью команды `cat` содержимое файла **recipe.txt**, который находится в начальном каталоге и получим первый флаг данной машины 🚩

<figure><img src="../.gitbook/assets/image (6) (2).png" alt=""><figcaption></figcaption></figure>

Второй флаг по заданию находится в текстовом файле **user.txt**, к котором мы не имеем доступ от лица пользователя **www-data**, следовательно, нужно получить данные пользователя, от лица которого мы сможем вывести содержимое нужного нам файла

Просмотрев корневую директорию, можем найти интересную папку **/incidents**, в которой находится файл **suspicious.pcapng**&#x20;

<figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

Перейдя в папку **/incidents** и используя **python3**, с помощью команды `python3 -m http.server` поднимаем сервер и скачиваем нужный нам файл с помощью команды `wget http://<ip_machine>:8000/suspicious.pcapng`

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

Данный файл содержит в себе дамп сетевых пакетов, перехваченных программами-анализаторами (например **WireShark**)

Найдя самый "большой" TCP пакет, просмотрим его содержимое с помощью **TCP Stream**'a

<figure><img src="../.gitbook/assets/image (7) (2).png" alt=""><figcaption></figcaption></figure>

В нем находим имя пользователя **lennie** и, вероятнее всего, пароль к нему **c4ntg3t3n0ughsp1c3**

<figure><img src="../.gitbook/assets/image (4) (3).png" alt=""><figcaption></figcaption></figure>

Нам остаётся лишь подключиться по протоколу ssh от лица пользователя **lennie** и прочитать содержимое файла **user.txt** 🚩

<figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>
