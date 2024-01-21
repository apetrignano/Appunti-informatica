# Lezione 3
## 3.1) iostream
Con #include <iostream> si inserisce cin e cout (appunto input e output)
(si scrive sempre using namespace std; perche' si)
```cc
int main () {
    codice
    return 0;
} //questo è il body della funzione
``` 
### Significato "using namespace std" 
(prima scrivo con e poi senza), si puo' fare senza ma e' piu' difficile.
#### Con:
```cc

#include <iostream>
using namespace std;
int main () {
    cout << "afammoc" << endl;
    return 0;
}
```
#### Ora facciamo quindi senza:
```cc
#include <iostream>
int main (){
    std :: cout << afammoc << std :: endl;
    return 0;
    } //in questo caso abbiamo spostato il std ogni volta all'interno del programma.
```
Iostream e' il grande contenitore che contiene std (libreria standard di c++), che contiene cout, cin eccetera.
A volte non e' possibile utilizzare std, molto piu' avanti con la carriera 
c'e' una terza possibilita', ovvero dichiarare tutti i namesapce che si vuole usare:
ad esempio:
```cc
using std :: cout; //in questo caso quindi si include SOLAMENTE il cout senza doverlo "introdurre"
```
## 3.2) cmath
si puo' fare #include un numero illimitato di volte:
```cc
#include <iostream>
    #include <cmath>
    using namespace std;
    itn main (){
        sin (5);
        cos (7);
    }
```
cmath contiene le funzioni trigonometriche standard, le funzioni trigonometriche iperboliche, poi : asin, acos, atan, exp (Ex = e^x == esp (x)), poi log, log10..., abs (valori assoluti), fabs, le potenze (square, radice di due,) pow, la potenza (es pow (base, expo)), radice quadrata: sqrt (n). 
### Ad esempio
Voglio calcolare 2^(1/3): 
```cc 
double b = 2;
double e = 1/3.0;
cout << pow (b,e) ,, endl; // cosi pero non la abbiamo "salvata"
double c = pow (b,e); //diciamo questo per avere la variabile disponibile all'interno del programma
cout << c << endl;
```
## 3.3) String
```cc
char n = 'a';
char n [] = "hallo"; //la n va dichiarata sulla stessa riga e le parentesi quadre sono da tenere vuote se no si sa la "dimensione" del coso la'
```
In questo caso la size e' semplice, i blocchi di memoria sono pochi e li conosciamo ( con blocchi di memoria si intende ciascuna lettera) quindi:
```cc
char n [6]= "hello"; 
cout << n ;
```
Si possono anche stampare componenti specifiche, nel cout mettiamo:
```cc
cout << n [3]; //ed esce "l", questo perche' la prima lettera e' lo zero, in c++ si inizia a contare dallo zero
```
la costruzione di questo char e' basato su blokki di memoria.
### Problema 1: 
Se si definisce una n non si puo' modificare ' il contenuto di sta roba, quiiiiiindi c++ ha introdotto #include <string>, quindi poi si puo' fare 
```cc
string n = "hello";
cout << n; //poi si puo' fare dopo: 
n = "cioao!!!" //si puo'' modificare la string.
```
## 3.4) cin/cout
```cc
#include <iostream>
#inclue <string>
using namesapce std;
int main () {
    int a;
    cin >> a ;
    int b, c;
    cin >> b >> c; //si scrivono le variabili in cin
    string t;
    cin >> t;
    cout << b << c; //cosi si stampano i due numeri messi tutti assieme, se b=7 e c=8 esce "78"
    quindi si fa cout << b << << c ; //--> 7 8, abbiamo messo lo spazio
    cout << "b=" << b << " ", c=" << c ;
     }
```
## 3.5) makefile
```makefile
$ make (con il dollaro si indica il terminale)
```
### Sintassi: 
``` makefile
target:dependence
    cmd1   (è fondamentale mettere la tab, se no non funziona nulla)  
    cmd2
    .
    .
    .

all: prog1
    prog1: main.cc

g++ -o prog1 main.cc
    $ make prog 1
    $ make (se si scrive solo make si fanno partire tutti i programmi)
```

NB non ho seguito piu un cazz su make, sarebbe da rivedere.
## 3.6) I/O files
Serve per riportare salvati i risultati stampati su schermo.
```cc
#include <fstream> 
using namespace std;
int main () {
    fstream g; //come se fosse un intero, un double, un chart, ecc
    //input
    g.open ("nome_file_da_aprire.txt/dat", ios :: in); //per leggere il file
    //output
    g.open("nomefile.txt", ios :: out); (per aprire il file)
    //poi pero' se il programma non riesce ad aprire il file non lo dice, si deve fare:
    g.good (), //si mettono true e false, variabili bool (bool k = g.good)
    g.close (); //serve per chiudere il file
    g.eof (); //end of file, per dire se la lettura e' arrivata fino alla fine
//read from:
    g >> d; (==cin >> d) //g dal file, tutto questo e' uguale a scrivere ios :: in
//write to:
g << d;
g << "hello" //uguale a ios :: out
```
## 3.7) funzioni di controllo
```cc
int a = 10;
if (a==10) {
    cout << "si, e uguale a 10" ; 
} //se il controllo non da esito positivo, semplicemente cosi si salta il programma, e continua a controllare piu avanti
```
### Oppure per piu variabili:
```cc
int a,b;
if(a==10 && b<5) {
comando1
} else {
comando2
} //questo per non mandare avanti alla compilazione
```
### esempio:
```cc
#include <iostream>
using namespace std; 
int main () {
    fstream g;
    g.open (file.dot, ios :: in);
    if (g.good()==false) {
    cout <<"bad file";
    return -1; //non fa return 0 perche il file non e andato a buon fine, serve per non far andare avanti il programma

    } 
    return 0;
}
``` 
    
 
