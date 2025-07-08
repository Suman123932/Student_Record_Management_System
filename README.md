# Student_Record_Management_System
import java.util.ArrayList;
import java.util.Scanner;

class Student {
    int rollNo;
    String name;
    String course;

    Student(int rollNo, String name, String course) {
        this.rollNo = rollNo;
        this.name = name;
        this.course = course;
    }

    @Override
    public String toString() {
        return "Roll No: " + rollNo + ", Name: " + name + ", Course: " + course;
    }
}

public class StudentManagementSystem {
    static ArrayList<Student> studentList = new ArrayList<>();
    static Scanner sc = new Scanner(System.in);

    public static void main(String[] args) {
        int choice;

        do {
            System.out.println("\n--- Student Record Management System ---");
            System.out.println("1. Add Student");
            System.out.println("2. View All Students");
            System.out.println("3. Delete Student by Roll No");
            System.out.println("4. Update Student by Roll No");
            System.out.println("5. Exit");
            System.out.print("Enter your choice: ");
            choice = sc.nextInt();

            switch (choice) {
                case 1 -> addStudent();
                case 2 -> viewStudents();
                case 3 -> deleteStudent();
                case 4 -> updateStudent();
                case 5 -> System.out.println("Exiting...");
                default -> System.out.println("Invalid choice!");
            }
        } while (choice != 5);
    }

    static void addStudent() {
        System.out.print("Enter Roll No: ");
        int roll = sc.nextInt();
        sc.nextLine();  // Consume newline

        System.out.print("Enter Name: ");
        String name = sc.nextLine();

        System.out.print("Enter Course: ");
        String course = sc.nextLine();

        studentList.add(new Student(roll, name, course));
        System.out.println("Student added successfully!");
    }

    static void viewStudents() {
        if (studentList.isEmpty()) {
            System.out.println("No records found.");
        } else {
            System.out.println("\n-- All Student Records --");
            for (Student s : studentList) {
                System.out.println(s);
            }
        }
    }

    static void deleteStudent() {
        System.out.print("Enter Roll No to delete: ");
        int roll = sc.nextInt();

        boolean removed = studentList.removeIf(s -> s.rollNo == roll);
        if (removed)
            System.out.println("Student deleted successfully.");
        else
            System.out.println("Student not found.");
    }

    static void updateStudent() {
        System.out.print("Enter Roll No to update: ");
        int roll = sc.nextInt();
        sc.nextLine();  // Consume newline

        for (Student s : studentList) {
            if (s.rollNo == roll) {
                System.out.print("Enter new Name: ");
                s.name = sc.nextLine();

                System.out.print("Enter new Course: ");
                s.course = sc.nextLine();

                System.out.println("Student updated successfully.");
                return;
            }
        }
        System.out.println("Student not found.");
    }
}
