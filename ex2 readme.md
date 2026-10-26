#include <stdio.h>
#include <fcntl.h>
#include <unistd.h>

int main() {
    int source, destination, n;
    char buffer[100];

    source = open("input.txt", O_RDONLY);

    if (source < 0) {
        printf("Cannot open input file\n");
        return 1;
    }

    destination = open("output.txt",
                       O_WRONLY | O_CREAT | O_TRUNC, 0644);

    if (destination < 0) {
        printf("Cannot create output file\n");
        close(source);
        return 1;
    }

    while ((n = read(source, buffer, sizeof(buffer))) > 0) {
        if (write(destination, buffer, n) != n) {<img width="1363" height="552" alt="Screenshot 2026-10-26 215137" src="https://github.com/user-attachments/assets/c6199575-de9e-4950-9127-b6f041799036" />

            printf("File write failed\n");
            close(source);
            close(destination);
            return 1;
        }
    }

    printf("File copied successfully\n");

    close(source);
    close(destination);

    return 0;
}
