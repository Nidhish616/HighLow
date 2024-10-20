# HighLow
#include <stdio.h>
#include <time.h>

#define MAX 100
#define MAX_TRIALS 3


struct Stack {
    int items[MAX];
    int top;
};

void initStack(struct Stack* s) {
    s->top = -1;
}

int isFull(struct Stack* s) {
    return s->top == MAX - 1;
}

int isEmpty(struct Stack* s) {
    return s->top == -1;
}

void push(struct Stack* s, int value) {
    if (isFull(s)) {
        printf("Stack is full!\n");
    } else {
        s->items[++(s->top)] = value;
    }
}

int pop(struct Stack* s) {
    if (isEmpty(s)) {
        printf("Stack is empty!\n");
        return -1;
    } else {
        return s->items[(s->top)--];
    }
}

int peek(struct Stack* s) {
    if (isEmpty(s)) {
        printf("Stack is empty!\n");
        return -1;
    } else {
        return s->items[s->top];
    }
}

int main() {
    struct Stack numbers;
    initStack(&numbers);
    char guess;
    int current, next, score = 0;
    int trials = 0;  // Counter to track number of trials

    srand(time(0));

    current = rand() % 100 + 1;
    push(&numbers, current);
    printf("Welcome to the High-Low Game with Stacks!\n");
    printf("The first number is: %d\n", current);

    while (trials < MAX_TRIALS) {
  
    printf("Will the next number be higher (H) or lower (L)? Enter Q to quit: ");
    scanf(" %c", &guess);
    
    if (guess == 'Q' || guess == 'q') {
        printf("Thanks for playing! Your final score is: %d\n", score);
        break;
    }

    next = rand() % 100 + 1;
    printf("The next number is: %d\n", next);
    
    if ((guess == 'H' || guess == 'h') && next > current) {
        printf("You guessed right! It's higher.\n");
        score++;
    } else if ((guess == 'L' || guess == 'l') && next < current) {
        printf("You guessed right! It's lower.\n");
        score++;
    } else {
        printf("Oops! You guessed wrong.\n");
        printf("Your final score is: %d\n", score);
        break;
        }

        push(&numbers, next);
        current = next;  

        trials++;
    }

    if (trials == MAX_TRIALS) {
        printf("You reached the maximum number of trials. Your final score is: %d\n", score);
    }

    return 0;
}
