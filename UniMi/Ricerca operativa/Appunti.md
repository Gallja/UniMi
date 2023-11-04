Programmazione lineare quando:
- le variabili hanno un dominio continuo
- i vincoli sono equazioni e disequazioni lineari (<=, >=, =)
- la funzione obiettivo è una funzione lineare delle variabili

Forma generale problema PL
1. maximize/minimize $z = cx$ funzione $z$ data dalla combinazione lineare di variabili x
2. subject to (introduzione del sistema di vincoli)
	- A1x >= b1 con A1 la matrice dei coefficienti e b1 i termini noti
	- A2x <= b2
	- A3x = b3
	- x' >=0 variabile soggetta a condizione di non negatività
	- x'' variabili libere / non ristrette

I problemi di PL sono riformulati nella formula alle disuguaglianze, per avere un utile interpretazione geometrica
Per passare dalla forma generale alla forma alle disuguaglianze occorre eliminare i vincoli di uguaglianza e le variabili libere.

Si puo sempre passare da un problema in forma generale a forma alle disuguaglianze

es
...

E' semplice identificare i vincoli ridondanti 
Per eliminare le variabili libere, sostituisco ogni variabile libera con la differenza tra due variabili non libere che introduco
Possiamo poi togliere i termini noti o costanti nella funzione obiettivo perche non cambia il ranking delle soluzioni (poi correggerremo il valore ottimo)
Rendiamo poi coerenti tutte le disequazioni: (tranne quello di condizione di non negativita)
- <= SE obiettivo di massimizzazione
- >= SE obiettivo di minimizzazione

Possiamo rappresentare lo stesso modello in maniera piu compatta come
w = c^T x
Ax <= b
x >= 0

...

Interpretazione geometrica della PL
Ogni soluzione x è un assegnamento di valore alle variabili, quindi un punto in uno spazio continuo ad n dimensioni, con n il numero di variabili.

Ogni vincolo di uguaglianza ax=b corrisponde ad un iperpiano
Ogni vincolo di disuguaglianza ax <= b corrisponde ad un semispazio

Il sistema dei vincoli nel modello alle disuguaglianze corrisponde all'intersezione dei corrispondenti semispazi, un poliedro

I semispazi sono convessi quindi l'intersezione di insiemi convessi è un insieme convesso QUINDI i poliedri sono convessi
Un insieme è convesso quando presi due qualunque punti nell insieme, tutti i punti dei segmenti fanno parte dell insieme convesso

Regione ammissibile
I "baffetti" dicono da quale parte il vincolo è violato

Poliedri ottenibili
- Poliedro limitato / politopo
- Poliedro illimitato: esiste una direzione per cui se parto da un punto e continuo per quella direzione, non incontro mai una frontiera 
- Poliedro vuoto: i vincoli sono combinati tali da non avere una soluzione ammissibile (e quindi una regione)

Tutte le soluzioni equivalenti giacciono su uno stesso iperpiano
La funzione obiettivo corrisponde ad un fascio di iperpiani paralleli ordinati come i corrispondenti valori dell'obiettivo
La direzione di ottimizzazione definisce l'ordinamento degli iperpiano del fascio

es
minimize z = 2x1 - 3x2
essendo x2 l'asse dell y e considerando che ha segnmo negativo, la direzione di ottimizzazione e verso l alto in quanto cosi x1 diminuisce e x2, aumentando, fa diminuire z

Considerando
- Convessita del poliedro = regione ammissibile
- Linearita delle curve di livello della funzione obiettivo
ne derivano 3 casi
- SE poliedro vuoto, non ci sono soluzioni ammissibili
- SE poliedro è illimitato nella direzione di ottimizzazione, allora non esiste un valore ottimo finito
- ALTRIMENTI esiste almeno un vertice del poliedro che corrisponde al valore ottimo, proprietà fondamentale della PL


Forma standard
Poniamo tutti i vincoli in forma di uguaglianza introducendo opportune variabili non negativo di scarto (slack) o di surplus

Mettendo in forma standard un problema alle disuguaglianze con m vincoli e n variabili, si ottiene un modell ocon m vincoli e n+m variabili tutte non negative

Il sistema dei vincoli è un sistema di m equazioni lineari in n+m variabili
SE non ci sono vincoli ridondanti, la matrice dei coefficienti ha rango m
Il sistema quindi ha una soluzione univocamente determinabile SE eliminiamo gli n gradi di liberata fissando n variabili

Ad ogni variabile nulla nella forma standard corrisponde un vincolo attivo nella forma alle disuguaglianze
Fissare n variabili a 0 nella forma standard, corrisponde a scegliere un punto in cui n vincoli sono attivi nella forma alle disuguaglianze

Soluzione di base
Una base è un sottoinsieme di m vairabili scelte tra le n+m della forma standard 
\[B|N]
Il numero di basi è combinatorio, crescendo esponenzialmente con m e n
Una volta scelta la base, il sistema si puo riscrivere come 
B\*xB + N\*xN = b

La soluzione del sistema m x m che si ottiene dopo aver fissato a 0 le n variabili fuori base è una soluzione di base
Per ottenerla biosgna invertire la matrice B formata dalla base

xB = B^(-1) b - B^(-1)NxN
da cui 
xN = 0 e xB = B^(-1)\*b

esistono soluzioni di base non ammissibili quando xB !>= 0
Per verificare cio basta controllare che le variabili di base siano ancora >=0


Degenerazione
Quando una variabile in base risulta avere valore nullo, si ha degenerazione in quanto piu soluzioni di base coincidono
Piu di n vincoli sono attivi nello stesso punto in uno spazio ad n dimensioni

