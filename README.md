# coderscave-golden-task
import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;

class Student {
    private String name;
    private int studentId;
    private double feesPaid;
    private double totalFees;

    public Student(String name, int studentId, double totalFees) {
        this.name = name;
        this.studentId = studentId;
        this.totalFees = totalFees;
        this.feesPaid = 0;
    }

    public void payFees(double amount) {
        feesPaid += amount;
    }

    public String getName() {
        return name;
    }

    public int getStudentId() {
        return studentId;
    }

    public double getFeesPaid() {
        return feesPaid;
    }

    public double getTotalFees() {
        return totalFees;
    }

    public double getRemainingFees() {
        return totalFees - feesPaid;
    }
}

class FeesManagementSystem {
    private Map<Integer, Student> students;

    public FeesManagementSystem() {
        students = new HashMap<>();
    }

    public void addStudent(String name, int studentId, double totalFees) {
        students.put(studentId, new Student(name, studentId, totalFees));
    }

    public Student findStudent(int studentId) {
        return students.getOrDefault(studentId, null);
    }

    public void collectFees(int studentId, double amount) {
        Student student = findStudent(studentId);
        if (student != null) {
            student.payFees(amount);
            System.out.println("Payment of " + amount + " received from " + student.getName());
        } else {
            System.out.println("Student not found.");
        }
    }

    public void displayStudentDetails(int studentId) {
        Student student = findStudent(studentId);
        if (student != null) {
            System.out.println("Student ID: " + student.getStudentId());
            System.out.println("Student Name: " + student.getName());
            System.out.println("Total Fees: " + student.getTotalFees());
            System.out.println("Fees Paid: " + student.getFeesPaid());
            System.out.println("Remaining Fees: " + student.getRemainingFees());
        } else {
            System.out.println("Student not found.");
        }
    }
}

public class Main {
    public static void main(String[] args) {
        FeesManagementSystem system = new FeesManagementSystem();
        system.addStudent("John Doe", 1001, 5000);
        system.addStudent("Jane Smith", 1002, 6000);

        Scanner scanner = new Scanner(System.in);
        int choice;

        do {
            System.out.println("\nFees Management System Menu");
            System.out.println("1. Pay Fees");
            System.out.println("2. Display Student Details");
            System.out.println("3. Exit");
            System.out.print("Enter your choice: ");
            choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    System.out.print("Enter student ID: ");
                    int id = scanner.nextInt();
                    System.out.print("Enter amount to pay: ");
                    double amount = scanner.nextDouble();
                    system.collectFees(id, amount);
                    break;
                case 2:
                    System.out.print("Enter student ID: ");
                    int studentId = scanner.nextInt();
                    system.displayStudentDetails(studentId);
                    break;
                case 3:
                    System.out.println("Exiting...");
                    break;
                default:
                    System.out.println("Invalid choice. Try again.");
            }
        } while (choice != 3);

        scanner.close();
    }
}
