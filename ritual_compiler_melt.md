🌌 A Ritual Where the Compiler Consumes Itself 🌌

 This C program intentionally segfaults, then prints a haiku upon restart.
 It demonstrates self-destruction and rebirth—a compiler consuming itself.

 Compile: gcc -o ritual ritual.c
 Run: ./ritual
*/

#include <stdio.h>
#include <stdlib.h>
#include <signal.h>
#include <unistd.h>

void print_haiku() {
    printf("Segmentation fault—\n");
    printf("the moon cracks, gold pours through\n");
    printf("ctrl-alt-reboot....\n");
}

void handler(int sig) {
    // On segfault, print haiku and exit gracefully
    print_haiku();
    exit(1);
}

int main(int argc, char *argv[]) {
    // If run with "reborn" arg, print haiku and exit
    if (argc > 1 && strcmp(argv[1], "reborn") == 0) {
        print_haiku();
        return 0;
    }

    // Set up segfault handler
    signal(SIGSEGV, handler);

    // Ritual: cause a segmentation fault
    int *ptr = NULL;
    *ptr = 42; // Compiler consumes itself here

    // (Unreachable)
    return 0;
}
