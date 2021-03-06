## Verifica delle false occorrenze

Il metodo di Rabin-Karp può trovare dele false occorrenze, anche se la probabilità è molto bassa che queste compaiano.

L'algoritmo di Mathukrishnan serve per verificare se ci sono o meno delle false occorrenze in tempo *O(n)*.

L'algoritmo prende in input la lista delle posizioni in cui c'è un'occorrenza vera o meno. Per ogni posizione in input viene calcolata la distanza che ...

Tutte le posizioni della stessa corsa devono quindi essere alla stessa distanza *d*, altrimenti c'è una falsa correnza che viene scoperta perché non rispetta il periodo del pattern.

Una volta verificato ciò è necessario controllare che *T[pos_s + m, pos_t +m -1]* abbia effettivamente periodo *d* uguale alla distanza tra due occorrenze (*pos_s è la prima posizione della corsa, pos_t è l'ultima posizione, m è lunghezza della stringa che rimane "scoperta"*).

Da notare che si può partire già da *pos_s + m* perché i primi *m* caratteri vengono già confrontati direttamente dall'algoritmo.

```
TODO: algoritmo
```

### Complessità

Per ogni corsa si hanno al massimo *pos_t - pos_s - d*, se il risultato è negativo viene segnalata una falsa occorrenza e l'algorimto termina, altrimenti passa alla corsa successiva.

Durante la verfica di una corsa, ogni carattere del testo viene confrontato al massimo 2 volte con i caratteri del pattern più 1 volta con il carattere successivo (*a distanza d credo*) del testo.

Dal momento che le corse distinte non si sovrappongono, si ha che vengono fatti al massimo *O(3n)* confronti, che portano ad una complessità di *O(n)*.

# Alberi dei suffissi

L'albero dei suffissi permette di evidenziare maggiormente la struttura interna di una stringa, permetttendo così di risolvere in tempo lineare il pattern matching esatto, così come altri problemi di pattern matching più complesso.

Con il pattern matching esatto è possibile effettaure una pre-elaborazione del testo in *O(n)* dopo la quale è possibile verificare in tempo *O(m)* la presenza del pattern, rendendo questi algortimi adatti ai problemi che hanno un testo fisso che deve essere matchato con più pattern distinti.

L'**albero dei suffissi** per una stringa *S* di lunghezza *n* è costituito da:

- *n* foglie numerate da 1 ad *n*.
- Ogni nodo interno, eventualmente esclusa la radice, ha almeno due figli.
- Ogni arco è etichettato con una sottostringa di *S*.
- Due archi uscenti dallo stesso nodo non possono avere etichette che iniziano con lo stesso carattere.
- La concatenazione delle etichette lungo il cammino dalla radice alla foglia etichettata *i* è il suffisso *S[i,n]* di lunghezza *n-i+1*

![Albero dei suffissi della stringa S = dabdac](./immagini/l18-fig1.png)

Da notare che non sempre è possibile costruire l'albero dei suffisi, perché se un suffisso è anche prefisso, questo termina in un nodo interno dell'albero, violandone la definizione.
Per evitare questo problema è necessario aggiungere un carattere sentinella alla fine della stringa. Assumeremo che questa ci sia sempre.

Nell'esempio *S=dabdac* è *c* che fa da sentinella, se non ci fosse non sarebbe possibile costruire l'albero.

L'**etichetta di un cammino** è la concatenazione delle etichette degli archi del cammino, mentre l'etichetta di un nodo *u* è data dall'etichetta della cammino dalla radice al nodo.

```
La profondità di un nodo è la lunghezza della sua etichetta.Se l’etichetta di un arco (u, v) tra due nodi u e v ha lunghezza k maggiore di 1 l’arco (u,v) è suddiviso in k parti (una per ogni carattere dell’etichetta) mediante k 1 nodi impliciti le cui etichette sono la concatenazione dell’etichetta di u con i caratteri dell’etichetta dell’arco (u, v) che precedono il nodo implicito stesso.
```

## Matching esatto con l'albero dei suffissi

...

### Complessità del matching esatto

C'è una complessità *O(n)* per la costruzione dell'albero (che per il momento non è stata vista).

...

Quindi *O(m)* per la ricerca del pattern e *O(k)* per elencare la *k* occorrenze.

## L'algoritmo naive per la costruzione dell'albero

L'albero dei suffissi per la stringa *S[1,n]$* viene costruito a partire dal suffisso più lungo della stringa *S*, ovvero tutta la stringa, per poi aggiungere gli altri suffissi *S[i,n]$* con *i = 2, ..., n+1*. (Viene assunto che la stirnga termina con la sentinella)

Con *Ai* viene indicato l'albero intermedio che contiene tutti i siffussi che iniziano nelle posizioni da 1 a *i*.

L'albero *A1* contiene solamente un unico arco etichettato con *S[1,n]$* che congiunge la radice e il nodo *1*.

Ogni albero *Ai+1* viene costruito nel seguente modo:
...

### Complessità dell'algoritmo

Quando devo aggiungere un suffisso vengono passati tutti i carattere per aggiungere un arco e ci sono al massimo *n* suffissi, portando ad una complessità di *O(n^2)*

## Algoritmo di Ukkonen

Questo algoritmo costruisce l'albero dei suffissi un carattere alla volta.

Così facendo viene persa la condizione che un suffisso non possa essere un prefisso dell'albero, per questo si dice che l'algoritmo crea una successio di alberi dei suffissi impliciti.

...


// Fino ai 3 casi