# Java Streams Samples for Reference

### POJO
```java
public class Employee {

    Integer grade;
    String name;
    Integer age;

    // getters and setters
}
```

### Data Setup
```java
List<Employee> employeeList = new ArrayList<>();
employeeList.add(new Employee(3, "Vicky", 25));
employeeList.add(new Employee(3, "Dinesh", 22));
employeeList.add(new Employee(3, "Ganesh", 24));
employeeList.add(new Employee(1, "Ravi", 34));
employeeList.add(new Employee(1, "Sathappan", 33));
employeeList.add(new Employee(2, "Meenakshi", 31));
employeeList.add(new Employee(2, "Mahesh", 30));
```

### Stream Samples
```java

Map<Integer, List<Employee>> employeeGradeMap = employeeList.stream()
    .collect(Collectors.groupingBy(Employee::getGrade));

Map<Integer, List<String>> employeeNameListGroupedByGrade = employeeList.stream()
    .collect(Collectors.groupingBy(Employee::getGrade,
                Collectors.mapping(Employee::getName, Collectors.toList())));

Map<Integer, List<Integer>> employeeAgeListGroupedByGrade = employeeList.stream()
    .collect(Collectors.groupingBy(Employee::getGrade,
                Collectors.mapping(Employee::getAge,
                Collectors.toList())));

Map<Integer, Long> employeeCountAsLongBasedOnGrade = employeeList.stream()
    .collect(Collectors.groupingBy(Employee::getGrade,
                Collectors.counting()));

Map<Integer, Integer> employeeCountAsIntegerBasedOnGrade = employeeList.stream()
    .collect(Collectors.groupingBy(Employee::getGrade,
                Collectors.collectingAndThen(Collectors.counting(),
                Long::intValue)));

```
