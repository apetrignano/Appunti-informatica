# lezione 4 
## Ripasso fstream
Ha due utilizzi: di input e di output (ovvero lettura e scrittura su file).
### Input
```cc
#include <iostream>
#include <fstream>

int main () {
    fstream v;  //questo è importante, dichiara la variabile
    v.open("nome_file", ios :: in);
    if (!v.good()){ //il punto esclamativo è la negazione, quindi quando il booleano è false
    return -1 //il programma si ferma a questa riga, si può anche aggiungere con cout che il programma è crashato
    }
    v >> //per la lettura, importante
    //(cin >> ...) 
    v.close (); //per chiudere il file
    return 0;
} 
```
### Output
```cc
#include <iostream>
#include <fstream>

int main () {
    fstream v;
    v.open ("nome_file", ios :: out); //out è l'unica differenza pratica
    if (!v.good()) {
        return -1
    }
    v << //per la scrittura, importante
    //(cin << ...)
    v.close ();
    return 0;
}
```
## 4.1)  Algoritmi di selection
### 4.1.1) One-way selection
Significa introdurre un pezzo di codice per una situazione precisa, per poi diciamo arrivare alla fine stessa riga di codice di se quella situazione non si fosse verificata.
#### Formula generale:
```cc
if (expression) {
    statement
} //n.bb Nell'expression servono operatori relazionali diciamo, ora metto degli esempi
```
#### Esempi operatori relazionali:
```cc
a == b //uguaglianza
a != b //disuguaglianza, anche qui punto esclamativo è negazione
a < b //minore 
a > b //maggiore
a <= b //minore o uguale
a >= b //maggiore o uguale
```
Ovviamente ogni relazione può essere solo due cose: giusta o sbagliata (true o false), quindi booleana, a seconda del booleano l'if condition decide se eseguire o no lo statement.
#### Esempio pratico:
```cc
8 == 6 //restituisce false (0)
8 < 15 //restituisce true (1)  
```
#### Altro esermpio:
```cc
int a = 10,  b = 2;
if(a == 10) { //valore true
    cout << "a è uguale a 10" << endl;
}
if (a > b) { //ancora valore true
    cout << "a è maggiore di b" << endl;
}
```
Possiamo anche fare in un altro modo, ovvero introdurre prima il booleano che "verifica la cosa":
```cc
bool c = (a == 10) //è quindi la condizione che poi dice che c è true
if (c) { //significa proprio: se c restituisce true allora esegui lo statement
    statement
}
```
### 4.1.2) Two-way selection
Non è molto diverso dal one way selection, quindi in sostanza significa assegnare uno statement ANCHE al valore false, o il contrario ecco.
#### Formula generale:
```cc
if (exp...) {
    statement 1
} else  {
    statement 2
}
```
#### Esempio 1:
```cc
int a = 10;
if (a > 0) {
    cout << "a è positivo"; //a > 0 -->true
} else {
    cout << "a è negativo"; //a < 0 --> false
}
```
Nel caso di prima è ovvio che si comporta così, però se metto un cin lo fa in automatico ad esempio.
### 4.1.3) Multi-way selection
La struttura è circa come il two-way, però è più complessa.
#### Formula generale:
```cc
if (exp...) {
    statement 1
} else if (exp2..) {
    statement 2
} else if (expn...) {
    statement n
} else{ //chiamato "resto"
    statement finale
}
```
#### Esempio 1 (condizioni contemporanee):
```cc
int a = 5, b = 10;
if (a > 0) {
    if (b < 50) {
        cout << "hello"; //la condizione è che a deve essere maggiore di 0 E b minore di 50, si potrà fare in un modo più semplice
    }
}
```
Ecco il modo più semplice:
```cc
if (a > 0 && b < 50) {
    cout << "hello"; //se una delle due non è verificata il booleano è false
}
```
#### Esempio 2 (condizioni "oppure"):
Si usa questa cosa per non scrivere due volte lo stesso statement e snellire il codice:
```cc
int a = numero, b = numero;
if (a < 0 || b > 5) {
    cout << "hello";
}
```
#### Esempio 3 (mix delle cose precedenti):
```cc
if (a > 0 || (a < 5 && b > -10)) { //deve verificarsi la prima condizione OPPURE la terza e la quarta contemporaneamente
    statement
} //n.b. Occhio alle parentesi, come in matematica, se si vogliono combinare due espressioni concateniamo nel modo opportuno attraverso le parentesi
```
#### Esempio 4:
```cc
int a = 10:;
if (a > 5) {
    a = 2*a;
} else {
    a = 3*a
}
```
Questa cosa si può scrivere anche in un altro modo:
```cc
ina a = 10;
a = (a > 5)? 2*a : 3*a; //può essere utile se si vuole scrivere "in line", se la condizione è true si esegue l'espressione prima dei due punti, dopo se la condizione è false
```
In Phyton si usa parecchio sta cosa.
## 4.2) Debugging
Significa semplicemente controllare cosa non funziona nel programma, soprattutto se il compilatore dice che è tutto ok, quindi c'è un problema di LOGICA.
### Steps:
#### 1. verificare il contenuto delle variabili;
#### 2. verificare i dati di input.
La soluzione è usare il cout per verificare i contenuti di queste variabili, se è tutto giusto si mettono le due parentesi davanti al cout per "togliere" il pezzo di codice alla fine.
#### Esempio 1:
```cc
f >> a;
cout << a; //per vedere se il contenuto della variabile a è quello giusto
```
#### Esempio 2:
```cc
n++;
cout << n; 
cout << n++ //ancora meglio
```
#### Esempio 3 (più utile):
```cc
double x = -1;
cout << x;
double y = sqrt(x); //un casino perchè è un numero complesso
```
VScode mette a disposizione strumenti molto utili per "tracciare le variabili" e altre cose, come gdb, trace...
## 4.3) Escursus scope, variabili e parentesi
Le variabili possono essere locali oppure globali, le prime sono racchiuse dentro una parentesi graffa, e sono dichiarate in quello scope, che appunto sono le parentesi graffe, o meglio in quella funzione, e fuori da quello non valgono; invece le variabili globali esistono FUORI dagli scope e sono dichiarate fuori.
#### Esempio:
```cc
#include <iostream>
double f = 3; //questa è una variabile globale
int main() {
    double g = 9.8; //questa è una variabile locale
}
``` 
### Per gli esercizi:
Quando ci troviamo una disequazione, per calcolare quella con delta negativo, dobbiamo tenere a mente che:
```
 reale: x1,2 = -b/2a
 immaginaria: x1,2 = +- (i * sqrt(-D) / 2c)
```
