#include <stdio.h>

int main() {
    int n, i, q, time = 0, done;
    int bt[20], rem[20], wt[20] = {0}, tat[20];

    printf("Enter number of processes: ");
    scanf("%d", &n);

    for (i = 0; i < n; i++) {
        printf("Enter burst time of P%d: ", i + 1);
        scanf("%d", &bt[i]);
        rem[i] = bt[i];
    }

    printf("Enter time quantum: ");
    scanf("%d", &q);

    if (q <= 0)
        return 1;

    do {
        done = 1;

        for (i = 0; i < n; i++) {
            if (rem[i] > 0) {
                done = 0;

                if (rem[i] > q) {
                    time += q;
                    rem[i] -= q;
                } else {
                    time += rem[i];
                    wt[i] = time - bt[i];
                    rem[i] = 0;
                }
            }
        }
    } while (!done);

    printf("\nProcess\tBT\tWT\tTAT\n");

    for (i = 0; i < n; i++) {
        tat[i] = bt[i] + wt[i];

        printf("P%d\t%d\t%d\t%d\n",
               i + 1, bt[i], wt[i], tat[i]);
    }

    return 0;
}<img width="1365" height="545" alt="Screenshot 2026-10-26 221216" src="https://github.com/user-attachments/assets/55d49dee-d303-40bd-9845-cf29967e00b3" />
