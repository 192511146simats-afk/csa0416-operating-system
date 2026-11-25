#include <stdio.h>

int main()
{
    int block[20], process[20];
    int allocation[20];
    int m, n;
    int i, j;
    int worst;

    printf("Enter number of memory blocks: ");
    scanf("%d", &m);

    printf("Enter size of each memory block:\n");
    for (i = 0; i < m; i++)
    {
        printf("Block %d: ", i + 1);
        scanf("%d", &block[i]);
    }

    printf("\nEnter number of processes: ");
    scanf("%d", &n);

    printf("Enter size of each process:\n");
    for (i = 0; i < n; i++)
    {
        printf("Process %d: ", i + 1);
        scanf("%d", &process[i]);
        allocation[i] = -1;
    }

    /* Worst Fit Allocation */
    for (i = 0; i < n; i++)
    {
        worst = -1;

        for (j = 0; j < m; j++)
        {
            if (block[j] >= process[i])
            {
                if (worst == -1 || block[j] > block[worst])
                {
                    worst = j;
                }
            }
        }

        if (worst != -1)
        {
            allocation[i] = worst;
            block[worst] = block[worst] - process[i];
        }
    }

    printf("\n--- WORST FIT MEMORY ALLOCATION ---\n");
    printf("Process\tProcess Size\tBlock\n");

    for (i = 0; i < n; i++)
    {
        if (allocation[i] != -1)
        {
            printf("P%d\t%d\t\tB%d\n",
                   i + 1,
                   process[i],
                   allocation[i] + 1);
        }
        else
        {
            printf("P%d\t%d\t\tNot Allocated\n",
                   i + 1,
                   process[i]);
        }
    }

    return 0;
}
