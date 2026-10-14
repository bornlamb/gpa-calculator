# gpa-calculator
Java command-line tool that calculates a credit-weighted GPA and the minimum final exam score needed to hit a target grade.


import java.util.Scanner;

public class GpaCalc {

    static double points(String grade) {
        switch (grade.toUpperCase()) {
            case "A":  return 4.0;
            case "A-": return 3.7;
            case "B+": return 3.3;
            case "B":  return 3.0;
            case "B-": return 2.7;
            case "C+": return 2.3;
            case "C":  return 2.0;
            case "D":  return 1.0;
            default:   return 0.0;
        }
    }

    // target = current*(1 - w) + x*w   ->   solve for x
    static double neededOnFinal(double current, double w, double target) {
        return (target - current * (1 - w)) / w;
    }

    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);

        System.out.print("How many courses? ");
        int n = in.nextInt();
        double totalPoints = 0;
        int totalCredits = 0;

        for (int i = 1; i <= n; i++) {
            System.out.print("Course " + i + " credits: ");
            int credits = in.nextInt();
            System.out.print("Course " + i + " grade (A, A-, B+...): ");
            String grade = in.next();
            totalPoints += points(grade) * credits;
            totalCredits += credits;
        }
        System.out.printf("Your GPA: %.2f%n", totalPoints / totalCredits);

        System.out.print("Current class grade (%): ");
        double current = in.nextDouble();
        System.out.print("Final exam weight (e.g. 0.30): ");
        double w = in.nextDouble();
        System.out.print("Grade you want (%): ");
        double target = in.nextDouble();

        System.out.printf("You need %.1f%% on the final.%n",
                neededOnFinal(current, w, target));
    }
}
