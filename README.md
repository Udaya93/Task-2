import java.util.Random;
import java.util.Scanner;

public class NumberGuessingGame {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Random random = new Random();

        int minRange = 1;
        int maxRange = 100;
        int maxAttempts = 10;
        int totalRounds = 3;
        int score = 0;

        System.out.println("Welcome to the Number Guessing Game!");

        for (int round = 1; round <= totalRounds; round++) {
            int targetNumber = random.nextInt(maxRange - minRange + 1) + minRange;
            int attempts = 0;

            System.out.println("\nRound " + round + " - Guess the number between " + minRange + " and " + maxRange);

            while (attempts < maxAttempts) {
                System.out.print("Enter your guess (Attempt " + (attempts + 1) + "/" + maxAttempts + "): ");
                int guess = scanner.nextInt();
                attempts++;

                if (guess < minRange || guess > maxRange) {
                    System.out.println("Your guess is out of the valid range.");
                } else if (guess == targetNumber) {
                    System.out.println("Congratulations! You've guessed the correct number in " + attempts + " attempts.");
                    score += calculatePoints(attempts);
                    break;
                } else if (guess < targetNumber) {
                    System.out.println("Try a higher number.");
                } else {
                    System.out.println("Try a lower number.");
                }

                if (attempts == maxAttempts) {
                    System.out.println("Sorry, you've reached the maximum number of attempts. The correct number was " + targetNumber);
                }
            }
        }

        System.out.println("\nGame over! Your total score is: " + score);
        scanner.close();
    }

    private static int calculatePoints(int attempts) {
        // You can customize the scoring logic based on the number of attempts
        // For example, more points for fewer attempts
        if (attempts <= 3) {
            return 10;
        } else if (attempts <= 6) {
            return 5;
        } else {
            return 2;
        }
    }
}
