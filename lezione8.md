# Lezione 8 (Structs)
## Introduzione
Nascono per risolvere un problema abbastanza comune:ad esempio, in un grafico si vuole rappresentare un punto p in questo grafico, con una coordinata x e una coordinata y di riferimento.
Se si ha questa tipologia di problema si intende rappresentare il punto p come un vettore, con coordinate x e y, che assumono datatype double oppure float. Questa cosa si può fare in più dimensioni di due obv.
In c++ la rappresentazione di oggetti di questo tipo può essere semplificata grazie alle "strutture"(struct) e le "class"(queste ultime non vengono trattate nel corso).
## 8.1) Definizione
```cc
struct structName {
    dataType name1;
    dataType name2;
    .
    .
    dataType nameN; //tutti gli N membri della struct
}; //importante il punto e virgola DOPO le parentesi graffe
```
### NB 
Questo va fatto FUORI dal main e in generale dalla funzione.
### Esempio 1 (x, y)
```cc
struct punto {
    double x;
    double y;
};
int main () {
    punto p; //la variabile punto ora si chiama p, è un nuovo oggetto di tipo custom
    .
    .
    return 0;
}
```
### Esempio 2 (struct per salvare costanti)
```cc
struct constants {
    double pi = 3.14;
    double hbar = ...
    .
    .
    
} myconst; //se faccio così l'occetto myconst sarà disponibile per tutto il programma, quindi si usa per produrre una variabile globale
```
## 8.2) Accesso ai membri della struct
### Def:
```cc
structName.nomeMembro;
```
### Esempio 3
```cc
struct punto {
    double x;
    double y;
};
int main () {
    punto p;
    p.x = 2.5;
    p.y = 3;
    .
    .
    return 0;
}
```
### Esempio 4 (Altra modalità di utilizzo)
Si può inizializzare il valore con cin:
```cc
cin >> p.x;
```
Il numero verrà associato solo al valore x del punto p.
### NB 
Con le struct non si hanno "cose fisse". Si fa nel caso si prima solo nell'istanza p.x, se si hano ad esempio f.x questo non viene cambiato.
### Esempio 5 (Con cout)
```cc
cout << p.,x << " " << p.y << endl;
```
### Esempio 6
```cc
punto a, b, c, d;
```
a.x non è uguale a b.x e le altre robe!!!
### Caso particolare
Questo nel caso sappiamo già i valori:
```cc
punto p = {2.5, 3}; //in fase di compilazione si assegna il primo valore alla prima variabile nella struct e così via
```
### Cosa da ricordare
Quando vogliamo "paragonare" due oggetti:
```cc
punto a, b;
a.x = 5;
a.y = 10;
//voglio copiare questi numeri anche con b:
b = a;
/*
equivalente a:
b.x = a.x;
b.y = a.y
*/
```
### Esempio 7
```cc
if (a.x == b.y) ... //questi qua sono oggetti di tipo double
```
## 8.3) Struct e funzioni
Supponiamo di avere una struttura void e di stampare i valori di una funzione:
```cc
void printStruct(punto a) {
    cout << a.x << " " << a.y << endl
}
int main() {
    punto p;
    p.x = 5;
    p.y = 10;
    printStruct(p); //noi stiamo copiando il valore del main nella funzione void, e ricorda, sono delle variabili locali
    .
    .
    return 0;
}
```
### Esempio 8
```cc
void setStruct(punto &a){ //così quindi si passa l'argomento per riferimento, non per copia
    a.x = 10;
    a.y = 20;
}
int main() {
    punto p;
    setStruct(p);
    cout << p.x << " " << p.y << endl;
    .
    .
    .
    return 0;
}
```
Se si passa per riferimento si può modificare il contenuto.
## 8.4) Struct e array
### Stack
```cc
struct punto {
    double xcoord[2];
};
int main() {
    punto p;
    p.xcoord[0] = 5;
    p.xcoord[1] = 10;
    .
    .
    return 0;
}
```
### Heap
```cc
struct punto {
    double *xcoord; //è un puntatore
};
int main() {
    punto p;
    p.xcoord = new double[2];
    .
    .
    p.xcoord[0] = 5;
    p.xcoord[1] = -6;
    .
    .
    delete[] p.xcoord;
    return 0;
}
```
## 8.5) Array di struct
E' una cosa estremamente utile questa!!
```cc
struct punto {
    double x, y;
}
int main() {
    /*con stack
    */
    punto p[10]; //così ho creato un array di tipo punto
    /*con heap
    */
    punto *p = new punto[10];
    delete[] p; //questo è utile per caricare dati
    for(int i = 0; i < 10; i++)
        cin >> p[i].x >> p[i].y;
    .
    .
    return 0;
}
```
### Esempio 9
```cc 
punto p;
p.x = 5;
p.y = 6;
/* 
oppure
*/
punto *p = new punto;
p -> x= 5;
p -> y = 6;
```
## 8.6) Funzioni
Nell'ultima lezione sono state introdotte le funzioni e come dichiarare il funzionamento di queste:
```cc
#include <iostream>
double y(double x) {
    return 4 * x + 5;
}
int main() {
    double k = y(10);
    return 0;
}
```
la funzione deve restituire un valore double.
Ricorda: la funzione deve essere messa prima del main, questo è molto importante.-
In alcuni casi è più comodo avere non tutta la funzione sopra, quindi bisogna dichiarare solo l'esistenza della funzione, e poi esplicitarla, questo è utile quando il programma viene "spaccato" in diversi file.
```cc
#include <iostream>
double y(double x); //questa cosa si chiama "signature"
int main() {
    double k = y(10);
    return 0;
}
double y(double x) {
    return 4 * x + 5;
}
```
Adesso passiamo a un ragionamento più "complicato":
## 8.7) Header(s)
Sono i file che hanno un'estensione *.h (ad esempio iostream, fstream, ecc...)
Ad esempio possiamo creaere un file fun.h per includere le funzioni in un file *.cc.
In questo caso così i file sorgente sono due: main.cc e fun.cc.
Quindi per compilare:
```makefile
g++ -o prog main.cc fun.cc ...
```
### File 1:
#### Header: functions.h
```h
void setValue(double &x, double y);
//la regola è solo dichiarare la signature, non bisogna dire cosa fa la funzione
```
#### functions.cc
```cc
#include "functions.h" //se il file è nostro usiamo gli apici e scriviamo il nome intero del file
void setValue(double &x, double y) {
    x = y;
}
```
#### main.cc
```cc
#include "functions.h"
int main() {
    double v;
    setValue(v, 5);
    .
    .
    .
    return 0;
}
```
Ecco, questo era un esempio di "spaccamento" del programma, abbiamo spostato le funzioni all'interno di altri file, con un'header e un file in cui si mette "in azione" la funzione, tutto questo per "snellire" il main. Adesso eseguiamo il programma:
```make
g++ -o main.cc functions.cc


oppure


g++ -c functions.cc
.
.
.
g++ -o prog functions.o main.o
questo secondo modo serve per "spezzare" la compilazione, per rendere più veloce la compilazione
```
## 8.7) stringstream
Il "problema" è creare un'unica stringa che rappresenti tutto il contenuto del nostro programma.
```cc
cout << "hello" << a << ... << endl; //noi vogliamo però "salvare la serie di cose stampate
```
```cc
#include <sstring>
stringstream ss;
ss << "hello" << a << .... << endl;
cout << ss.str();
string a = ss.str;
```
Questo è importante perchè è comodo stampare sul terminale il risultato e salvare il risultato su un file.
Ecco quanto è lungo fare senza sstream:
```cc
int main() {
    cout << "hello";
    fstream f;
    f.open("...", ios :: out);
    f << "hello;
}
```
Invece:
```cc
stringstream ss;
ss << "hello";
print(ss);
/*definita come:
void print(stringstream &v){
    cout << v.str();
    fstream f;
    f.open(...);
    f << v.str();
}  */
```
## 8.8) Loading dati
#### data.dat (numero imprecisato di elementi)
Metodo per are il conteggio dei dati di un file;
```cc
fstream f;
f.open("data.dat", ios :: in);
int count = 0;
string tmp;
for(;;) {
    getline(f, tmp);
    if(f.eof()) break;
    count ++;
}
cout << count;
```
Questa cosa si può fare anche con while:
```cc
while(f.peak()!=EOF) {
    getline(f, tmp);
    count++;
}
```
Procediamo con la lettura vera e propria dei dati, ovvero l'obiettivo è tornare a capo del file:
```cc
f.clean();
f.seekg(0);
f >> ...
```
Questa è una cosa "aggiuntiva", ma MOLTO importante.
