#include <stdio.h>
#include <string.h>
#include <unistd.h>
#include <sys/ipc.h>
#include <sys/msg.h>
#include <sys/wait.h>

struct message {
    long type;
    char text[100];
};

int main() {
    int qid = msgget(IPC_PRIVATE, IPC_CREAT | 0600);

    if (qid == -1) {
        perror("msgget");
        return 1;
    }

    int pid = fork();

    if (pid == 0) {
        struct message msg;

        msgrcv(qid, &msg, sizeof(msg.text), 1, 0);
        printf("Received message: %s\n", msg.text);
    } else if (pid > 0) {
        struct message msg;

        msg.type = 1;
        strcpy(msg.text, "Hello through message queue");

        msgsnd(qid, &msg, strlen(msg.text) + 1, 0);
        wait(NULL);
    }

    msgctl(qid, IPC_RMID, NULL);
    return 0;
}<img width="1365" height="544" alt="Screenshot 2026-10-26 221857" src="https://github.com/user-attachments/assets/ed090c3a-6844-4aa0-8e8a-506002da1926" />
