# Scheduletask
my schedule 



import java.util.ArrayList;
import java.util.Scanner;

public class DailyScheduler {

    private static ArrayList<Task> tasks = new ArrayList<>();
    private static Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {
        boolean exit = false;

        while (!exit) {
            System.out.println("\n=== Daily Scheduler Menu ===");
            System.out.println("1. Add Task");
            System.out.println("2. Mark Task as Completed");
            System.out.println("3. View To-Do List");
            System.out.println("4. Exit");
            System.out.print("Enter your choice: ");

            int choice = scanner.nextInt();
            scanner.nextLine(); // Consume newline

            switch (choice) {
                case 1:
                    addTask();
                    break;
                case 2:
                    markTaskAsCompleted();
                    break;
                case 3:
                    viewToDoList();
                    break;
                case 4:
                    exit = true;
                    break;
                default:
                    System.out.println("Invalid choice. Please enter a number from 1 to 4.");
            }
        }

        System.out.println("Exiting Daily Scheduler. Have a nice day!");
        scanner.close();
    }

    private static void addTask() {
        System.out.print("Enter task description: ");
        String description = scanner.nextLine();
        tasks.add(new Task(description));
        System.out.println("Task added successfully!");
    }

    private static void markTaskAsCompleted() {
        if (tasks.isEmpty()) {
            System.out.println("No tasks to mark as completed.");
            return;
        }

        System.out.println("Tasks:");
        for (int i = 0; i < tasks.size(); i++) {
            System.out.println((i + 1) + ". " + tasks.get(i));
        }

        System.out.print("Enter the number of the task to mark as completed: ");
        int index = scanner.nextInt() - 1;
        scanner.nextLine(); // Consume newline

        if (index < 0 || index >= tasks.size()) {
            System.out.println("Invalid task number.");
        } else {
            Task task = tasks.get(index);
            task.setCompleted(true);
            System.out.println("Task marked as completed: " + task.getDescription());
        }
    }

    private static void viewToDoList() {
        if (tasks.isEmpty()) {
            System.out.println("To-Do List is empty.");
        } else {
            System.out.println("=== To-Do List ===");
            for (int i = 0; i < tasks.size(); i++) {
                Task task = tasks.get(i);
                String status = task.isCompleted() ? "Completed" : "Pending";
                System.out.println((i + 1) + ". " + task.getDescription() + " - " + status);
            }
        }
    }

    private static class Task {
        private String description;
        private boolean completed;

        public Task(String description) {
            this.description = description;
            this.completed = false;
        }

        public String getDescription() {
            return description;
        }

        public boolean isCompleted() {
            return completed;
        }

        public void setCompleted(boolean completed) {
            this.completed = completed;
        }

        @Override
        public String toString() {
            return description;
        }
    }
}
