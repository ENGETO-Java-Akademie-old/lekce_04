## Zapouzdření (*encapsulation*)

_Zapouzdření_  znamená, že:

-   s hodnotami atributů objektu  `A`  může manipulovat vždy pouze tentýž objekt  `A`.
-   Žádný jiný objekt (ani objekt téže třídy) by neměl mít možnost manipulovat s hodnotami atributů našeho objektu.
-   Pokud chceme, aby objekt, že změnil hodnotu svých atributů (t.j. přešel do jiného  _stavu_), pošleme mu zprávu (zavoláme některou z metod tohoto objektu).


## Abstrakce (*abstraction*)

Abstrakce znamená, že každý objekt musí pohlížet na ostatní objekty jako na „černé skříňky“, které mají jasně dané ovládací prvky (_rozhraní_), ale nesmí spoléhat na to, jak fungují uvnitř.

## Dědičnost (*inheritance*)

Dědičnost řeší situaci, kdy máme dvě velmi podobné třídy, přičemž jedna z nich je „rozšířením“ té druhé.

Pojmy:

-   Původní třídu budeme označovat jako  **předka**  (_predecestor_) nebo také  **rodičovskou třídu**,
-   Odvozenou třídu budeme označovat jako  **potomka**  (_ancestor_).


## Polymorfismus (*polymorphism*)

Polymorfismus znamená, že **různé objekty mohou na stejnou zprávu reagovat různě.**


## Skládání (*composition*) 
**Skládání** (_composition_) znamená, že jeden objekt může být atributem jiného.


## Delegování (*delegation*)

označuje situaci, kdy objekt na volání metody reaguje tím, že zavolá metodu vnořeného objektu.
