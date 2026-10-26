#include <stdio.h>

int main() {
    int n, i, time = 0, completed = 0, best;
    int at[20], bt[20], rem[20], pr[20];
    int ct[20], wt[20], tat[20];

    printf("Enter number of processes: ");
    scanf("%d", &n);

    for (i = 0; i < n; i++) {
        printf("Enter arrival time, burst time and priority of P%d: ", i + 1);
        scanf("%d%d%d", &at[i], &bt[i], &pr[i]);
        rem[i] = bt[i];
    }

    while (completed < n) {
        best = -1;

        for (i = 0; i < n; i++) {
            if (at[i] <= time && rem[i] > 0) {
                if (best == -1 || pr[i] < pr[best])
                    best = i;
            }
        }

        if (best == -1) {
            time++;
            continue;
        }

        rem[best]--;
        time++;

        if (rem[best] == 0) {
            ct[best] = time;
            completed++;
        }
    }

    printf("\nProcess\tAT\tBT\tPriority\tWT\tTAT\n");

    for (i = 0; i < n; i++) {
        tat[i] = ct[i] - at[i];
        wt[i] = tat[i] - bt[i];

        printf("P%d\t%d\t%d\t%d\t\t%d\t%d\n",
               i + 1, at[i], bt[i], pr[i], wt[i], tat[i]);
    }

    return 0;
}<img width="1365" height="549" alt="Screenshot 2026-10-26 220600" src="https://github.com/user-attachments/assets/798c4968-edad-4c07-9bdb-b13d2a053e43" />
