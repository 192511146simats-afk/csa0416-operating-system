#include <stdio.h>

int main() {
    int n, i, time = 0, done = 0, best;
    int at[20], bt[20], finish[20] = {0};
    int ct[20], wt[20], tat[20];

    printf("Enter number of processes: ");
    scanf("%d", &n);

    for (i = 0; i < n; i++) {
        printf("Enter arrival time and burst time of P%d: ", i + 1);
        scanf("%d%d", &at[i], &bt[i]);
    }

    while (done < n) {
        best = -1;

        for (i = 0; i < n; i++) {
            if (!finish[i] && at[i] <= time) {
                if (best == -1 || bt[i] < bt[best])
                    best = i;
            }
        }

        if (best == -1) {
            time++;
            continue;
        }

        time += bt[best];
        ct[best] = time;
        finish[best] = 1;
        done++;
    }

    printf("\nProcess\tAT\tBT\tWT\tTAT\n");

    for (i = 0; i < n; i++) {
        tat[i] = ct[i] - at[i];
        wt[i] = tat[i] - bt[i];

        printf("P%d\t%d\t%d\t%d\t%d\n",
               i + 1, at[i], bt[i], wt[i], tat[i]);
    }

    return 0;
}<img width="1363" height="547" alt="Screenshot 2026-10-26 220859" src="https://github.com/user-attachments/assets/dd6ae332-4741-487b-bfa7-2e98a1cdc190" />
