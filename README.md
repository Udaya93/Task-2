# OTask-1
import java.util.Scanner;
import java.util.Random;

public class NumberGuessingGame {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Random random = new Random();

        int minRange = 1;
        int maxRange = 100;
        int maxAttempts = 10;
        int score = 0;

        System.out.println("Welcome to the Number Guessing Game!");

        boolean playAgain;

        do {
            playRound(scanner, random, minRange, maxRange, maxAttempts);
            score++;

            System.out.print("Do you want to play again? (yes/no): ");
            playAgain = scanner.next().equalsIgnoreCase("yes");

        } while (playAgain);

        System.out.println("Game over! Your total score is: " + score);
        scanner.close();
    }

    private static void playRound(Scanner scanner, Random random, int minRange, int maxRange, int maxAttempts) {
        int targetNumber = random.nextInt(maxRange - minRange + 1) + minRange;
        int attempts = 0;

        System.out.println("Round " + (score + 1));

        while (attempts < maxAttempts) {
            int guess = getValidGuess(scanner, minRange, maxRange);
            attempts++;

            if (guess == targetNumber) {
                System.out.println("Congratulations! You've guessed the correct number in " + attempts + " attempts.");
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

    private static int getValidGuess(Scanner scanner, int minRange, int maxRange) {
        int guess;

        while (true) {
            System.out.print("Enter your guess: ");
            guess = scanner.nextInt();

            if (guess < minRange || guess > maxRange) {
                System.out.println("Your guess is out of the valid range.");
            } else {
                break;
            }
        }
         
        return guess;
    }
}