Teorema fondamentale della PL
Dato un problema lineare in forma standard
z = min{c^T x : Ax = b, x>=0} 
con A di rango m
SE esiste una soluzione ammissibile, esiste anche una soluzione ammissibile di base 
(SE un poliedro non è vuoto, deve avere almeno un vertice)
SE esiste una soluzione ottima, esiste anche una soluzione ottima di base 
(SE il poliedro non è illimitato verso la direzione di ottimizzazione, ci deve essere un vertice del poliedro che ha il valore ottimo)

Perciò un problema lineare nel continuo può essere risolto come problema combinatorio discreto, limitandosi a considerare solo le soluzioni di base.


La complessita della programmazione lineare è polinomiale (all'aumentare di n e m) tramite l algoritmo dell'ellissoide (Khachiyan 1979)
Il metodo piu utilizzato per risolvere i problemi di PL è l'algoritmo del simplesso (Dantzig 1947)

L'algoritmo del simplesso non da garanzia di terminare in un numero di iterazioni limitato da un polinomio MA è molto veloce 

L'algoritmo garantisce di terminare in un numero finito di passi, garantendo una di queste tre situazioni
- la soluzione corrente è ottima
- NON esiste una soluzione ammissibile
- NON esiste soluzione ottima finita

L'algoritmo del simplesso procede iterativamente da una soluzione di base ad una adiacente


L'algoritmo del simplesso
Forma canonica
- Dalla forma standard del problema di PL
minimize z = c^T x
subject to Ax = b
x>=0

- Scegliendo una base e permutando le colonne di conseguenza si ha
minimize z = c^TB xB + c^TN xN
subject to BxB + NxN = b
xB, xN >= 0

- Moltiplicando a sinistra per B^-1
minimize z = c^TB xB + c^TN xN
subject to IXB + (B^-1 N) xN = B^-1 b
xB, xN >=0
con I matrice di identità

la soluzione di base xB = B^-1 b - (B^-1 N) xN

- Sostituendo xB = B^-1 b - (B^-1 N) xN in z
minimize z = c^TB B^-1 b + (c^TN - B^-1 N) xN
subject to IXB + (B^-1 N) xN = B^-1 b
xB, xN >=0

- Riscrivendo z
minimize z = zB + ...

con zB costante che dipende da B, come abbiamo scelta la base
con c segnato perche sono diversi dai c coefficienti iniziali

- Quando si pone xN = 0 si ha xB = B^-1 n = bsegnato
SE b segnato >= 0 ALLORA la soluzione di base è ammissibile 

Esistono quindi un numero combinatorio di forme canoniche, tante quante le possibili scelte della base
Un problema di PL è in forma canonica SE e SOLO SE
- i coefficienti delle variabili di base, xB, formano una matrice identità m x m
- le variabili di base xB NON compaiono nella funzione obiettivo

La forma canonica è forte SE e SOLO SE i termini noti dei vincoli sono non negativi, bsegnato >=0
Una forma canonica debole implica una soluzione di base non ammissibile 


Una volta posto in forma canonica un problema di PL si puo rappresentare in una matrice, tableau.
E' una struttura dati fondamentale sulla quale opera l'algoritmo del simplesso

es
...

```c
while (!Infeasible(b,c)) AND (!FeasibleBase(b)) do
	Pivot(A,b,c)
if Infeasible(b, c) then
	"Stop: problema inammissibile"
else 
	while (!Optimal(c)) AND (!Unbounded(A, c)) do
		Pivot(A, b, c)
	if Optimal(c) then 
		"Stop: soluzione ottima"
	else 
		"Stop: problema illimitato"
```

Nella prima parte si trova una soluzione di base ammissibile.
Wile finche la base non è Ammissibile e non abbiamo dimostrato che il problema è Infeasible
L'iterazione fondamentale del simplesso è il Pivot step

SE il problema è inammissibile, allora l algoritmo termina
Nella seconda parte si cerca una soluzione ottima
Ogni iterazione conserva l ammissibilita
O si trova la soluzione ottima o si scopre che il problema è illimitato

Infeasible = Ammissibile
Unbounded = Test che verifica che il problema sia illimitato

- Pivot(A, b, c)
Ogni iterazione consiste in un cambio di base
Una variabile in base esce dalla base e una variabile fuori base entra in base 
Geometricamente è come se ci muovessimo dal un vertice a un vertice adiacente

1. Si scegli un elemento pivot positivo posto su una colonna fuori base
2. Divido la riga del pivot per il pivot, in modo che il pivot diventi 1
3. Sottraggo ad ogni riga diversa da quella del pivot, la riga del pivot moltiplicata per aic cioè il coefficiente sulla riga i-esimo e sulla colonna del pivot. Nella colonna del pivot compariranno tutti 0 tranne il pivot. entra quindi in base la conolla del pivot ed esce di base la colonna corrispondente alal riga del pivot

Interpretazione
- Algebrica
Il tableau è un sistema di equazioni
L'iterazione corrisponde a riformare in modo equivalente il sistema di m equazioni e n variabili
Si prende la riga del pivot riscrivendo l equazione nuova incognita =... e poi per sostituzione ottieniamo un nuovo sistema

- Geometrica
Associato ad ogni vincolo un indice, la corrispondente variabile che quando è a 0, il vincolo è attivo
indice 1 è associato a x2 e 2 a x1 perche quando x1=0, allora è attivo x2

es
...

Facendo un Pivot, ottengo il punto B


Test di ottimalità: Optimal(c)
-20m