<p align="center">
  <img src="https://engeto.cz/wp-content/uploads/2019/01/engeto-square.png" width="200" height="200">
</p>

# Java - 4. lekce

## Co bychom měli mít hotové

 - Po třech hodinách už umíme slušně pracovat s vývojovými nástroji
 
 - Umíme pracovat s proměnnými, definovat vlastní třídami, vytvářet objekty

 - Měli bychom znát základní operátory a umět z nich sestavit výraz
 
 - Umíme program větvit a provádět operace v cyklech
 
## Co nás čeká

- [Vícerozměrné pole](#více-rozměrné-pole)
- [Klíčová slova break a continue](#klíčová-slova-break-a-continue)
- [Větvení pomocí switch](#větvení-pomocí-switch)
- [Switch pomocí výrazů (Switch Expression)](#switch-pomocí-výrazů-switch-expression)

- [Vysvětlení Big O notace]()

- Úvod do OOP (Objektově orientovaného programování)
-- Principy OOP
-- Abstraktní třída,
-- Interface



## Pokračování polí

V minulé lekci jsme si ukázali, jak funguje pole. Možná vás napadlo, jak programy pracují s vícerozměrným světem. Jedna z možností je použít vícerozměrná pole.

### Více rozměrné pole
Fungují stejně jako jednorozměrná. Při definici je potřeba určit počet dimenzí pole a při inicializaci je nutné specifikovat kolik prvků bude v každé dimenzi.

#### Syntaxe 
```
DataType[1st dimension][2nd dimension][]..[Nth dimension] arrayName = new DataType[size1][size2]….[sizeN];
```
#### Příklad 2D pole
```
Integer[][] pole = new Integer[10][5];

int c = 0;
for (int y = 0;y<pole.length;y++){
    for (int x = 0;x<pole[y].length;x++){
        c++;
        pole[y][x] = c;
    }
}

System.out.println(Arrays.deepToString(pole));

for (int y = 0;y<pole.length;y++){
    for (int x = 0;x<pole[y].length;x++){
        System.out.printf("%-4s",pole[y][x]);
    }
    System.out.println();
}


[[1, 2, 3, 4, 5], [6, 7, 8, 9, 10], [11, 12, 13, 14, 15], [16, 17, 18, 19, 20], [21, 22, 23, 24, 25], [26, 27, 28, 29, 30], [31, 32, 33, 34, 35], [36, 37, 38, 39, 40], [41, 42, 43, 44, 45], [46, 47, 48, 49, 50]]
1   2   3   4   5   
6   7   8   9   10  
11  12  13  14  15  
16  17  18  19  20  
21  22  23  24  25  
26  27  28  29  30  
31  32  33  34  35  
36  37  38  39  40  
41  42  43  44  45  
46  47  48  49  50
```

#### Úkol
Napište program, který naformátuje danou tabulku automaticky, tak aby se tam vešla všechna čísla, ale okolo nebylo zbytečné volné místo.


## Pokračování podmínky a cykly
V poslední lekci jsem si vysvětlovali podmínky a cykly. Na dnešní lekci nám k tomuto tématu zbývá několik věcí.

### Klíčová slova `break` a `continue`
První z nich je vysvětlení klíčovových slov `break` a `continue`. Občas nastane situace, kdy by se hodilo volání bloku v cyklu nějak ukončit. V úvahu přichází použití `return`, které ukončí danou metodu a volitelně pošle návratovou hodnotu. Co když ale necheme ukončit celou metodu, ale jenom ukončit aktualní cyklus, případně jenom blok volání v daném cyklu?

Na ukončení volání cyklu použijeme klíčové slovo `break`. Hodí se to zejména v situacích, kdy máme vnořené cykly a potřebujeme se vrátit o úroven zpět.


#### Ukázka vnořeného cyklu.
```
for (int y = 0; y<10;y++){
    for (int x = 0; x<10;x++){
        System.out.print("█");
    }
    System.out.println();
}

██████████
██████████
██████████
██████████
██████████
██████████
██████████
██████████
██████████
██████████
```

#### Ukázka vnořeného cyklu a jeho ukončení pomocí `break`
```
for (int y = 0; y<10;y++){
    for (int x = 0; x<10;x++){
        if (x > y){
            break;
        }
        System.out.print("█");
    }
    System.out.println();
}

█
██
███
████
█████
██████
███████
████████
█████████
██████████
```


Pokud potřebujeme ukončit jenom blok volání v daném cyklu, tak použijeme `continue`

#### Ukázka vnořeného cyklu a přeskočení zbytku bloku pomocí `continue`
```
for (int y = 0; y<10;y++){
    for (int x = 0; x<10;x++){
        if (x < y){
            continue;
        }
        System.out.print("█");
    }
    System.out.println();
}


██████████
█████████
████████
███████
██████
█████
████
███
██
█
```

#### Úkol:
Napište program, který vypíše čísla od 1 do X za použití cyklu a `break`.

### Větvení pomocí `switch`

V předchozí lekci jsme si ukázali chování `if/else` k větvení programu. Během domácích cvičení jste mohli narazit na situace, kde jste potřebovali program rozvětvit na několik možností a řada `if (...) {...} else if (...) {...} else if` byla velice dlouhá a nepřehledná. Navíc v některých případech se části bloků překrývali a měli jste dilemma jak to řesit.

Mezi verzemi Javy 12 a 15 došlo k podstatnému vylepšení chování výrazu switch. Tak pozor, na to kterou verzi Javy máte nainstalovanou.

V dnešní lekci si nejdříve ukážeme původní chování vyrazu  `switch` tak i nového vylepšeného chování za použití výrazů `switch expression`.


#### Ukázka if-else
```
Integer value = 3;

if (value == 0) { 
    // A
} else if (value == 1 || value == 2)  {
    // A
    // B
} else if (value == 3) {
    // A
    // C
} else if (value == 4) {
    // C
} else  {
    // C
    // D
}
```


#### Syntaxe 

Switch podporuje jako přoměnné jenom některé typy:
- enum
- String
- Character/char
- Byte/byte
- Short/short
- Integer/int
Pozor nikoliv Long/long nebo typy s desetinou čárkou.

```
switch (proměnná) {
    case hodnota: 
        výraz;
        další-výraz;
    case hodnota2:
    case hodnota3:
        jiný-výraz;
        break;
    default:
        výraz;
        break;
}
```

#### Switch přes enum
```
public enum Day { SUNDAY, MONDAY, TUESDAY,
    WEDNESDAY, THURSDAY, FRIDAY, SATURDAY; }
...

int numLetters = 0;
Day day = Day.WEDNESDAY;
switch (day) {
    case MONDAY:
    case FRIDAY:
    case SUNDAY:
        numLetters = 6;
        break;
    case TUESDAY:
        numLetters = 7;
        break;
    case THURSDAY:
    case SATURDAY:
        numLetters = 8;
        break;
    case WEDNESDAY:
        numLetters = 9;
        break;
    default:
        throw new IllegalStateException("Invalid day: " + day);
}
System.out.println(numLetters);
```

### Klíčové slovo `yield`
Další klíčové slovo, kterým můžeme upravovat běh programu je `yield`. Toto slovo použijeme v případě, že chceme z výrazu `switch` vrátit hodnotu a tu uložit do proměnné.

#### Switch návratová hodnota pomocí `yield`
```
Den den = Den.PATEK;
String zprava = switch (den){
    case PATEK:
        yield "Bude vikend";
    default:
        yield "Jiny den";
};

System.out.println(zprava);


===useYield===
Bude vikend
```

### Switch pomocí výrazů (Switch Expression)

Od verze Javy 12, přibyla nová možnost zapisovat `switch` pomocí jiné syntaxe. Tato syntaxe značně zpřehledňuje daný zápis. Už není potřeba psát `break`, a také není potřeba vypisovat `case` v případě, že se použije stejný blok kódu. A pokud potřebujeme jenom vrátit jednoduchou hodnotu, tak nemusíme psát slovo `yield`.

```
Day day = Day.WEDNESDAY;    
System.out.println(
    switch (day) {
        case MONDAY, FRIDAY, SUNDAY -> 6;
        case TUESDAY                -> 7;
        case THURSDAY, SATURDAY     -> 8;
        case WEDNESDAY              -> 9;
        default -> throw new IllegalStateException("Invalid day: " + day);
    }
);    
```

#### Úkol:
Napište program, který na základě ročního období vypíše jiný text a napište tři různé implementace pomocí (if-else, switch, switch expression)
```
enum RocniObdobi {JARO, LETO, PODZIM, ZIMA}
```

## Big O notace (Landauova notace)

Jedna z důležitých věcí k pochopení proč nekteré věci nefungují rychle nebo padají na `OutOfMemoryError` je pochopení komplexity algoritmů resp. jejich asymptotické chování.

### O(1) - konstantní čas
```
boolean IsFirstElementNull(List<string> elements)
{
    return elements[0] == null;
}
```

### O(logN) - lineární čas

Binary Search

### O(N) - lineární čas


```
boolean containsValue(List<string> elements, String value)
{
    foreach (String element : elements)
    {
        if (element == value) return true;
    }
    
    return false;
}
```

### O(N^2) - kvadratický čas
```
bool ContainsDuplicates(IList<string> elements)
{
    for (var outer = 0; outer < elements.Count; outer++)
    {
        for (var inner = 0; inner < elements.Count; inner++)
        {
            // Don't compare with self
            if (outer == inner) continue;

            if (elements[outer] == elements[inner]) return true;
        }
    }

    return false;
}
```
### O(2^N) - exponenciální čas

```
int Fibonacci(int number)
{
    if (number <= 1) return number;

    return Fibonacci(number - 2) + Fibonacci(number - 1);
}
```

#### Příklady bežných algoritmů (výpočetní náročnost):
- Constant O(1) - value lookup
-  Logarithmic algorithm – O(logn) – Binary Search
-  Linear algorithm – O(n) – Linear Search
- Superlinear algorithm – O(nlogn) – Heap Sort, Merge Sort
- Polynomial algorithm – O(n^c) – Strassen’s Matrix Multiplication, Bubble Sort, Selection Sort, Insertion Sort, Bucket Sort
- Exponential algorithm – O(c^n) – Tower of Hanoi
- Factorial algorithm – O(n!) – Determinant Expansion by Minors, Brute force Search algorithm for Traveling Salesman Problem.

#### Příklady bežných algoritmů (paměťová náročnost):
- Ideal algorithm - O(1) - Linear Search, Binary Search
    Bubble Sort, Selection Sort, Insertion Sort, Heap Sort, Shell Sort
- Logarithmic algorithm - O(log n) - Merge Sort
- Linear algorithm - O(n) - Quick Sort
- Sub-linear algorithm - O(n+k) - Radix Sort

### K prostudování k kolekcí (pokračování v dalších lekcích)
https://www.bigocheatsheet.com/
