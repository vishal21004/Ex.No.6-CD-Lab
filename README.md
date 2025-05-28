# Ex.No:6
# IMPLEMENTATION OF THE BACK END OF THE COMPILER 
## REGNO:212222230177
## NAME :Vishal M.A


## AIM:
To write a program to implement the back end of the compiler.


## ALGORITHM:
1. Start the program.
2. Get the three variables from statements and stored in the text file k.txt.
3. Compile the program and give the path of the source file.
4. Execute the program.
5. Target code for the given statement is produced.
6. Stop the program.

## PROGRAM:
```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>

void remove_spaces(char* str) {
    char* i = str;
    char* j = str;
    while (*j != 0) {
        if (!isspace(*j)) {
            *i = *j;
            i++;
        }
        j++;
    }
    *i = 0;
}

int main() {
    char line[100], var[10], op1[10], op2[10], res[10], op;
    char filename[50];
    FILE *fp;
    int reg = 0;

    printf("Enter the filename of the intermediate code: ");
    scanf("%s", filename);

    fp = fopen(filename, "r");
    if (fp == NULL) {
        printf("Error: Could not open file.\n");
        return 1;
    }

    printf("\nIntermediate Code:\n\n");

    while (fgets(line, sizeof(line), fp)) {
        printf("\t\t%s", line);
    }

    rewind(fp);

    printf("\n\n\tStatement\t\tTarget Code\n\n");

    while (fgets(line, sizeof(line), fp)) {
        // Remove newline
        line[strcspn(line, "\n")] = 0;

        // Remove all spaces
        remove_spaces(line);

        // Try parsing 3-address code
        if (sscanf(line, "%[^=]=%[^+*/-]%c%s", res, op1, &op, op2) == 4) {
            printf("%s\t\tMOV %s, R%d\n", line, op2, reg);
            printf("\t\t\t");

            switch (op) {
                case '+': printf("ADD "); break;
                case '-': printf("SUB "); break;
                case '*': printf("MUL "); break;
                case '/': printf("DIV "); break;
                default:  printf("UNKNOWN "); break;
            }

            printf("%s, R%d\n\n", op1, reg);
            reg++;
        } else if (sscanf(line, "%[^=]=%s", res, op1) == 2) {
            // Handle simple assignment like t1=a
            printf("%s\t\tMOV %s, R%d\n\n", line, op1, reg);
            reg++;
        }
    }

    fclose(fp);
    return 0;
}
```

## OUTPUT:
![EXP 6 OUT](https://github.com/user-attachments/assets/e7857c56-c3ff-42e6-8aac-6ab90506fb68)



## RESULT:
The back end of the compiler is implemented successfully, and the output is verified.
