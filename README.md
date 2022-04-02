# treeCSPsolver
## class SegmentMatrix
### __init__(self, n)
Crea una matrice nxn di zeri con diagonale -1.
### insert_segment(self, p1_name, p2_name)
Inserisce dei segmenti nella matrice, infatti all'interno della matrice nella posizione [p1_name, p2_name] e [p2_name, p1_name] viene assegnato valore 1 per indicare che vi è un arco tra i due punti.
## class Map
### reset(self)
Resetta la mappa svuotando l'array contenente i punti e il dizionario contenente i parametri dei segmenti scelti durante la creazione della mappa.
### isThere_point(self, x, y)
Controlla se il punto con coordinate x e y è già presente tra i punti precedentemente generati e se lo è ritorna True, altrimenti False.
### generate_points(self, n)
Genera n punti con coordinate casuali e al suo interno chiama isThere_point(self, x, y), se quest'ultimo ritorna True richiama se stesso con n=1.
### is_intersected(self, p3, p4)
Controlla se il segmento che voglio inserire (p3, p4) ne interseca almeno uno tra quelli già selezionati e se ciò avviene ritorna True, altrimenti False. Per sapere se i segmenti si intersecano si prendono in considerazione le equazioni delle rette e si cerca l'eventuale punto di intersezione e in seguito a che coordinate avviene.
### find_connection(self, p, matrix)
Seleziona e ritorna il nome del punto tale che non esiste un arco che collega se stesso e il punto p all'interno della matrice di tipo SegmentMatrix e che tra tutti i punti diversi da p è quello a distanza minore che non inteseca i segmenti precedentementi selezionati per creare la mappa.
### are_connections_possible(self, matrix)
Controlla se potrebbero essere possibili altre connessioni tra i punti. Per farlo scorre tutta la matrice dei segmenti e se almeno in un punto (che poi in realtà sarebbe due dato che la matrice è simmetrica rispetto alla diagonale) il valore è 0 allora è possibile che si possa inserire un segmento aggiuntivo.
### generate_map(self, n)
Crea la mappa generando inzialmente n punti e in seguito seleziona un punto casuale tra quelli generati e cerca un segmento con find_connection(self, p, matrix) finchè ci sono possibili connessioni da aggiungere alla matrice dei segmenti.
## class Tree
### __init__(self, map)
Inizializza MST, un dizionario di liste inizialmente vuoto, che contiene gli archi selezionati durante la ricerca dell'albero di copertura a peso minimo e inoltre inizializzo una matrice simmetrica rispetto alla diagonale contenente dei pesi positivi generati casualmente quando nella matrice dei segmenti della classe Map l'arco ij ha valore 1, altrimenti il peso che gli viene assegnato è 0.
### primsAlgorithm(self, map)
Sceglie un nodo casuale e lo visita, in seguito visita il nodo 'j' tale che non é ancora stato visitato e che l'arco 'ij' ha il peso minore possibile con 'i' visitato. In seguito inserisce tale arco non orientato nel dizionario MST.
## class Variable 
### __init__(self, tree)
Inizializza un dizionario di liste che contiene i vicini di ogni nodo, un array vuoto dove inserire i genitori di ogni nodo e un dizionario di liste dove inserire i figli di ogni nodo. 
## class Constraint
### respected_constraint(self, di, dj)
Controlla se i valori dei domini di due diverse variabili sono diversi, se lo sono allora ritorna True, altrimenti False
## class CSP
### __init__(self, tree)
Genera X di tipo Variable, C di tipo Constraint e inoltre genera un dizionario di liste contenente il dominio dei colori di ogni variabile e crea un array che contiene l'assegnazione del colore delle variabili.
### topologicalSortUtil(self, v, visited, stack)
Visita il nodo v, scorre tutti i suoi vicini e controlla se sono già stati visitati, se non lo sono allora: segna che il genitore del nodo selezionato tra i vicini, i, è v e che il figlio di v è i e inoltre viene richiamato topologicalSortUtil(i,visited,stack). Se inece sono già stati visitati tutti i vicini del nodo v allora viene inserito in cima all'array stack il nodo v.
### topologicalSort(self, root)
Crea un array di zeri che indica se sono stati visitati o meno i vari nodi (1 se sono stati visitati), un array vuoto dove inserire poi l'ordine topologico dei nodi e infine chiamo topologicalSortUtil(root, visited, stack)
### check_domain(self, di, i, j)
Controlla se, assunto il valore di del dominio del nodo i, esiste almeno un valore del dominio del nodo j che rispetti il vincolo di soddisfacimento, e si salva nell'array remove_fromDomain quali valori del dominio di j non rispettano il vincolo.
### revise(self, i, j)
Controlla con check_domain(di, i, j) tutti i possibili valori del dominio del nodo i e se non esiste almeno un valore nel dominio di j che rispetta il vincolo di soddisfacimento allora l'arco ij non si può rendere consistente, altrimenti, se invece è consistente o lo si può rendere tale, si rimuovono dal dominio di j i valori che impedirebbero il soddisfacimento dei vincoli. Infine ritorna se ij è consistente e se sono stati tolti dei valori dal dominio di j.
### make_arc_consistent(self, parent, child)
Controlla se l'arco parent-child è consistente, se non lo è ritorna False, in seguito se sono state apportate modifiche al dominio child e se il nodo child ha dei figli allora viene chiamato make_arc_consistent anche su di essi.
### tree_CSP_solver(self)
Sceglie un nodo casuale come radice, fa l'ordine topologico dei nodi, controlla se gli tutti gli archi sono o possono essere resi consistenti, e a partire dalla radice fino alle foglie dell'albero assegna il primo valore consistente disponibile all'interno del dominio.
