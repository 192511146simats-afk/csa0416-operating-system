#include <stdio.h>

int readCount = 0;
int mutex = 1;
int wrt = 1;
int sharedData = 0;

void wait(int *semaphore)
{
    while (*semaphore == 0)
    {
        /* Wait */
    }

    (*semaphore)--;
}

void signal(int *semaphore)
{
    (*semaphore)++;
}

void reader()
{
    wait(&mutex);

    readCount++;

    if (readCount == 1)
    {
        wait(&wrt);
    }

    signal(&mutex);

    printf("\nReader is reading the data.");
    printf("\nShared data = %d\n", sharedData);

    wait(&mutex);

    readCount--;

    if (readCount == 0)
    {
        signal(&wrt);
    }

    signal(&mutex);

    printf("Reader finished reading.\n");
}

void writer()
{
    wait(&wrt);

    printf("\nWriter is writing data.\n");

    printf("Enter new value: ");
    scanf("%d", &sharedData);

    printf("Writer updated shared data to: %d\n", sharedData);

    signal(&wrt);

    printf("Writer finished writing.\n");
}

int main()
{
    int choice;

    while (1)
    {
        printf("\n--- READER WRITER PROBLEM ---\n");
        printf("1. Reader\n");
        printf("2. Writer\n");
        printf("3. Display Data\n");
        printf("4. Exit\n");

        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice)
        {
            case 1:
                reader();
                break;

            case 2:
                writer();
                break;

            case 3:
                printf("\nShared data = %d\n", sharedData);
                break;

            case 4:
                printf("Exiting...\n");
                return 0;

            default:
                printf("Invalid choice!\n");
        }
    }

    return 0;
}
