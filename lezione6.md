# Lezione 6 (array)
## Ricordo 
* come e' composto un vettore (le sue componenti) con valori appartenenti a R, e anche della notazione trasposta;
* shape [n,1], in notazione trasposta [1,n].
## Array
### Definizione: 
- E' una "collezione" di n elementi dello stesso type salvati in uno spazio di memoria (non possiamo quindi creare vettori con data type diversi).
- Ci sono due tipi di array:
1. "stack" (dimensione fissa, predefinita, i calcoli sono molto piu' veloci); 
1. "heap" (dimensione dinamica, sono scritti sulla ram, ovvero fuori dalla CPU).
## Stack array
### Definizione:
dataType *(int, double ecc)* arrayName [intExp (puo' essere una costante, un numero intero, una macro(??))] 
### Esempio 1:
```c++
int v [3] //le caselle sono riempite con 0, 1, 2.
//n.b il conteggio va da 0 fino a N-1 (prima n=3)
```
### Esempio 2: 
```c++
const int N = 3;
 int [N]  //importante perche' questo valore deve essere una costante, non deve essere modificabile
```
### Esempio 3: 
```c++
#include <quello che vuoi>
 # define N 3 //questo e' la macro
int main () {
int v [N] //la N viene definita fuori dal main, quindi non puo' essere modificata
 }
 ```
### Pro e contro degli stack:
### PRO: 
- accesso veloce ai dati;
- "automatic management";
- "memory management" efficiente.
### CONTRO: 
- la dimensione e' limitata;
- la dimensione e' fissa (dobbiamo sapere esattamente la dimensione del vettore);
- lavora con delle variabili locali (e magari invece e' utile tenerle).'
### Esempio: 
```c++
int list [10];
list [0] = 1;
list [1] = 5;
.
.
.
cout: for (int i = 0; i < 10; i ++)
    cout << list [i] >>;
```
### Altri esempi:
### 1. Media:
```c++
const int N = 10;
double v[N], sum = 0;
for (int i = 0; i < N; i ++)
    cin >> v[i];
for (int j = 0; j < N; j ++)
    sum += v[j];
cout << sum / N;
```
### 2. Media con un numero ignoto di elementi:
```c++
int n = 0; //fara' il conteggio degli elementi inseriti
const int N = 10000; //e' il numero massimo di elementi consentiti
double v[N], x;
for (;;) {
cin >> x;
if (cin.eof()|| n > N-1) break; //eof sarebbe ctrl+d
v[n] = x;
n ++;
}
for (int i = 0; i < n; i ++)
sum += v [i];
cout << sum / n <<; //non e' ottimale perche' e' un po' uno spreco di memoria
```
## Inizializzare gli stack array 
Si possono assegnare subito gli elementi;
```c++
double p[3] = {2.0, 2.5, 3.7};
double p [ ] = {2.0, 3.5, -4.7, ....} //viene contato il numero di elementi
int l[10] = {0}; //inizializzo al valore 0 tutti gli elementi
double v[20] = {0, 1, 2} //cosi' facendo a tutti gli altri elementi viene assegnato il valore 0
```
### Problemi comuni: 
- Stack overflow, avviene quando:
```c++
int a[10]
cout << a[10] <<; //segfault, ricordo che si parte da 0, quindi la posizione 10 non e' inclusa
```
- Operazioni "vietate":
```c++
double a[5], b[5];
b = a; E' SBAGLIATO
```
La formula giusta e' cosi':
```c++
for (i = 0; i < 5; i ++)
b[i] = a[i];
```
``` c++
cin >> a; SBAGLIATO
```
Sintassi giusta:
```c++
cin >> a[0];
.
.
.
```
## PRODOTTO SCALARE
double s = 0;
```c++
for (inf k = 0; k < 5; k++)
    s += a[k] * b[k];
cout << "prodotto scalare: " << s << endl;
```
## Stack array in 2D
#### Def: 
```c++ 
dataType nameVan[N][M]; 
```
#### ex: 
```c++
int A[5][5];
A[0][0] = 1;
for (int i = 0; i < 5; i++)
 for (int j = 0; j < 5; j++)
  cout << A[i][j];
```
## Dynamic array
#### Def:
```c++
dataType *arrayname = new dataType [ int expression];
```
### ex. 
```c++
double *v = new double [10]; //10 e' la dimensione dell'array, cosi' abbiamo inizializzato questo array dinamico
//era un metodo heap (1)
delete [] v; //il processo di pulizia della memoria va fatto a mano, alla fine del programma (2)
```
### Pro e contro di heap:
#### pro: 
- usa la ram e a volte e' comodo;
- dimensione dinamica.
#### contro: 
- e' lento;
- la gestione della memoria non e' automatica.
#### ex. 
```c++
int *a = new int[5];
a[0] = 1;
a[1] = 3;
.
.
a[4] = -3;
for (int i = 0; i < 5; i++)
  cout << a[i];
delete[a];
```
#### ex. 
```c++ 
int n;
cin >> n;
int *v = new int[n];
.
.
.
delete[] v;
```
## Algoritmi di base:
### Media: 
```c++
const int n = 100;
double v[n];
..parte algoritmo;
double sum = 0;
for (int i = 0; i < n; i++)
    sum += v[i];
double m = sum / n;
```
### Deviazione std: 
```c++
double std = 0, sum2 = 0; 
for (int i = 0; i < n; i++)
    sum2 += pow(v[i] - m, 2);
std = sqrt (sum2 / (n-1));
```
### Max value: double v[n];
```c++
double max = v[0];
for (int i = 1; i < n; i++)
    if (v[i] > max)
        max = v[i]; 
```
### min value: 
```c++
double v[n];
double min = v[0];
for (int i = 1; i < n; i++)
   if (v[i] < min)
    min = v[i];
```                             
### Search (ordine n lineare): vogliamo un numero con la x = 7:
```c++
double x = 7;
int iloc = -1;
for (int i = 0; i < n; i++){
    if v[i] == x {
        iloc = i;
break;
}
}
cout << v[iloc]
```
### Ordinamento in ordine di vettorI (selection sort): 
#### Richiesta: dato un v[n], posso metterli in ordine crescente?
### Soluzione: 
```c++   
for (int = 0; i < n - 1; i++)
for (int j = i + 1; j < n; j++)
    if (v[i] > v[j]) {
        double tmp = v[i];
v[i] = v[j];
v[j] = tmp;
} //se vogliamo l'ordine decrescente ===> v[i] < v[j]; (ovviamente nella parte if)
```
