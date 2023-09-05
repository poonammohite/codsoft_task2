
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

class Student {
    private String name;
    private int rollNumber;
    private String grade;
    private String otherDetails;

    public Student(String name, int rollNumber, String grade, String otherDetails) {
        this.name = name;
        this.rollNumber = rollNumber;
        this.grade = grade;
        this.otherDetails = otherDetails;
    }

    

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getRollNumber() {
        return rollNumber;
    }

    public void setRollNumber(int rollNumber) {
        this.rollNumber = rollNumber;
    }

    public String getGrade() {
        return grade;
    }

    public void setGrade(String grade) {
        this.grade = grade;
    }

    public String getOtherDetails() {
        return otherDetails;
    }

    public void setOtherDetails(String otherDetails) {
        this.otherDetails = otherDetails;
    }
}

class StudentManagementSystem {
    private List<Student> students;

    public StudentManagementSystem() {
        students = new ArrayList<>();
    }

    public void addStudent(Student student) {
        students.add(student);
    }

    public boolean removeStudent(int rollNumber) {
        for (Student student : students) {
            if (student.getRollNumber() == rollNumber) {
                students.remove(student);
                return true;
            }
        }
        return false;
    }

    public Student searchStudent(int rollNumber) {
        for (Student student : students) {
            if (student.getRollNumber() == rollNumber) {
                return student;
            }
        }
        return null;
    }

    public List<Student> getAllStudents() {
        return students;
    }
}

public class main {
    public static void main(String[] args) {
        StudentManagementSystem studentSystem = new StudentManagementSystem();
        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.println("\nStudent Management System");
            System.out.println("1. Add Student");
            System.out.println("2. Remove Student");
            System.out.println("3. Search Student");
            System.out.println("4. Display All Students");
            System.out.println("5. Exit");

            System.out.print("Enter your choice: ");
            int choice = scanner.nextInt();
            scanner.nextLine(); 

            switch (choice) {
                case 1:
                    System.out.print("Enter student name: ");
                    String name = scanner.nextLine();
                    System.out.print("Enter student roll number: ");
                    int rollNumber = scanner.nextInt();
                    scanner.nextLine(); 
                    System.out.print("Enter student grade: ");
                    String grade = scanner.nextLine();
                    System.out.print("Enter other details (optional): ");
                    String otherDetails = scanner.nextLine();
                    Student student = new Student(name, rollNumber, grade, otherDetails);
                    studentSystem.addStudent(student);
                    System.out.println("Student added successfully!");
                    break;

                case 2:
                    System.out.print("Enter student roll number to remove: ");
                    int removeRollNumber = scanner.nextInt();
                    if (studentSystem.removeStudent(removeRollNumber)) {
                        System.out.println("Student removed successfully!");
                    } else {
                        System.out.println("Student not found!");
                    }
                    break;
                    
                case 3:
                    System.out.print("Enter student roll number to search: ");
                    int searchRollNumber = scanner.nextInt();
                    Student foundStudent = studentSystem.searchStudent(searchRollNumber);
                    if (foundStudent != null) {
                        System.out.println("Student found:");
                        System.out.println("Name: " + foundStudent.getName());
                        System.out.println("Roll Number: " + foundStudent.getRollNumber());
                        System.out.println("Grade: " + foundStudent.getGrade());
                        System.out.println("Other Details: " + foundStudent.getOtherDetails());
                    } else {
                        System.out.println("Student not found!");
                    }
                    break;

                case 4:
                    List<Student> allStudents = studentSystem.getAllStudents();
                    System.out.println("All Students:");
                    for (Student s : allStudents) {
                        System.out.println("Name: " + s.getName());
                        System.out.println("Roll Number: " + s.getRollNumber());
                        System.out.println("Grade: " + s.getGrade());
                        System.out.println("Other Details: " + s.getOtherDetails());
                        System.out.println("-----------------------------");
                    }
                    break;

                case 5:
                    System.out.println("Exiting Student Management System.");
                    scanner.close();
                    System.exit(0);
                    break;

                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        }
    }
}

