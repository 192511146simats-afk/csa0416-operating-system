#include <stdio.h>
#include <string.h>
#include <unistd.h>
#include <sys/mman.h>
#include <sys/wait.h>

int main() {
    char *shared = mmap(NULL, 4096,
        PROT_READ | PROT_WRITE,
        MAP_SHARED | MAP_ANONYMOUS, -1, 0);

    if (shared == MAP_FAILED) {
        perror("mmap");
        return 1;
    }

    int pid = fork();

    if (pid == 0) {
        strcpy(shared, "Hello from child process");
    } else if (pid > 0) {
        wait(NULL);
        printf("Message: %s\n", shared);
    } else {
        perror("fork");
    }

    munmap(shared, 4096);
    return 0;
}<img width="1365" height="547" alt="Screenshot 2026-10-26 221636" src="https://github.com/user-attachments/assets/e69f2bdf-b616-4f39-99de-7e29af5ee3e1" />
