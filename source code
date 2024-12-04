
import java.io.*;
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

class User {
    private String username;
    private String password;

    public User(String username, String password) {
        this.username = username;
        this.password = password;
    }

    public String getUsername() {
        return username;
    }

    public String getPassword() {
        return password;
    }
}

class Expense {
    private String category;
    private double amount;
    private String date;

    public Expense(String category, double amount, String date) {
        this.category = category;
        this.amount = amount;
        this.date = date;
    }

    public String getCategory() {
        return category;
    }

    public double getAmount() {
        return amount;
    }

    public String getDate() {
        return date;
    }
}

class Income {
    private String source;
    private double amount;
    private String date;

    public Income(String source, double amount, String date) {
        this.source = source;
        this.amount = amount;
        this.date = date;
    }

    public String getSource() {
        return source;
    }

    public double getAmount() {
        return amount;
    }

    public String getDate() {
        return date;
    }
}

class BudgetManager {
    private List<Expense> expenses;
    private List<Income> incomes;

    public BudgetManager() {
        expenses = new ArrayList<>();
        incomes = new ArrayList<>();
    }

    public void addExpense(String category, double amount, String date) {
        expenses.add(new Expense(category, amount, date));
    }

    public void addIncome(String source, double amount, String date) {
        incomes.add(new Income(source, amount, date));
    }

    public void displayExpenses() {
        for (Expense expense : expenses) {
            System.out.println("Category: " + expense.getCategory() + ", Amount: " + expense.getAmount() + ", Date: " + expense.getDate());
        }
    }

    public void displayIncomes() {
        for (Income income : incomes) {
            System.out.println("Source: " + income.getSource() + ", Amount: " + income.getAmount() + ", Date: " + income.getDate());
        }
    }

    public double calculateBalance() {
        double totalIncome = incomes.stream().mapToDouble(Income::getAmount).sum();
        double totalExpense = expenses.stream().mapToDouble(Expense::getAmount).sum();
        return totalIncome - totalExpense;
    }

    public List<Expense> getExpenses() {
        return expenses;
    }

    public List<Income> getIncomes() {
        return incomes;
    }
}

class FileHandler {
    private static final String EXPENSES_FILE = "expenses.txt";
    private static final String INCOMES_FILE = "incomes.txt";
    private static final String USERS_FILE = "users.txt";

