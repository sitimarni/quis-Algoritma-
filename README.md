import java.util.ArrayList;
import java.util.HashMap;
import java.util.Scanner;
import java.time.LocalDate;
import java.time.Period;

public class hese {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);

        ArrayList<String> names = new ArrayList<String>();
        ArrayList<String> nims = new ArrayList<String>();
        ArrayList<String> majors = new ArrayList<String>();
        ArrayList<Integer> ages = new ArrayList<Integer>();
        ArrayList<String> genders = new ArrayList<String>();

        int numberOfStudents;

        System.out.print("Enter the number of students: ");
        numberOfStudents = input.nextInt();
        input.nextLine();

        for (int i = 1; i <= numberOfStudents; i++) {
            System.out.println("\nEnter the details of student " + i + ":");
            System.out.print("Name: ");
            String name = input.nextLine();
            names.add(name);

            System.out.print("NIM: ");
            String nim = input.nextLine();
            nims.add(nim);

            System.out.print("Major: ");
            String major = input.nextLine();
            majors.add(major);

            System.out.print("Date of Birth (yyyy-mm-dd): ");
            String dateOfBirthString = input.nextLine();
            LocalDate dateOfBirth = LocalDate.parse(dateOfBirthString);
            LocalDate currentDate = LocalDate.now();
            int age = Period.between(dateOfBirth, currentDate).getYears();
            ages.add(age);

            System.out.print("Gender (Male/Female): ");
            String gender = input.nextLine();
            genders.add(gender);
        }

        System.out.println("\n\nStudent Information\n");
        System.out.printf("%-4s| %-30s | %-14s | %-30s | %-3s | %-6s |%n", "No.", "Name", "NIM", "Major", "Age", "Gender");
        System.out.println("=======================================================================================================");
        int numberOfMaleStudents = 0;
        int numberOfFemaleStudents = 0;
        HashMap<String, Integer> majorSummary = new HashMap<>();
        for (int i = 0; i < numberOfStudents; i++) {
            System.out.printf("%-4s| %-30s | %-14s | %-30s | %-3d | %-6s |%n", (i+1), names.get(i), nims.get(i), majors.get(i), ages.get(i), genders.get(i));
            if (genders.get(i).equalsIgnoreCase("male")) {
                numberOfMaleStudents++;
            } else if (genders.get(i).equalsIgnoreCase("female")) {
                numberOfFemaleStudents++;
            }

            String major = majors.get(i);
            if (majorSummary.containsKey(major)) {
                majorSummary.put(major, majorSummary.get(major) + 1);
            } else {
                majorSummary.put(major, 1);
            }
        }
        System.out.println("=======================================================================================================");
        System.out.println("\n\nStudent Summary");
        System.out.println("Number of Male Students: " + numberOfMaleStudents);
        System.out.println("Number of Female Students: " + numberOfFemaleStudents);
        System.out.println("Major Summary:");
        for (String major : majorSummary.keySet()) {
            System.out.printf("%-30s : %-2d%n", major, majorSummary.get(major));
        }

        input.close();
    }
}
