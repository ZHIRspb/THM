# Watcher WriteUp (Medium)✅

Перейдя по ip адресу, мы видим страницу с подставками (?) для посуды

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

Проверив файл **robots.txt**, мы обнаруживаем 2 файла

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

В файле **flag\_1.txt** находится первый флаг

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

Во втором файле находится записка, но мы не можем прочитать её содержимое, просто перейдя в него с помощью адресной строки

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

Нажав на картинку на основной странице, в адресной строке появляется html-запрос, используя его, прочитаем содержимое файла **secret\_file\_do\_not\_read.txt**

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

В данной записке находится логин и пароль для подключения по протоколу ftp&#x20;

<figure><img src="../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

Используя логин и пароль из записки, подключаемся к машине и скачиваем файл **flag\_2.txt**

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

Выводим содержимое данного файла и получаем второй флаг

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>
