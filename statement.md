# Sziasztok kedves Hallgatók!

Ez egy online C játszótér, ahol le tudjátok futtatni és szerkeszteni a megírt kódokat és ellenőrző kérdéseket is tudtok kitölteni,
így teljesen tökéletes tanuláshoz.
Az alábbiakban megtalálhatjátok a Szétválogatás, Kiválogatás, Metszet és Únió szekciókat, amikben részletesen leírom hogyan is kell őket megírni.
<br /><b>Készítette: <a href="#" target="_blank">Pavlik Dániel</a></b>

# 1. Válogassunk szét pár dolgot!
A <b>szétválogatás</b> azt jelenti, hogy egy tömbből <b>a T tulajdonságú elemeket elválasztjuk a nem T tulajdonságúaktól.</b>
A mi esetünkben 2 tömbös szétválogatással fogunk foglalkozni, azaz az egyik tömbbe a T tulajdonságúakat a másikba pedig a nem T tulajdonságú elemeket gyűjtük ki.
A <b>T tulajdonság</b> lehet bármi, <b>pl.: páratlan; nagyobb, mint 4; Osztható 16-al; stb.</b>
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
    //így ezt a hosszt állítjuk be a páros és páratlan elemeket tartalmazó tömbjeinknek.
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

    return 0;
}

```
?[Mi az a szétválogatás?]
-[ ] Egyszerű. Be kell járni mindkét tömböt, összehasonlítani az elemeiket és ha nincs egyező, azt egy külön tömbbe rakjuk.
-[x] Amikor a tömbünk T tulajdonságú és nem T tulajdonságú elemeit külön szedjük.
-[ ] Nem tudom!
-[ ] Bejárjuk az egyik tömböt és minden egyes eleménél eldöntjük, hogy a másik tömbben van-e olyan elem. Ha van, akkor egy külön tömbbe tesszük azt.

# 2. Válogassunk ki egy tömbből!
A kiválogatásnak rengeteg módszere van, mi a szétválogatáshoz hasonlót fogjuk megnézni, ugyanis így könnyebb lehet megérteni.
Lesz egy tömbünk, aminek kiválogatjuk a T tulajdonságú elemeit egy másik tömbbe, viszont itt nem érdekelnek minket a nem T tulajdonságúak.
Az alábbi példában a negatív előjellel rendelkező elemeket fogjuk kiválogatni.

```C runnable
#include <stdio.h>
#include <stdlib.h>

#define N 6

int main() {
    // A kezdeti tömbünk létrehozása
    int tomb_a[N] = {-1,2,3,-4,5,-7};
    
    //Mivel tudjuk, hogy a kiválogatás után a kiválogatott elemeket tartalmazó tömbünk nem lehet hosszabb az eredeti tömbünknél,
    //így ezt a hosszt állítjuk be a negatív elemeket tartalmaző tömbünknek.
    int tomb_negativ[N];
    int negativhossz = 0;

    // Járjuk be a tömbünket! (Mivel tudjuk a tömb hosszát (N), ezért for ciklussal célszerű ezt megtenni)
    int i;
    for(i=0;i<N;i++){
        
        //A tömb i-dik eleméről döntsük el, hogy T tulajdonságú-e és ha igen, másoljuk a negativ elemeket tartalmazú tömbbe.
        //Ebben az esetben a T tulajdonság a negatív előjelre vonatkozik.
        if(tomb_a[i] < 0){

            //Ebben az esetben teljesül a T tulajdonság, így átmásoljuk a tömbünk i-dik elemét és a negatív számokat tartalmaző tömbünk hosszát 1-el növeljük.
            tomb_negativ[negativhossz] = tomb_a[i];
            negativhossz++;

        }

    }

    //Hogy meggyőzőjünk a sikeresenen kiválogatott tömbünkről, irassuk ki az elemeit.
    printf("Negatív tömb elemei: ");
    for(i=0;i<negativhossz;i++){
        printf("%d,",tomb_negativ[i]);
    }

    return 0;
}

```
?[Mi az a kiválogatás?]
-[ ] Egyszerű. Be kell járni mindkét tömböt, összehasonlítani az elemeiket és ha nincs egyező, azt egy külön tömbbe rakjuk.
-[x] Amikor a tömbünk T tulajdonságú elemeit külön szedjük, de a nem T tulajdonságúak nem érdekelnek minket.
-[ ] Nem tudom!
-[ ] Amikor a tömbünk T tulajdonságú és nem T tulajdonságú elemeit külön szedjük.

# 3. Nézzük is a metszetet
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

    return 0;
}

```
?[Hogyan néznéd meg két tömb metszetét?]
-[ ] Nem tudom!
-[ ] Egyszerű. Be kell járni mindkét tömböt, összehasonlítani az elemeiket és ha nincs egyező, azt egy külön tömbbe rakjuk.
-[] Még egyszerűbb. Használjuk a beépített intersect() függvényt.
-[x] Bejárjuk az egyik tömböt és minden egyes eleménél eldöntjük, hogy a másik tömbben van-e olyan elem. Ha van, akkor egy külön tömbbe tesszük azt. 

