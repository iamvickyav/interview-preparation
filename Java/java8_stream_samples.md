# Java Streams Samples for Reference

```java
public class Employee {

    Integer grade;
    String name;
    Integer age;

    // getters and setters
}

List<Employee> employeeList = new ArrayList<>();
employeeList.add(new Employee(3, "Vicky", 25));
employeeList.add(new Employee(3, "Dinesh", 22));
employeeList.add(new Employee(3, "Ganesh", 24));
employeeList.add(new Employee(1, "Ravi", 34));
employeeList.add(new Employee(1, "Sathappan", 33));
employeeList.add(new Employee(2, "Meenakshi", 31));
employeeList.add(new Employee(2, "Mahesh", 30));
```

```java

Map<Integer, List<String>> list1 = employeeList.stream()
.collect(Collectors.groupingBy(Employee::getGrade,
                Collectors.mapping(Employee::getName, Collectors.toList())));

Map<Integer, List<Integer>> list3 = employeeList.stream()
.collect(Collectors.groupingBy(Employee::getGrade,
                Collectors.mapping(Employee::getAge,
                Collectors.toList())));

Map<Integer, Long> collect = employeeList.stream()
.collect(Collectors.groupingBy(Employee::getGrade,
                Collectors.counting()));

Map<Integer, Integer> collect2 = employeeList.stream()
.collect(Collectors.groupingBy(Employee::getGrade,
                Collectors.collectingAndThen(Collectors.counting(),
                Long::intValue)));

Map<Integer, List<Employee>> list2 = employeeList.stream()
.collect(Collectors.groupingBy(Employee::getGrade));

```
