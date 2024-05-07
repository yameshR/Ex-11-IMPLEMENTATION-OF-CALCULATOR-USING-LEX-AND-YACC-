# Ex-11-IMPLEMENTATION OF CALCULATOR USING LEX AND YACC
# NAME: Yamesh R
# REGISTER NUMBER:212222220059
# Aim :
To implement a calculator using LEX and YACC.
# ALGORITHM
1. Start the program.
2. Write a program in the vi editor and save it with .l extension.
3. In the lex program, write the translation rules for the various mathematical functions.
4. Write a program in the vi editor and save it with .y extension.
5. Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6. Compile the yacc program with yacc compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7. Compile these with the C compiler as gcc lex.yy.c y.tab.c
8. Enter an expression as input and it is evaluated and the answer is displayed as output.
# PROGRAM
```
#include <stdio.h>
#include <string.h>

struct op {
    char l;
    char r[20];
} op[10], pr[10];

int main() {
    int a, i, k, j, n, z = 0, m, q;
    char *p, *l;
    char temp, t;
    char *tem;

    printf("Enter the Number of Values: ");
    scanf("%d", &n);

    for (i = 0; i < n; i++) {
        printf("left: ");
        scanf(" %c", &op[i].l); // Notice the space before %c to consume the newline character
        printf("\tright: ");
        scanf("%s", op[i].r);
    }

    printf("Intermediate Code\n");
    for (i = 0; i < n; i++) {
        printf("%c=%s\n", op[i].l, op[i].r);
    }

    for (i = 0; i < n - 1; i++) {
        temp = op[i].l;
        for (j = 0; j < n; j++) {
            p = strchr(op[j].r, temp);
            if (p) {
                pr[z].l = op[i].l;
                strcpy(pr[z].r, op[i].r);
                z++;
            }
        }
    }

    pr[z].l = op[n - 1].l;
    strcpy(pr[z].r, op[n - 1].r);
    z++;

    printf("\nAfter Dead Code Elimination\n");
    for (k = 0; k < z; k++) {
        printf("%c\t=%s\n", pr[k].l, pr[k].r);
    }

    for (m = 0; m < z; m++) {
        tem = pr[m].r;
        for (j = m + 1; j < z; j++) {
            p = strstr(tem, pr[j].r);
            if (p) {
                t = pr[j].l;
                pr[j].l = pr[m].l;
                for (i = 0; i < z; i++) {
                    l = strchr(pr[i].r, t);
                    if (l) {
                        a = l - pr[i].r;
                        printf("pos: %d", a);
                        pr[i].r[a] = pr[m].l;
                    }
                }
            }
        }
    }

    printf("Eliminate Common Expression\n");
    for (i = 0; i < z; i++) {
        printf("%c=%s\n", pr[i].l, pr[i].r);
    }

    for (i = 0; i < z; i++) {
        for (j = i + 1; j < z; j++) {
            q = strcmp(pr[i].r, pr[j].r);
            if ((pr[i].l == pr[j].l) &&!q) {
                pr[i].l = '\0';
                strcpy(pr[i].r, "\0");
            }
        }
    }

    printf("Optimized Code\n");
    for (i = 0; i < z; i++) {
        if (pr[i].l!= '\0') {
            printf("%c=%s\n", pr[i].l, pr[i].r);
        }
    }

    return 0;
}
```
# OUTPUT
<img width="494" alt="image" src="https://github.com/manomadhivanan/Ex-11-IMPLEMENTATION-OF-CALCULATOR-USING-LEX-AND-YACC-/assets/115543366/4d7c6f3f-dd8f-45c7-88c3-40a73a345fee">

# RESULT
The calculator is implemented using LEX and YACC and the output is verified.