    public static void saveExpenses(List<Expense> expenses) {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(EXPENSES_FILE))) {
            for (Expense expense : expenses) {
                writer.write(expense.getCategory() + "," + expense.getAmount() + "," + expense.getDate());
                writer.newLine();
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    public static void saveIncomes(List<Income> incomes) {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(INCOMES_FILE))) {
            for (Income income : incomes) {
                writer.write(income.getSource() + "," + income.getAmount() + "," + income.getDate());
                writer.newLine();
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    public static void saveUsers(List<User> users) {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(USERS_FILE))) {
            for (User user : users) {
                writer.write(user.getUsername() + "," + user.getPassword());
                writer.newLine();
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    public static void loadExpenses(List<Expense> expenses) {
        try {
            File file = new File(EXPENSES_FILE);
            if (!file.exists()) {
                file.createNewFile();
            }
            try (BufferedReader reader = new BufferedReader(new FileReader(file))) {
                String line;
                while ((line = reader.readLine()) != null) {
                    String[] parts = line.split(",");
                    expenses.add(new Expense(parts[0], Double.parseDouble(parts[1]), parts[2]));
                }
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    public static void loadIncomes(List<Income> incomes) {
        try {
            File file = new File(INCOMES_FILE);
            if (!file.exists()) {
                file.createNewFile();
            }
            try (BufferedReader reader = new BufferedReader(new FileReader(file))) {
                String line;
                while ((line = reader.readLine()) != null) {
                    String[] parts = line.split(",");
                    incomes.add(new Income(parts[0], Double.parseDouble(parts[1]), parts[2]));
                }
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    public static void loadUsers(List<User> users) {
        try {
            File file = new File(USERS_FILE);
            if (!file.exists()) {
                file.createNewFile();
            }
            try (BufferedReader reader = new BufferedReader(new FileReader(file))) {
                String line;
                while ((line = reader.readLine()) != null) {
                    String[] parts = line.split(",");
                    users.add(new User(parts[0], parts[1]));
                }
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}


public class budgetManager{
    private static List<User> users = new ArrayList<>();
    private static User currentUser = null;

    public static void main(String[] args) {
        BudgetManager budgetManager = new BudgetManager();
        Scanner scanner = new Scanner(System.in);

        // Load existing data
        FileHandler.loadExpenses(budgetManager.getExpenses());
        FileHandler.loadIncomes(budgetManager.getIncomes());
        FileHandler.loadUsers(users);

        while (true) {
            if (currentUser == null) {
                System.out.println("1. Register");
                System.out.println("2. Login");
                System.out.print("Choose an option: ");
                int choice = scanner.nextInt();
                scanner.nextLine(); // Consume newline

                switch (choice) {
                    case 1:
                        register(scanner);
                        break;
                    case 2:
                        login(scanner);
                        break;
                    default:
                        System.out.println("Invalid choice. Please try again.");
                }
            } else {
                System.out.println("1. Add Income");
                System.out.println("2. Add Expense");
                System.out.println("3. View Income");
                System.out.println("4. View Expenses");
                System.out.println("5. Calculate Balance");
                System.out.println("6. Save and Exit");
                System.out.print("Choose an option: ");
                int choice = scanner.nextInt();
                scanner.nextLine(); // Consume newline

                switch (choice) {
                    case 1:
                        addIncome(scanner, budgetManager);
                        break;
                    case 2:
                        addExpense(scanner, budgetManager);
                        break;
                    case 3:
                        budgetManager.displayIncomes();
                        break;
                    case 4:
                        budgetManager.displayExpenses();
                        break;
                    case 5:
                        System.out.println("Balance: " + budgetManager.calculateBalance());
                        break;
                    case 6:
                        FileHandler.saveExpenses(budgetManager.getExpenses());
                        FileHandler.saveIncomes(budgetManager.getIncomes());
                        System.out.println("Data saved. Exiting...");
                        return;
                    default:
                        System.out.println("Invalid choice. Please try again.");
                }
            }
        }
    }

    private static void register(Scanner scanner) {
        System.out.print("Enter username: ");
        String username = scanner.nextLine();
        System.out.print("Enter password: ");
        String password = scanner.nextLine();
        users.add(new User(username, password));
        FileHandler.saveUsers(users);
        System.out.println("Registration successful. Please login.");
    }

    private static void login(Scanner scanner) {
        System.out.print("Enter username: ");
        String username = scanner.nextLine();
        System.out.print("Enter password: ");
        String password = scanner.nextLine();

        for (User user : users) {
            if (user.getUsername().equals(username) && user.getPassword().equals(password)) {
                currentUser = user;
                System.out.println("Login successful.");
                return;
            }
        }
        System.out.println("Invalid username or password. Please try again.");
    }

    private static void addIncome(Scanner scanner, BudgetManager budgetManager) {
        System.out.print("Enter source: ");
        String source = scanner.nextLine();
        System.out.print("Enter amount: ");
        double amount = scanner.nextDouble();
        scanner.nextLine(); // Consume newline
        System.out.print("Enter date (YYYY-MM-DD): ");
        String date = scanner.nextLine();
        budgetManager.addIncome(source, amount, date);
    }

    private static void addExpense(Scanner scanner, BudgetManager budgetManager) {
        System.out.print("Enter category: ");
        String category = scanner.nextLine();
        System.out.print("Enter amount: ");
        double amount = scanner.nextDouble();
        scanner.nextLine(); // Consume newline
        System.out.print("Enter date (YYYY-MM-DD): ");
        String date = scanner.nextLine();
        budgetManager.addExpense(category, amount, date);
    }
}
