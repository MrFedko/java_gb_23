## Урок 1. Компиляция и интерпретация кода

Создать [проект из трёх классов](/src/main/java/ru/geekbrains/lesson1) (основной с точкой входа и два класса в другом пакете),
которые вместе должны составлять одну программу, позволяющую
производить четыре основных математических действия и осуществлять форматированный
вывод результатов пользователю (ИЛИ ЛЮБОЕ ДРУГОЕ ПРИЛОЖЕНИЕ НА ВАШ ВЫБОР, которое просто демонстрирует работу некоторого механизма).

- Необходимо установить Docker Desktop.
- Создать [Dockerfile](/src/main/dockerfile), позволяющий откопировать исходный код вашего приложения в образ для демонстрации работы вашего приложения при создании соответствующего контейнера.
```dockerfile
FROM bellsoft/liberica-openjdk-alpine:latest
COPY ./java ./src
RUN mkdir ./out
RUN javac -sourcepath ./src -d out src/ru/geekbrains/lesson1/sample/Main.java
CMD java -classpath ./out ru.geekbrains.lesson1.sample.Main
```