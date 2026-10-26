#include <stdio.h>
#include <unistd.h>
#include <sys/wait.h>

int main() {
    int pid = fork();

    if (pid == 0) {
        printf("Child Process ID: %d\n", getpid());
        printf("Parent Process ID: %d\n", getppid());
    } else if (pid > 0) {
        printf("Parent Process ID: %d\n", getpid());
        printf("Child Process ID: %d\n", pid);
        wait(NULL);
    } else {
        printf("Process creation failed\n");
    }

    return 0;
}<img width="1366" height="768" alt="Screenshot 2026-10-26 214558" src="https://github.com/user-attachments/assets/baa6e081-ce0b-4a96-88f6-49cc3bebc1df" />
