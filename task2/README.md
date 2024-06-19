# Задача 2: Работяга

## Класс `Main`
```java
import java.util.*;


public class Main {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Jack", "Connor", "Harry", "George", "Samuel", "John");
        List<String> families = Arrays.asList("Evans", "Young", "Harris", "Wilson", "Davies", "Adamson", "Brown");
        Collection<Person> persons = new ArrayList<>();
        for (int i = 0; i < 10_000_000; i++) {
            persons.add(new Person(
                    names.get(new Random().nextInt(names.size())),
                    families.get(new Random().nextInt(families.size())),
                    new Random().nextInt(100),
                    Sex.values()[new Random().nextInt(Sex.values().length)],
                    Education.values()[new Random().nextInt(Education.values().length)])
            );
        }

        long kinders = persons.stream()
                .filter(person -> person.getAge() < 18)
                .count();
        System.out.printf("Количество несовершеннолетних - %s \n", kinders);

        List<String> soldiers = persons.stream()
                .filter(person -> person.getAge() >= 18 && person.getAge() <= 27 && person.getSex() == Sex.MAN)
                .map(Person::getFamily)
                .toList();
        System.out.printf("Список призывников: %s \n", soldiers);

        List<Person> workers = persons.stream()
                .filter(person -> (person.getSex() == Sex.MAN && person.getAge() >= 18 && person.getAge() <= 65 && person.getEducation() == Education.HIGHER)
                        || (person.getSex() == Sex.WOMAN && person.getAge() >= 18 && person.getAge() <= 60) && person.getEducation() == Education.HIGHER)
                .sorted(Comparator.comparing(Person::getFamily))
                .toList();
        System.out.println("\n Пофамильный отсортированный список работоспособных людей: \n");
        for (Person per : workers) {
            System.out.println(per);
        }
    }
}
```

## Класс `Sex`
```java
public enum Sex {
    MAN,
    WOMAN
}
```

## Класс `Education`
```java
public enum Education {
    ELEMENTARY,
    SECONDARY,
    FURTHER,
    HIGHER
}
```

## Класс `Person`
```java
class Person {
    private String name;
    private String family;
    private Integer age;
    private Sex sex;
    private Education education;

    public Person(String name, String family, int age, Sex sex, Education education) {
        this.name = name;
        this.family = family;
        this.age = age;
        this.sex = sex;
        this.education = education;
    }

    public String getName() {
        return name;
    }

    public String getFamily() {
        return family;
    }

    public Integer getAge() {
        return age;
    }

    public Sex getSex() {
        return sex;
    }

    public Education getEducation() {
        return education;
    }

    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", family='" + family + '\'' +
                ", age=" + age +
                ", sex=" + sex +
                ", education=" + education +
                '}';
    }
}
```
