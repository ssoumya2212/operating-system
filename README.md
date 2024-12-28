#include <fcntl.h>  // For open()
#include <unistd.h> // For read(), write(), close()
#include <stdio.h>  // For perror()

#define BUFFER_SIZE 1024

int main(int argc, char *argv[]) {
    if (argc != 3) { printf("Usage: %s <source> <destination>\n", argv[0]); return 1; }
    
    int src = open(argv[1], O_RDONLY);
    int dest = open(argv[2], O_WRONLY | O_CREAT | O_TRUNC, 0644);
    if (src < 0 || dest < 0) { perror("Error"); return 1; }

    char buf[BUFFER_SIZE];
    ssize_t n;
    while ((n = read(src, buf, BUFFER_SIZE)) > 0)
        write(dest, buf, n);

    close(src); close(dest);
    return 0;
}


op:output:
Child: PID=26850, Parent PID=26849
Parent: PID=26849, Child PID=26851
Parent: PID=26851, Child PID=0
