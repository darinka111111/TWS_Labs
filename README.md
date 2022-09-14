# TWS_Labs
Web Services Technologies's labs
Для выполнения лабораторной работы были скачаны и установлены:
1.	Docker
2.	java 11
3.	GlassFish
4.	Postgres
5.	dbeaver
6.	Idea Community Edition
7. JUUDI
8. Java 8
В БД создана таблица Books с полями Title, Authors, ISBN, PublicationDate, Annotation
Запустить docker-compose up -d

Лабораторная работа 1, 2, 3
Запускаем командную строку, переходим в каталог jax-ws-service\standalone\target.
Запускаем файл командой java -jar jaxws-standalone.jar.
Проверяем, что wsdl доступна по адресу http://127.0.0.1:8080/jaxws/BookService?wsdl.
Перейдем в каталог jax-ws-service\client\target. 
Доступно 5 команд - save, find, findById, update, delete. 
По каждой команде можно вывести справку по ключу -h. (Пример команды: save - java -jar client-1.0-SNAPSHOT-shaded.jar save -h). 
Результат выполнения команды отображается в логах.

Для работы с JEE
Запускаем сервер glassfish командой asadmin start-domain admin
Создадим пул подключения к БД, в JDBC Connection Pools
Pool Name: BookPool
Resource Type: javax.sql.DataSource
Datasource Classname: org.postgresql.ds.PGSimpleDataSource
Выбрать BookPool
Driver Classname: org.postgresql.Driver
Перейти на вкладку Additional Properties. По кнопке Add property добавить параметры:
datasourceName: bookDataSource
serverName:localhost
portNumber:5432
databaseName:books
user:secret_user
password:secret_password
Save. Настроить дефолтный пул соединений: 
JDBC -> JDBC Resources
Откроем jdbc/__default.
Pool Name: BookPool
В GlassFish UI, на вкладке Applications задеплоить jee.war из jax-ws-service\jee\target.
Устанавливаем Context Root в значение jaxws.
Проверяем, что по адресу http://localhost:8080/jaxws/BookService?wsdl снова доступна wsdl-схема.
Работа с БД выполняется аналогично Standalone - версии
При введении неверных значений(например пустого Названия книги) - будет ошибка

Лабораторная работа 4, 5, 6
Запускаем командную строку, переходим в каталог jax-rs-service\jax-rs-standalone\target.
Запускаем файл командой java -jar jax-rs-standalone.jar.
Проверяем, что в браузере http://localhost:8080/api/books отобразился список книг.
Перейдем в каталог jax-rs-service\jax-rs-client\target. 
Доступно 5 команд - save, find, findById, update, delete. 
Результат выполнения команды всегда отображается в логах.

Для работы с JEE
Запускаем сервер glassfish командой asadmin start-domain admin
glassfish настроен в предыдущих лабораторных работах
На вкладке Applications деплоим артефакт jax-rs-jee.war из папки jax-rs-service\jax-rs-jee\target
Устанавливаем Context Root в значение api
Проверяем, что по адресу http://localhost:8080/api/books доступен сервис
Работа с БД выполняется аналогично Standalone - версии
При введении неверных значений(например пустого Названия книги) - будет ошибка

Лабораторная работа 7
Скачиваем zip-дистрибутив JUUDI
Переходим в каталог \juddi-distro-3.3.10\juddi-tomcat-3.3.10\bin\
Устанавливаем ссылку на Java 8 SET JAVA_HOME=C:\temurin-1.8.0_322
Выполняем команду catalina.bat run
Открываем пользовательский интерфейс http://localhost:8080/juddi-gui/home.jsp
Вводим login, password
Создаем тестовый бизнес через Create -> Business
Запускаем jaxws-standalone.jar из каталога jax-ws-service/standalone/target
java -jar juudi-cli.jar find --name имя созданного сервиса
Для проверки создания сервиса используем команду java -jar juudi-cli.jar find --name имя созданного сервиса 
Для поиска книги с латинской буквой S в названии, выполним команду: java -jar juudi-cli.jar find --name "Book service" -t=S
