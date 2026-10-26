
#include <stdio.h>
#include <pthread.h>
#include <semaphore.h>
#include <unistd.h>

#define N 5

sem_t forks[N];

void *philosopher(void *arg)
{
    int id = *(int *)arg;
    int left = id;
    int right = (id + 1) % N;
    int i;

    for (i = 0; i < 2; i++)
    {
        printf("Philosopher %d is thinking\n", id + 1);

        if (id == N - 1)
        {
            sem_wait(&forks[right]);
            sem_wait(&forks[left]);
        }
        else
        {
            sem_wait(&forks[left]);
            sem_wait(&forks[right]);
        }

        printf("Philosopher %d is eating\n", id + 1);
        sleep(1);

        sem_post(&forks[left]);
        sem_post(&forks[right]);
    }

    return NULL;
}

int main()
{
    pthread_t t[N];
    int id[N], i;

    for (i = 0; i < N; i++)
        sem_init(&forks[i], 0, 1);

    for (i = 0; i < N; i++)
    {
        id[i] = i;
        pthread_create(&t[i], NULL, philosopher, &id[i]);
    }

    for (i = 0; i < N; i++)
        pthread_join(t[i], NULL);

    for (i = 0; i < N; i++)
        sem_destroy(&forks[i]);

    return 0;
}
<img width="1365" height="552" alt="Screenshot 2026-10-26 230034" src="https://github.com/user-attachments/assets/09862e0f-3edb-4bf0-9a5b-c73c12ab90c4" />
