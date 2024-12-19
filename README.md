import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class QuizGame {

    static class Question {
        private final String question;
        private final String[] options;
        private final int correctAnswerIndex;

        public Question(String question, String[] options, int correctAnswerIndex) {
            this.question = question;
            this.options = options;
            this.correctAnswerIndex = correctAnswerIndex;
        }

        public String getQuestion() {
            return question;
        }

        public String[] getOptions() {
            return options;
        }

        public boolean isAnswerCorrect(int answerIndex) {
            return answerIndex == correctAnswerIndex;
        }
    }

    public static void main(String[] args) {
        List<Question> questions = new ArrayList<>();
        questions.add(new Question("What is the capital of France?", new String[]{"1. Paris", "2. London", "3. Berlin", "4. Madrid"}, 0));
        questions.add(new Question("What is 2 + 2?", new String[]{"1. 3", "2. 4", "3. 5", "4. 6"}, 1));
        questions.add(new Question("What is the largest ocean?", new String[]{"1. Atlantic", "2. Indian", "3. Arctic", "4. Pacific"}, 3));

        Scanner scanner = new Scanner(System.in);
        int score = 0;

        System.out.println("Welcome to the Quiz Game!");
        System.out.println("You will be asked 3 questions. Choose the correct option by typing the number.");

        for (int i = 0; i < questions.size(); i++) {
            Question question = questions.get(i);

            System.out.println("\nQuestion " + (i + 1) + ": " + question.getQuestion());
            for (String option : question.getOptions()) {
                System.out.println(option);
            }

            System.out.print("Your answer (1-4): ");
            int userAnswer = scanner.nextInt() - 1;

            if (userAnswer >= 0 && userAnswer < question.getOptions().length) {
                if (question.isAnswerCorrect(userAnswer)) {
                    System.out.println("Correct!");
                    score++;
                } else {
                    System.out.println("Incorrect. The correct answer was option " + (question.correctAnswerIndex + 1) + ".");
                }
            } else {
                System.out.println("Invalid option. Please choose a number between 1 and 4.");
            }
        }

        System.out.println("\nGame Over!");
        System.out.println("Your score: " + score + "/" + questions.size());

        scanner.close();
    }
}
