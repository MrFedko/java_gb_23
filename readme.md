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

## Урок 2. Функции, манипулирующие данными
[link for lesson 2 programm](src/main/java/ru/geekbrains/lesson2/Program.java)
1. Полностью разобраться с кодом программы разработанной на семинаре, переписать программу. Это минимальная задача для сдачи домашней работы. [✓ done]()

Усложняем задачу:
2. ** Переработать метод проверки победы, логика проверки победы должна работать для поля 5х5 и
количества фишек 4. Очень желательно не делать это просто набором условий для каждой из
возможных ситуаций! Используйте вспомогательные методы, используйте циклы! 
 [✓ done]()

3. **** Доработать искусственный интеллект, чтобы он мог блокировать ходы игрока.


## Урок 3. Классы и объекты
[link for directory](src/main/java/ru/geekbrains/lesson3/)

- Построить три класса ([базовый](src/main/java/ru/geekbrains/lesson3/Worker.java) и 2 потомка), описывающих некоторых [работников с почасовой оплатой](src/main/java/ru/geekbrains/lesson3/HourlyWorker.java) (один из потомков) и [фиксированной оплатой](src/main/java/ru/geekbrains/lesson3/FixedWorker.java) (второй потомок).
  - Описать в базовом классе абстрактный метод для расчёта среднемесячной заработной платы.
  ```java
   public abstract double calculateAverageSalary();
  ```
  Для «повременщиков» формула для расчета такова: «среднемесячная заработная плата = 20.8 * 8 * почасовая ставка», для работников с фиксированной оплатой «среднемесячная заработная плата = фиксированная месячная оплата».
  ```java
    @Override
    public double calculateAverageSalary() {
        return 20.8 * 8 * hourlyRate;
    }
  
    @Override
    public double calculateAverageSalary() {
        return fixedMonthlyPayment;
    }
  ```
  - Создать на базе абстрактного класса массив сотрудников и заполнить его.
  - ** Реализовать интерфейсы для возможности сортировки массива (обратите ваше внимание на интерфейсы Comparator, Comparable)
  - ** Создать класс, содержащий массив сотрудников, и реализовать возможность вывода данных с использованием foreach.
  ```java
  class WorkersArray {
      private Worker[] workers;
  
      public WorkersArray(Worker[] workers) {
          this.workers = workers;
      }
  
      // Метод для сортировки массива работников по имени
      public void sortByName() {
          Arrays.sort(workers, Comparator.comparing(Worker::getName));
      }
  
      // Метод для сортировки массива работников по заработной плате
      public void sortByAverageSalary() {
          Arrays.sort(workers, Comparator.comparing(Worker::calculateAverageSalary));
      }
  
      // Метод для вывода информации о работниках
      public void printWorkersInfo() {
          for (Worker worker : workers) {
              System.out.println("Name: " + worker.getName() + ", Average Salary: " + worker.calculateAverageSalary());
          }
      }
  }
  ```