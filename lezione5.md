# Lezione 5 (cicli for, while, do/while)
## 5.1) Introduzione
Un esempio degli utilizzi delle cose che impareremo a lezione è calcolare una media di n numeri.
Per ora possiamo fare un numero n di double per i numeri da calcolare, il che è molto lungo e "noioso". Tuttavia se il numero di elementi per cui calcolare la media è grandissimo è impossibile ovviamente. Per questo possono tornare utili i cicli scritti prima, automatizzano queste procedure.
## 5.2) Ciclo for
### Formula generale
```cc
for(condizione iniziale; condizione di loop; condizione di update) {
    statement
} //condizione di loop diciamo che ci fornisce un "limite" a questo ciclo
```
### Esempio 1 (semplice)
Vogliamo far stampare sullo schermo i numeri da 0 a 10 in modo automatico:
```cc
for(int i = 0; i <= 10; i++) { //ricordo: i++ è uguale a scrivere i = i + 1, stessa cosa con sottrazioni
    cout << i << endl;
} //importante: succede che la prima volta il codice guarda i, vede che è = 0 es esegue il comando, poi fa i + 1 (aggiorna la i) e così via
```
Una volta che ho dichiarato i quella ovviamente diventa una variabile LOCALE. (vedi Esempio 7 per approfondimento)
### Esempio 2
```cc
for(intj = 0; j < 11; j++) {
    statement
} //questo comando è identico a quello precedente, perchè ho messo strettamente minore, questo è importante
```
### Esempio 3
```cc
for (int k = 1; k > 16; k = k + 2) {
    statement
}
```
Obv possiamo fare anche così.
### Esempio 4
Questo ciclo for possiamo farlo partire anche da un valore alto per farlo arrivare a un valore basso:
```cc
for(int g = 10; g > 1; g--) {
    statement
}
```
### Esempio 5
```cc
for(int j = 2; j < 100; j = 2 * j) {
    statement
}
```
### Esempio 6 (loop infinito)
Utile ad esempio quando dobbiamo far leggere un file e non conosciamo il numero di elementi da far leggere, non esiste una condizione A PRIORI per il ciclo for:
```cc
for(;;) {
    statement
}
```
In questo caso dobbiamo essere noi a implementare dei comandi per fermare il ciclo, come il comando break.
```cc
for(int i = 0; ; i++) {
    statement
}
```
### Esempio 7 (scope)
```cc
for(int k = 0; ; k++) {
    cout << k;
} //da adesso in poi non possiamo usare la variabile k, perchè è dentro una parentesi graffa che è stata chiusa
```
Tuttavia avere variabili FUORI dallo scope è utile, perchè così possiamo riutilizzarle, ecco un esempio di come possiamo "risolvere" questo problema:
```cc
int k = 0; //dichiarata fuori dal ciclo for
for(;;) {
    cout << k;
    k++
}
```
## Come fermare il ciclo for infinito
### Formula generale
```cc
for(;;) {
    statement;
    if(...) break; //questo comando porta direttamente alla fine dell'esecuzione del ciclo for
}
```
Una prima applicazione utile di questa formula è l'interruzione della lettura di un file quando si arriva alla fine di esso, ovvero:
```cc
if(;;) {
    statement
    if(f.eof()) break; //questa cos ala faremo fino alla fine della nostra vita
}
```
## Esercizio della media
Prima calcoliamo la somma e la media da numeri che inseriamo noi, al massimo 5 stavolta.
```cc
int n = 5; //numero richiesto dall'utente
double sum = 0; //se non mettiamo il valore 0 (o qualsiasi altro valore) la variabile viene salvata in memoria con un valore a caso ,IMPORTANTISSIMO
for(int i = 0; i < n; i++) { //i arriverà fino a n-1
    double x; //variabile di supporto
    cin >> x;
    sum += x // += è un modo più corto di scrivere sum = sum + x, idem con patate per -=, ma anche con moltiplicazione e divisione
}
cout << "media=" << sum/n;
```
In questo modo "consumiamo" pochissima memoria, non uno spazio per ogni numero, ma per ogni variabile, che sono solo due.
### Esempio 8 (numero di elementi non noto)
```cc
int n = 0;
double sum = 0;
for (;;) {
    double x;
    cin >> x;
    if(cin.eof) break; //significa "quando sulla tastiera si digita il comando eof, interrompi il ciclo"
    sum += x;
    n++;
}
.
.
.
return 0;
```
Biaogna sempre scrivere prima cin, DOPO la condizione di break (importantissimo).
PRIMA LETTURA POI CONTROLLO.
### Comando eof
Questo comando è molto importante, ed è semplicemente:
```
ctrl+d
```
#### ! Nota bene !
Il comando eof è diverso da quello che interrompe il programma:
```
ctrl+c
```
Quet'ultimo infatti porta proprio alla fine del programma, non alla fine delle parentesi graffe ecco.
### Esempio 9 (caricamento elementi da file)
```cc
int n = 0;
double sum = 0, x; //x variabile di supporto
fstream f; //f è il nome della variabile fstream
f.open("nome_file", ios :: in);
if(!f.good()) {
    cout << "errore apertura file" << endl;
    return -1;
}
for(;;) {
    f >> x; //1. questo è il comando di lettura
    if (f.eof()) break; //2. check del file
    sum += x; //3. comando da eseguire
    n++;
}
```
## 5.2/3/4) Saltati
## 5.5) break e continue
### 5.5.1) break
Serve per varie cose, la prima è uscire dal loop con i cicli detti prima, ma anche per saltare un certo statement per gli switch.
#### Esempio
```cc
while(!cin.eof()) {
    if(...) {
        break;
    }

} //il break porta direttamente qua
```
### 5.5.2) continue
Fa la cosa opposta del break, fa saltare al prossimo loop senza interromperlo.
Esempio, voglio calcolare la media di numeri positivi con cin:
```cc
double sum = 0, x;
while(!cin.eof()) {
    cin >> x;
    if (x < 0) continue; // se la x è negativa si riparte con il prossimo loop, quindi non si somma il numero negativo senza fermare il codice o il loop
    sum += x;
}
```
## ricordo eof()
Se scrivo il comando eof DAL TERMINALE è l'equivalente dell'eof da terminale.
## 5.6) Nested loops
Prima dobbiamo introdurre il concetto di matrice, in cui abbiamo due direzioni, la i (riga) e la j (colonna), bisogna avere presente come è fatta una matrice. Per stampare una matrice possiamo usare il ciclo for per comodità:
### Rappresentazione di una matrice con solo 1 e 0, con 1 lungo una diagonale:
```cc
for(int i = 0; i < 3; i++){
    for(int j = 0; j < 3, j++) {
        if(i==j)
            cout << 1 << " ";
        else
            cout << 0 << " ";
    }
    cout << endl;
}
```
Importante perchè dalla lezione successiva faremo operazione di vettori.
