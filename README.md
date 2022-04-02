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
