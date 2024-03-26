java
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class VegetableStore {
    private static int idCounter = 1;
    private static List<Vegetable> seedlings = new ArrayList<>();

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        boolean running = true;

        while (running) {
            System.out.println("--- Vegetable Store ---");
            System.out.println("1. Просмотр рассады овощей");
            System.out.println("2. Добавление растения");
            System.out.println("3. Выход");
            System.out.print("Выберите действие: ");

            int choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    displaySeedlings();
                    break;
                case 2:
                    addPlant(scanner);
                    break;
                case 3:
                    running = false;
                    break;
                default:
                    System.out.println("Недопустимый выбор. Попробуйте еще раз.");
                    break;
            }
            System.out.println();
        }
    }

    private static void displaySeedlings() {
        if (seedlings.isEmpty()) {
            System.out.println("Рассада овощей отсутствует.");
        } else {
            System.out.println("--- Рассада овощей ---");
            for (Vegetable vegetable : seedlings) {
                System.out.println(vegetable);
            }
        }
    }

    private static void addPlant(Scanner scanner) {
        System.out.print("Введите название овоща: ");
        String name = scanner.next();
        System.out.print("Введите описание овоща: ");
        String description = scanner.next();
        long timeToHarvest = (long)(Math.random() * 15000); // Генерация случайного числа от 0 до 15000
        Vegetable vegetable = new Vegetable(idCounter++, name, description, timeToHarvest);
        seedlings.add(vegetable);
        System.out.println("Растение успешно добавлено в рассаду.");
    }
}

class Vegetable {
    private int id;
    private String name;
    private String description;
    private long timeToHarvest;

    public Vegetable(int id, String name, String description, long timeToHarvest) {
        this.id = id;
        this.name = name;
        this.description = description;
        this.timeToHarvest = timeToHarvest;
    }

    @Override
    public String toString() {
        return "ID: " + id + ", Название: " + name + ", Описание: " + description + ", Срок созревания: " + timeToHarvest/1000 + " сек";
    }
}
