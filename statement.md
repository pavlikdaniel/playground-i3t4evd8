# Sziasztok!

Ez egy online C játszótér, ahol le tudjátok futtatni és szerkeszteni a megírt kódokat és még szöveget is tudok mellé írni, így teljesen tökéletes tanuláshoz.

# Nézzük is a metszetet
Van kettő különböző hosszúságú tömbünk, amik egész számmal vannak feltöltve. Ez tomb_a és tomb_b.
Ezeknek szeretnénk megtudni a metszetét, azaz azt, hogy melyik számok azok, amelyek mindkét tömbben megtalálhatóak.

```C runnable
#include <stdio.h>
#include <stdlib.h>

#define N 5
#define M 3

int main() {
    // A tömbök létrehozása
    int tomb_a[N] = {1,2,3,4,5};
    int tomb_b[M] = {3,5,1};

    // Járjuk be elsőnek az egyik tömböt (Mivel tudjuk a tömb hosszát(5), ezért for ciklussal célszerű ezt megtenni)
    int i;
    for(i=0;i<N;i++){
        printf("%d\n",tomb_a[i]);
    }
}

```

# Advanced usage

If you want a more complex example (external libraries, viewers...), see the [official documentation](https://tech.io/playgrounds/408/tech-io-documentation).
