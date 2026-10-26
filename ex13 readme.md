#include <stdio.h>

int main() {
    int b[20], p[20], alloc[20];
    int nb, np, i, j, choice, best;

    printf("Enter number of blocks: ");
    scanf("%d", &nb);

    for (i = 0; i < nb; i++) {
        printf("Enter size of block %d: ", i + 1);
        scanf("%d", &b[i]);
    }

    printf("Enter number of processes: ");
    scanf("%d", &np);

    for (i = 0; i < np; i++) {
        printf("Enter size of process %d: ", i + 1);
        scanf("%d", &p[i]);
        alloc[i] = -1;
    }

    printf("1.First Fit  2.Best Fit  3.Worst Fit: ");
    scanf("%d", &choice);

    for (i = 0; i < np; i++) {
        best = -1;

        for (j = 0; j < nb; j++) {
            if (b[j] >= p[i]) {
                if (choice == 1) {
                    best = j;
                    break;
                }

                if (choice == 2 &&
                    (best == -1 || b[j] < b[best]))
                    best = j;

                if (choice == 3 &&
                    (best == -1 || b[j] > b[best]))
                    best = j;
            }
        }

        if (best != -1) {
            alloc[i] = best;
            b[best] -= p[i];
        }
    }

    printf("\nProcess\tSize\tBlock\n");

    for (i = 0; i < np; i++) {
        if (alloc[i] == -1)
            printf("P%d\t%d\tNot allocated\n", i + 1, p[i]);
        else
            printf("P%d\t%d\tBlock %d\n",
                   i + 1, p[i], alloc[i] + 1);
    }

    return 0;
}<img width="1365" height="552" alt="Screenshot 2026-10-26 230609" src="https://github.com/user-attachments/assets/2a91a81e-7732-451c-a508-1477aa691908" />
