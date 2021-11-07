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
    
    //Mivel tudjuk, hogy a két tömbnek metszete nem lehet nagyobb, mint a legkisebb tömbb hossza, ezért a kisebb tömbb hosszát adjuk meg a metszetünket tartalmazó tömbb hosszának.
    int O = N;
    if(M<N){
        O = M;
    }
    int tomb_metszet[O];
    int metszethossz = 0;

    // Járjuk be elsőnek az egyik tömböt (Mivel tudjuk a tömb hosszát (N), ezért for ciklussal célszerű ezt megtenni)
    int i;
    for(i=0;i<N;i++){
        
        // Ide lényegében egy "eldöntés tétele" jön, azaz, hogy van-e T tulajdonságú elem a tomb_b tömbünkben. (A T tulajdonság jelenleg az, hogy egyezik-e a tomb_a i-dik eleme a tomb_b j-dik elemével)
        int j=0;
        // Figyeljünk arra, hogy a while-ban a j<M jöjjön első feltételnek
        while(j<M && tomb_a[i]!=tomb_b[j]){
            j++;
        }
        if(j<M){
            //Ebben az esetben találtunk a tomb_b tömbben tomb_a[i]-vel megegyező elemet (tehát az adott szám megtalálható mindkét tömbben), így azt elhelyezzük a metszet tömbünkben.
            tomb_metszet[metszethossz] = tomb_a[i];
            metszethossz++;
        }

    }

    //Hogy meggyőzőjünk a sikeresenen létrehozott metszet tömbünkről, egyszerűen irassuk ki az elemeit
    for(i=0;i<metszethossz;i++){
        printf("A metszet tömbünk elemei: ");
        printf("%d,",tomb_metszet[i]);
    }
}

```

# Advanced usage

If you want a more complex example (external libraries, viewers...), see the [official documentation](https://tech.io/playgrounds/408/tech-io-documentation).
