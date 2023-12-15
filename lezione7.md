# puntatori
## 7.1 Definizione: datatype.variabile;
sono tipi di dati che rappresentano la posizione  in memoria (variabili, classi...).
- ad es. int;
```c++
int * a; //non e' un prodotto obv
```

Per definire piu' variabili: 
```c++
int * a; * b; //l'asterisco va ripetuto, importante
```
        
## 7.2 A che serve?
Ah bho.
## 7.3 Sfilza di esempi
ah bho.
### Esempio: assegnare indirizzo al puntatore:
#### Legenda:
+ &x = posizione di x, cosa molto importante.
```c++
int x = 5; //abbiamo assegnato un valore 5 in una posizione della memoria
int * p; //che e' vuoto
p = &x; //vuol dire che nella casella della memoria del puntatore c'e' l posizione di x
cout << x << endl; //esce come risultato il numero 5
cout << &x << endl; // vuol dire che esce la posizione di x
cout << p << endl; //esce la posizione di x di nuovo, valore del puntatore
cout << &p << endl; //esce la posizione di p 
cout << *p < endl; //per il profe la cosa piu' interesting, esce il VALORE PUNTATO da p
```
### Altro step:
```c++
x = 6; // * p vale 6 ora, quindi il ountatore si aggiorna, e' meno sbatti
* p = 7; //ne segue che adesso p vale 7 
```
Quindi e' evidente che * p e x sono collegati.
## 7.4.1 : Inizializzazione puntatori
### Esempio
```c++
int * p = NULL; //oppure anche (vedi sotto)
int * p = 0; //sono equivalenti
if (p == NULL) {
    .
    .
    .
} //questo e' per conoscere lo stato del puntatore
```
### OP.NEW
* new dataType; (allocation 1 variabile)
* new dataType [intExp]; (array di variabili)
### Esempio
```c++
int * v = new int [2];
v[0] = 2; // segue che v[1] = 3
```
## 7.4.2 : Operatore delete
ovviamente questi puntatori vanno anche eliminati:
```c++
//allocation
dataType * v = new dataType;
//deallocation
delete v;
//allocation
dataType * v = new dataType [size];
//deallocation
delete [] v;
```
Vediamo che quindi se facciamo allocation con le parentesi va fatta deallocation con parentesi.
## 7.5 : Operazioni con puntatori
consideriamo int * p, * p;
```c++
op. p = q //punteranno verso lo stesso indirizzo
op. p == q, p! q //confronto tra indirizzi
* p == * q, * p! = * q //e' un confronto tra valori puntati
op. p++ oppure p = p = 1 //imp: questo e' uno spostamento del valore di p, ovvero si sposta tra INDIRIZZI
```
## 7.6 Funzioni in c++
Ovviamente nel programma ci possono essere altre funzioni oltre alla main, di base le funzioni sono di due tipi:
* return un valore; (A)
* return void. (B)
## A
```c++
int main () { //main nome della funzione, tra le parentesi ci sono gli eventuali argomenti

return 0; //return value, che e' una int
}
```
### Esempio
```
y(x) = 3*x + 5 
```
### Svolgimento:
```c++
double y(double x) {
    return 3*x + 5;
}
int main () {
    cout << y(9.5) << endl; //qui abbiamo inserito il valore 9.5 nella x della funzione prima
double t = -3.5;
double x = y(t);
}
```
### Massimo tra 2 double
```c++
double max(double a, double b){ //bisogna sempre scrivere i datatype, quindi se e' int etc
double r;
if(a > b)
    r = a;
else
    r = b;
return r;
} 
```
Oppure possiamo fare in un altro modo:
```c++
int main () {
    cout << max(5, 7) << endl;
    double w = 5, z = 7;
    double p = max (w, z);
    return 0;
}
```
## B
```c++
void prodotto(double a, double b){
    cout << a * b << endl;
}
int main () {
    prodotto(5, 4);
    .
    .
}
```
N.B. il main non e' per forza il luogo dove fare calcoli eccetera.
## 7.7 Funzioni per argomento e/o riferimento
```c++
double y(double x) {
    x = 5;
    return 3*x+5;
}
in un'altra parte del programma:
y(9);
double w = 9;
y(w);
cout << w << endl; //lo scope locale sovrascrive quello esterno 
```
* per riferimento:
```c++
void y(double &x){
    x = 5;
} 
piu avanti con il programma:
double w = 9;
cout <<w; //esce 9
y(w);
cout << w: //esce 5
```
### Sintassi c-style
```c++
void y(double *x){
    *x = 5;
}
piu avanti magari anche nel main:
double w = 9;
y(&w);
cout<< w; // esce 5
```
### Esempio (scambio di 2 valori)
(in c++):
```c++
void scambia(double &a, double &b){
    double dep = a;
    a = b;
    b = dep;
}
.
.
.
double z = 2, k = 1;
scambia(z, k);
cout << x << " " << k; //dovrebbero uscire 1 e poi 2
```
(in c):
```c++
void scambia(double *a, double *b){
    double dep = *a;
    *a = *b;
    *b = dep;
}
.
.
.
double z = 2, k = 1;
scambia(&z, &k);
cout << z << " " << k; //escono 1 e poi 2
```
## 7.8 Funzioni per array
```c++
void print(int *v, int n){
    for (int i = 0; i < n; i++)
        cout << v[i] << endl;
}
__________________________________
void print (int v[], int n) {
    for (int i = 0: i < n; i++)
        cout << v[i] << endl;
}
```
```c++
int main() {
    int *w = new int [10];
    .
    .
    .
    print(w, 10);
    .
    .
    .
    delete [] w;
    return 0;
}
```
