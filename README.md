import java.util.Scanner;

public class SmartBankingSystem {

    // 1. Abstraction - Interface
    interface BankOperations {
        void deposit(double amount);
        void withdraw(double amount);
        void checkBalance();
        void displayDetails();
    }

    // 2. Base Class - Encapsulation
    static class Account {
        private String accountHolderName;
        private String accountNumber;
        protected double balance;

        public Account(String name, String accNum, double balance) {
            this.accountHolderName = name;
            this.accountNumber = accNum;
            this.balance = balance;
        }

        public String getAccountHolderName() {
            return accountHolderName;
        }

        public String getAccountNumber() {
            return accountNumber;
        }

        public double getBalance() {
            return balance;
        }

        public void setBalance(double balance) {
            this.balance = balance;
        }
    }

    // 3. Inheritance + Polymorphism
    static class SavingsAccount extends Account implements BankOperations {

        public SavingsAccount(String name, String accNum, double balance) {
            super(name, accNum, balance);
        }

        @Override
        public void deposit(double amount) {
            if (amount > 0) {
                balance += amount;
                System.out.println("₹" + amount + " deposited successfully.");
            } else {
                System.out.println("Invalid deposit amount.");
            }
        }

        @Override
        public void withdraw(double amount) {
            if (amount > 0 && amount <= balance) {
                balance -= amount;
                System.out.println("₹" + amount + " withdrawn successfully.");
            } else {
                System.out.println("Invalid or insufficient amount.");
            }
        }

        @Override
        public void checkBalance() {
            System.out.println("Current balance: ₹" + balance);
        }

        @Override
        public void displayDetails() {
            System.out.println("Account Holder: " + getAccountHolderName());
            System.out.println("Account Number: " + getAccountNumber());
            System.out.println("Balance: ₹" + getBalance());
        }
    }

    // 4. Main Method
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        SavingsAccount userAccount = null;

        while (true) {
            System.out.println("\n=== Smart Banking System ===");
            System.out.println("1. Create Account");
            System.out.println("2. Deposit Money");
            System.out.println("3. Withdraw Money");
            System.out.println("4. Check Balance");
            System.out.println("5. Display Account Details");
            System.out.println("6. Exit");
            System.out.print("Choose an option (1-6): ");
            int choice = sc.nextInt();
            sc.nextLine(); // Clear buffer

            switch (choice) {
                case 1:
                    if (userAccount == null) {
                        System.out.print("Enter account holder name: ");
                        String name = sc.nextLine();
                        System.out.print("Enter account number: ");
                        String accNum = sc.nextLine();
                        System.out.print("Enter initial deposit: ");
                        double deposit = sc.nextDouble();
                        userAccount = new SavingsAccount(name, accNum, deposit);
                        System.out.println("Account created successfully!");
                    } else {
                        System.out.println("Account already exists.");
                    }
                    break;

                case 2:
                    if (userAccount != null) {
                        System.out.print("Enter amount to deposit: ");
                        double amount = sc.nextDouble();
                        userAccount.deposit(amount);
                    } else {
                        System.out.println("Please create an account first.");
                    }
                    break;

                case 3:
                    if (userAccount != null) {
                        System.out.print("Enter amount to withdraw: ");
                        double amount = sc.nextDouble();
                        userAccount.withdraw(amount);
                    } else {
                        System.out.println("Please create an account first.");
                    }
                    break;

                case 4:
                    if (userAccount != null) {
                        userAccount.checkBalance();
                    } else {
                        System.out.println("Please create an account first.");
                    }
                    break;

                case 5:
                    if (userAccount != null) {
                        userAccount.displayDetails();
                    } else {
                        System.out.println("Please create an account first.");
                    }
                    break;

                case 6:
                    System.out.println("Thank you for using Smart Banking System!");
                    sc.close();
                    System.exit(0);
                    break;

                default:
                    System.out.println("Invalid choice. Please select 1–6.");
            }
        }
    }
}
 
