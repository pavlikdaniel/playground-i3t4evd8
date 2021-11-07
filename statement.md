# Sziasztok!

Ez egy online C játszótér, ahol le tudjátok futtatni és szerkeszteni a megírt kódokat és ellenőrző kérdéseket is tudtok kitölteni,
így teljesen tökéletes tanuláshoz.
Az alábbiakban megtalálhatjátok a Szétválogatás, Kiválogatás, Metszet és Únió szekciókat, amikben részletesen leírom hogyan is kell őket megírni.

# Válogassunk szét pár dolgot!
A szétválogatás azt jelenti, hogy egy tömbből a T tulajdonságú elemeket elválasztjuk a nem T tulajdonságúaktól.
A mi esetünkiben 2 tömbös szétválogatással fogunk foglalkozni.
A T tulajdonság lehet bármi, pl.: páratlan; nagyobb, mint 4; Osztható 16-al; stb.
Az alábbi kód egy szétválogatást mutat be a tomb_a nevű egész számokat tartalmazó tömbünkön. A páros számokat a tomb_paros,
a páratlanokat pedig a tomb_paratlan nevű tömbbe fogjuk átmásolni.

```C runnable
#include <stdio.h>
#include <stdlib.h>

#define N 6

int main() {
    // A kezdeti tömbünk létrehozása
    int tomb_a[N] = {1,2,3,4,5,7};
    
    //Mivel tudjuk, hogy a szétválogatás után egyik tömbünk sem lehet az eredeti tömbnél hosszabb,
    //így ezt a hoszt állítjuk be a páros és páratlan elemeket tartalmazó tömbjeinknek.
    int tomb_paros[N];
    int tomb_paratlan[N];
    int paroshossz = 0;
    int paratlanhossz = 0;

    // Járjuk be a tömbünket! (Mivel tudjuk a tömb hosszát (N), ezért for ciklussal célszerű ezt megtenni)
    int i;
    for(i=0;i<N;i++){
        
        //A tömb i-dik eleméről döntsük el, hogy T tulajdonságú-e és ha igen, másoljuk az egyik tömbbe, ha nem, akkor pedig a másikba.
        //Ebben az esetben a T tulajdonság a párosságra vonatkozik.
        if(tomb_a[i]%2 == 0){

            //Ebben az esetben páros, tehát a páros tömbünkbe másoljuk, majd a tömbhossz változót 1-el növeljük,
            //hogy tudjuk ebben a tömbben mennyi elem van.
            tomb_paros[paroshossz] = tomb_a[i];
            paroshossz++;

        }else{

            //Ebben az esetben páratlan a tomb_a i-dik eleme, így ennek megfelelően cselekszünk. (További infóért: Lásd páros eset)
            tomb_paratlan[paratlanhossz] = tomb_a[i];
            paratlanhossz++;

        }

    }

    //Hogy meggyőzőjünk a sikeresenen létrehozott tömbjeinkről, irassuk ki az elemeiket.
    printf("Páros tömb elemei: ");
    for(i=0;i<paroshossz;i++){
        printf("%d,",tomb_paros[i]);
    }

    printf("\n\nPáratlan tömb elemei: ");
    for(i=0;i<paratlanhossz;i++){
        printf("%d,",tomb_paratlan[i]);
    }
}

```
?[Mi az a szétválogatás?]
-[ ] Egyszerű. Be kell járni mindkét tömböt, összehasonlítani az elemeiket és ha nincs egyező, azt egy külön tömbbe rakjuk.
-[x] Amikor a tömbünk T tulajdonságú és nem T tulajdonságú elemeit külön szedjük.
-[ ] Nem tudom!
-[ ] Bejárjuk az egyik tömböt és minden egyes eleménél eldöntjük, hogy a másik tömbben van-e olyan elem. Ha van, akkor egy külön tömbbe tesszük azt.


# Nézzük is a metszetet
Van kettő különböző hosszúságú tömbünk, amik egész számmal vannak feltöltve. Ez tomb_a és tomb_b.
Ezeknek szeretnénk megtudni a metszetét, azaz azt, hogy melyik számok azok, amelyek mindkét tömbben megtalálhatóak.

```C runnable
#include <stdio.h>
#include <stdlib.h>

#define N 6
#define M 4

int main() {
    // A tömbök létrehozása
    int tomb_a[N] = {1,2,3,4,5,7};
    int tomb_b[M] = {3,5,1,6};
    
    //Mivel tudjuk, hogy a két tömbnek metszete nem lehet nagyobb, mint a legkisebb tömb hossza,
    //ezért a kisebb tömb hosszát adjuk meg a metszetünket tartalmazó tömb hosszának.
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

        // Figyeljünk arra, hogy a while-ban a j<M jöjjön első feltételnek, ugyanis a feltételek balról jobbra lesznek kiértékelve,
        // azaz ha a "tomb_a[i] != tomb_b[j]" lenne az első, akkor a j túlfutása esetén egy memóriaszemetet hasonlítunk össze 
        // ugyanis a tomb_b-nek a j. eleme már "nem létezik", ha a j nagyobb, mint maga a tömb hossza.
        while(j<M && tomb_a[i]!=tomb_b[j]){
            j++;
        }
        
        if(j<M){

            //Ebben az esetben találtunk a tomb_b tömbben tomb_a[i]-vel megegyező elemet (tehát az adott szám megtalálható mindkét tömbben),
            // így azt elhelyezzük a metszet tömbünkben.
            tomb_metszet[metszethossz] = tomb_a[i];
            metszethossz++;

        }

    }

    //Hogy meggyőzőjünk a sikeresenen létrehozott metszet tömbünkről, egyszerűen irassuk ki az elemeit
    printf("A metszet tömbünk elemei: ");
    for(i=0;i<metszethossz;i++){
        printf("%d,",tomb_metszet[i]);
    }
}

```
?[Hogyan néznéd meg két tömb metszetét?]
-[ ] Nem tudom!
-[ ] Egyszerű. Be kell járni mindkét tömböt, összehasonlítani az elemeiket és ha nincs egyező, azt egy külön tömbbe rakjuk.
-[] Még egyszerűbb. Használjuk a beépített intersect() függvényt.
-[x] Bejárjuk az egyik tömböt és minden egyes eleménél eldöntjük, hogy a másik tömbben van-e olyan elem. Ha van, akkor egy külön tömbbe tesszük azt. 

# Advanced usage

If you want a more complex example (external libraries, viewers...), see the [official documentation](https://tech.io/playgrounds/408/tech-io-documentation).
