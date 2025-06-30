# snakewatergun
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>
#include <windows.h> // For Beep()

int getChoiceFromString(char input[]) {
    if (strcmp(input, "snake") == 0)
        return 0;
    else if (strcmp(input, "water") == 0)
        return 1;
    else if (strcmp(input, "gun") == 0)
        return 2;
    else
        return -1; // invalid
}

int main() {
    char input[20];
    int playerChoice, computerChoice;
    int playerScore = 0, computerScore = 0;
    const char *choices[] = {"Snake", "Water", "Gun"};

    srand(time(0)); // Seed random generator

    printf("=== Snake, Water, Gun Game ===\n");
    printf("Type 'snake', 'water', or 'gun' to play.\n");
    printf("Type 'exit' to quit the game.\n\n");

    while (1) {
        // Get user input
        printf("Your choice: ");
        scanf("%s", input);

        // Exit game
        if (strcmp(input, "exit") == 0) {
            printf("\nGame Over!\n");
            printf("Final Score - You: %d | Computer: %d\n", playerScore, computerScore);
            break;
        }

        playerChoice = getChoiceFromString(input);
        if (playerChoice == -1) {
            printf("Invalid input! Please enter 'snake', 'water', or 'gun'.\n");
            Beep(300, 200); // error tone
            continue;
        }

        // Generate computer choice
        computerChoice = rand() % 3;

        // Show choices
        printf("You chose: %s\n", choices[playerChoice]);
        printf("Computer chose: %s\n", choices[computerChoice]);

        // Game logic
        if (playerChoice == computerChoice) {
            printf("It's a Draw!!\n");
            Beep(600, 150); // Draw tone
        }
        else if ((playerChoice == 0 && computerChoice == 1) ||
                 (playerChoice == 1 && computerChoice == 2) ||
                 (playerChoice == 2 && computerChoice == 0)) {
            printf("You Won!!\n");
            Beep(1000, 200); // Win tone
            playerScore++;
        }
        else {
            printf("You Lose!!\n");
            Beep(300, 300); // Lose tone
            computerScore++;
        }

        printf("Score - You: %d | Computer: %d\n\n", playerScore, computerScore);
    }

    return 0;
}
