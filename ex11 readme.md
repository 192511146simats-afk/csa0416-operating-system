#include <stdio.h>
#include <pthread.h>

void *display(void *arg) {
    printf("Thread is running\n");
    return NULL;
}

int main() {
    pthread_t t1, t2;

    pthread_create(&t1, NULL, display, NULL);
    pthread_create(&t2, NULL, display, NULL);

    pthread_join(t1, NULL);
    pthread_join(t2, NULL);

    printf("Both threads completed\n");

    return 0;
}<img width="1365" height="549" alt="Screenshot 2026-10-26 225352" src="https://github.com/user-attachments/assets/1fffa700-4fcd-403c-851c-14624783edd3" />
