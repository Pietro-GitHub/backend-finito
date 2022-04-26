Per far funzionare il Backend bisogna utilizzare Docker.

Per un facile utilizzo consiglio di installare Docker Desktop, a questo link: https://www.docker.com/products/docker-desktop/
o cercando semplicemente Docker su internet e andare nella sezione Docker Desktop o quella che preferiamo, sarà seguita una procedura guidata per l'installazione.
Windows ha bisogno di WSL (Windows Subsystem for Linux) per il corretto funzionamento, durante l'installazione di Docker, si dovrebbe apparire la procedura guidata per instarlarlo, nel caso questo è il link: https://docs.microsoft.com/it-it/windows/wsl/install-manual basta seguire la procedura guidata.

Dopo di che bisogna andare nel CMD e avviare i container di MySQL e Apache.

1) Scaricare il file (create_employee.sql)
2) Metterlo in una cartella di nome "dump", per esempio nel Desktop
3) Avviare il container "my-mysql-server" tramite i comand:
    docker run --name my-mysql-server --rm -v /home/informatica/mysqldata:/var/lib/mysql -v /home/informatica/dump:/dump -e MYSQL_ROOT_PASSWORD=my-secret-pw -p 3306:3306 -d mysql:latest

Al posto di "/home/informatica" inserire il percorso della cartella "dump", in entrambi i punti, nel secondo punto senza ripetere due volte "/dump".

Altro comando:
docker exec -it my-mysql-server bash

Altro comando:
mysql -u root -p < /dump/create_employee.sql; exit;

In seguito le sarà chiesto di inserire la password, la password è questa:
my-secret-pw

4) Avviare un webserver dockerizzato con il seguente comando:
    docker run -d -p 8080:80 --name my-apache-php-app --rm  -v /home/informatica/mio-sito:/var/www/html zener79/php:7.4-apache

Anche qui al posto di "/home/informatica" dovrà mettere il percorso di dove ha salvato la cartella "mio-sito".