# 4. Nézzük két tömb únióját
Van kettő különböző hosszúságú tömbünk, amik egész számmal vannak feltöltve. Ez tomb_a és tomb_b.
Ezeknek szeretnénk megtudni az únióját, azaz azt, hogy melyik számok azok, amelyek legalább az egyik tömbben előfordulnak.

```C runnable
#include <stdio.h>
#include <stdlib.h>

#define N 6
#define M 4

int main() {
    // A tömbök létrehozása
    int tomb_a[N] = {1,2,3,4,5,7};
    int tomb_b[M] = {3,5,1,6};
    
    //Mivel tudjuk, hogy a két tömbnek únója nem lehet nagyobb, mint a két tömb hosszának összege,
    //ezért ezt adjuk meg az úniónkat tartalmazó tömb hosszának.
    int O = N+M;

    int tomb_unio[O];
    int uniohossz = 0;

    // Elsőnek másoljuk be tomb_b elemeit a tomb_unioba
    // Figyelem! ha a tömbünk ismétlődő elemeket tartalmaz, akkor ezt máshogy kell elvégezni!
    int i;
    for(i=0;i<M;i++){
        tomb_unio[uniohossz] = tomb_b[i];
        uniohossz++;
    }

    // Járjuk be a tomb_a-t (Mivel tudjuk a tömb hosszát (N), ezért for ciklussal célszerű ezt megtenni)
    for(i=0;i<N;i++){
        
        // Ide lényegében egy "eldöntés tétele" jön, azaz, hogy van-e T tulajdonságú elem a tomb_unio tömbünkben.
        //(A T tulajdonság jelenleg az, hogy egyezik-e a tomb_a i-dik eleme a tomb_unio j-dik elemével)
        int j=0;

        // Figyeljünk arra, hogy a while-ban a j<M jöjjön első feltételnek, ugyanis a feltételek balról jobbra lesznek kiértékelve,
        // azaz ha a "tomb_a[i] != tomb_unio[j]" lenne az első, akkor a j túlfutása esetén egy memóriaszemetet hasonlítunk össze 
        // ugyanis a tomb_unio-nek a j. eleme már "nem létezik", ha a j nagyobb, mint maga a tömb hossza.
        while(j<M && tomb_a[i]!=tomb_unio[j]){
            j++;
        }

        //Lényegében ebben különbözik az únió a metszettől. Tehát az eldöntésünk nem arra irányul, hogy találtunk-e egyező elemet,
        //hanem arra, hogy nem találunk az únió tömbben, ezért belerakjuk.
        if(j>=M){

            //Ebben az esetben találtunk a tomb_b tömbben tomb_a[i]-vel megegyező elemet (tehát az adott szám megtalálható mindkét tömbben),
            // így azt elhelyezzük az únió tömbünkben.
            tomb_unio[uniohossz] = tomb_a[i];
            uniohossz++;

        }

    }

    //Hogy meggyőzőjünk a sikeresenen létrehozott metszet tömbünkről, egyszerűen irassuk ki az elemeit
    printf("Az Únió tömbünk elemei: ");
    for(i=0;i<uniohossz;i++){
        printf("%d,",tomb_unio[i]);
    }

    return 0;
}

```
?[Hogyan néznéd meg két tömb únióját?]
-[ ] Nem tudom!
-[X] Egyszerű. Az egyik tömböt berakjuk az únió tömbünkbe, majd a másik tömbön végigmegyünk és ami nincs benne az únióban, azt belerakjuk.
-[ ] Még egyszerűbb. Használjuk a beépített intersect() függvényt.
-[ ] Bejárjuk az egyik tömböt és minden egyes eleménél eldöntjük, hogy a másik tömbben van-e olyan elem. Ha van, akkor egy külön tömbbe tesszük azt.

# Köszönöm, hogy végigolvastad!

Amennyiben elnyerte a tetszésedet ez a kis tanulós doksi, írj egy üzenetet, hogy szeretnél-e még ilyet a későbbiekben, illetve, hogy segített-e a tanulásban.
<br /><b>Készítette: <a href="#" target="_blank">Pavlik Dániel</a></b>