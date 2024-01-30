# Мониторинг с помощью Zabbix

В рамках проекта создан демо стенд Vagrant  
подготовлен docker-compose.yaml файл, который развёртывает на тестовом стенде контейнеры с необходимыми службами Zabbix:  
  - web-zabbix;  
  - zabbix-server;  
  - mariaDB (сервер базы данных).  
На хостовом сервере устанавливается агент Zabbix для отслеживания параметров серевера:  
  - CPU;  
  - Memory;  
  - Disk;  
  - Network.  
По завершению развертывания и запуска стенда (старт всех сервисов может занять несколько минут) можно подключиться к веб-консоли  Zabbix указав в адресной строке браузера http://localhost:8080  
Для выполнения задачи ДЗ, с помощью веб-консоли был добавлен сервер vagrant_host для отслеживания его параметров, а так же создан дашборд (его вид представлен на скрине)  
<image scr="./screens/dashboard.jpg" alt="Dashboard">
<image scr="https://github.com/gkronalf/monitoring/blob/8b434d76f8584bfc224ecfefc96d2c4e72b0273d/screens/dashboard.jpg" alt="Dashboard">
