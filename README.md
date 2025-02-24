import java.io.*;
import java.util.*;

public class ExpenseTracker {
    private static final String FILE_NAME = "expenses.txt";
    private static double balance = 0.0;
    
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        loadBalance();

        int choice;
        do {
            System.out.println("\n==== Expense Tracker ====");
            System.out.println("1. Add Expense");
            System.out.println("2. Add Income");
            System.out.println("3. View Balance");
            System.out.println("4. Exit");
            System.out.print("Enter choice: ");
            choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    System.out.print("Enter expense amount: ");
                    double expense = scanner.nextDouble();
                    balance -= expense;
                    saveBalance();
                    System.out.println("Expense added!");
                    break;
                case 2:
                    System.out.print("Enter income amount: ");
                    double income = scanner.nextDouble();
                    balance += income;
                    saveBalance();
                    System.out.println("Income added!");
                    break;
                case 3:
                    System.out.println("Current Balance: $" + balance);
                    break;
                case 4:
                    System.out.println("Exiting...");
                    break;
                default:
                    System.out.println("Invalid choice, try again.");
            }
        } while (choice != 4);
        scanner.close();
    }

    private static void loadBalance() {
        try (BufferedReader br = new BufferedReader(new FileReader(FILE_NAME))) {
            balance = Double.parseDouble(br.readLine());
        } catch (Exception e) {
            balance = 0.0;
        }
    }

    private static void saveBalance() {
        try (BufferedWriter bw = new BufferedWriter(new FileWriter(FILE_NAME))) {
            bw.write(String.valueOf(balance));
        } catch (IOException e) {
            System.out.println("Error saving balance.");
        }
    }
}
