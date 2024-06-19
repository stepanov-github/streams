# Задача 1: Работа с числами

## Класс 'Main'
```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<Integer> intList = List.of(1, 2, 5, 16, -1, -2, 0, 32, 3, 5, 8, 23, 4);

        List<Integer> correctNumbers = new ArrayList<>();
        for (int num : intList) {
            if (num > 0) {
                correctNumbers.add(num);
            }
        }

        List<Integer> evenNumbers = new ArrayList<>();
        for (int num : correctNumbers) {
            if (num % 2 == 0) {
                evenNumbers.add(num);
            }
        }

        Collections.sort(evenNumbers);

        for (int num : evenNumbers) {
            System.out.print(num + " ");
        }
    }
}
```

## Класс 'StreamMain' 
```java
import java.util.Arrays;
import java.util.List;

public class StreamMain {
    public static void main(String[] args) {
        List<Integer> intList = Arrays.asList(1, 2, 5, 16, -1, -2, 0, 32, 3, 5, 8, 23, 4);

        List<Integer> result = intList.stream()
                .filter(x -> x > 0)
                .filter(x -> x % 2 == 0)
                .sorted()
                .toList();

        result.forEach(num -> System.out.print(num + " "));
    }
}

```
