#include <stdio.h>

int main() {
    int n, i, j, bt[20], pr[20], p[20];
    int wt[20], tat[20], temp;
    float avgwt = 0, avgtat = 0;

    printf("Enter number of processes: ");
    scanf("%d", &n);

    for (i = 0; i < n; i++) {
        p[i] = i + 1;
        printf("Enter burst time and priority of P%d: ", p[i]);
        scanf("%d%d", &bt[i], &pr[i]);
    }

    for (i = 0; i < n - 1; i++) {
        for (j = i + 1; j < n; j++) {
            if (pr[i] > pr[j]) {
                temp = pr[i]; pr[i] = pr[j]; pr[j] = temp;
                temp = bt[i]; bt[i] = bt[j]; bt[j] = temp;
                temp = p[i]; p[i] = p[j]; p[j] = temp;
            }
        }
    }

    wt[0] = 0;

    for (i = 1; i < n; i++)
        wt[i] = wt[i - 1] + bt[i - 1];

    for (i = 0; i < n; i++) {
        tat[i] = wt[i] + bt[i];
        avgwt += wt[i];
        avgtat += tat[i];
    }

    printf("\nProcess\tBT\tPriority\tWT\tTAT\n");

    for (i = 0; i < n; i++)
        printf("P%d\t%d\t%d\t\t%d\t%d\n",
               p[i], bt[i], pr[i], wt[i], tat[i]);

    printf("Average Waiting Time = %.2f\n", avgwt / n);
    printf("Average Turnaround Time = %.2f\n", avgtat / n);

    return 0;
}<img width="1365" height="545" alt="Screenshot 2026-10-26 220232" src="https://github.com/user-attachments/assets/d3ac0e26-653d-47b6-8f18-aa9e670ca86f" />
