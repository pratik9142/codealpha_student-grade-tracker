# codealpha_student-grade-tracker
import java.util.Scanner;

public class StudentGradeManager {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Input number of students
        System.out.print("Enter the number of students: ");
        int numStudents = scanner.nextInt();
        scanner.nextLine(); // Consume newline

        String[] studentNames = new String[numStudents];
        double[] studentGrades = new double[numStudents];

        // Input names and grades
        for (int i = 0; i < numStudents; i++) {
            System.out.print("Enter name of student " + (i + 1) + ": ");
            studentNames[i] = scanner.nextLine();

            System.out.print("Enter grade for " + studentNames[i] + ": ");
            while (true) {
                try {
                    studentGrades[i] = Double.parseDouble(scanner.nextLine());
                    if (studentGrades[i] < 0 || studentGrades[i] > 100) {
                        throw new NumberFormatException();
                    }
                    break;
                } catch (NumberFormatException e) {
                    System.out.print("Invalid grade! Please enter a number between 0 and 100: ");
                }
            }
        }

        // Calculate statistics
        double total = 0;
        double highest = studentGrades[0];
        double lowest = studentGrades[0];
        int highestIndex = 0;
        int lowestIndex = 0;

        for (int i = 0; i < numStudents; i++) {
            double grade = studentGrades[i];
            total += grade;

            if (grade > highest) {
                highest = grade;
                highestIndex = i;
            }

            if (grade < lowest) {
                lowest = grade;
                lowestIndex = i;
            }
        }

        double average = total / numStudents;

        // Display summary report
        System.out.println("\n--- Summary Report ---");
        System.out.printf("Average Grade: %.2f\n", average);
        System.out.println("Highest Grade: " + studentNames[highestIndex] + " - " + highest);
        System.out.println("Lowest Grade: " + studentNames[lowestIndex] + " - " + lowest);

        System.out.println("\nAll Students:");
        for (int i = 0; i < numStudents; i++) {
            System.out.println(studentNames[i] + " - " + studentGrades[i]);
        }

        scanner.close();
    }
}
