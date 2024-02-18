# Lezione 9
## 9.1) scp/cp
Come sappiamo, cp è il comando di copia, scp invece è il "secure copy", fa riferimento al "sistema" per avere sicurezza durante la copia, i dati vengono criptati durante il trasferimento.
Questa cosa è utile diciamo per trasferire i file da pc a un altro pc in remoto.
Per collegarsi noi abbiamo già visto ssh:
```
ssh username@IP
```
### Da locale a remoto
Dal punto di vista sintattico:
```
scp <file> username@IP:~/
```
Così abbiamo copiato il fle sulla home della macchina, partiamo da dove siamo e da dove vogliamo andare.
Invece con le cartelle:
```
scp -r <nome_directory> username@IP:<percorso_per_esteso>
```
n.b. username si usa solo se gli username da locale a remoto sono diversi, altrimenti si può omettere.
### Da remoto a locale
Siamo a casa e vogliamo copiare un file dalla macchina al nostro computer, questo è perchè è difficile, dalla macchina, mandare file al computer a casa:
```
scp username.IP:/home/test/file.cc .
```
Il punto è per indicare il punto preciso in cui ci si trova, volendo si può anche scrivere il persorso dove si vuole mandare il file.
## Per l'esame:
# NB: questa cosa va memorizzata perchè è di un'importanza fondamentale, non saperlo è una vergogna
La richiesta classica è creare una cartella (dove mettere i file) chiamata: cognome_matricola.
### Dalla macchina di laboratorio
Sul terminale:
```
mkdir <cognome_matricola>
cd <cognome_matricola>
cp /home/comune/.../<nome_file_da_copiare> .
```
Così ho preso i dati e li ho copiati nella mia cartella.
Nel caso dobbiamo copiare più dati ripetiamo il processo.
Una volta finito l'esame procediamo alla consegna.
```
cd ..
cp -r <cognome_matricola> /home/comune/...
```
### Dal computer di casa
Sul terminale:
```
mkdir <cognome_matricola>
cd <cognome_matricola>
scp username@tolab.fisica.unimi.it:/home/comune/.../file.cc .
```
Adesso passiamo alla consegna:
```
cd ..
scp -r <cognome_matricola> username@tolab.fisica.unimi.it:/home/comune/.../...
```
## 9.2) Plotting
### Cos'è
Obv è un grafico, molto utile in fisica, a noi servono gli scatter plot, error bar plot, istogrammi. 
### Come farli
In sostanza dobbiamo controllare una matrice di pixel, assegnando a ciascun pixel un colore specifico.
Il problema è che quando programmiamo dobbiamo cercare di "mappare" i colori e poi chiedere al computer di inviare il risultato sullo schermo, la seconda parte è fatta dalla scheda grafica diciamo, la prima invece è responsabilità nostra.
esempio: (su c++)
```cpp
void draw()
{
    clClearColor(0.0f, 0.0f, 0.0f); //così è tutto scuro
    glBegin (GL_TRIANGLES);
    .
    .
    .
    glEnd()
}
```
Per questo su c++ usiamo la libreria opengl.
### Per fare cose più "complesse"
Ci sono altre librerie a un livello più alto, in cui la mole di lavoro è minore, ma anche tipo unity.
### iostream
Si può stampare direttamente sul terminale usando iostream,  l ragionamento è sempre lo stesso: si passando le coordinate x e y e l'algoritmo si occupa di stampare le cose al posto giusto.
### In pratica
Dal punto di vista grafico si cercano librerie, come openGl, oppure ROOT, che è "ottimo" per i fisici, poichè è stato sviluppato proprio per questo scopo, ma è molto macchinoso, ed è stato "superato" da python, ma comunqnue utile perchè si gestisce tutto in c++.
### Altre alternative
Una molto semplice è gnuplot, che ha una sintassi diversa da c++.
```
gnuplot
plot <funzione da disegnare>
```
C'è anche matlab e altre robe.
## 9.3) Python
Sarebbe uno dei linguaggi più potenti per fare grafici, così non siamo limitati dalla sintassi di gnuplot, in cui non possiamo modificare grafici eccetera.
Anche python è un linguaggio costruito TRAMITE c, anche se il linguaggio è diverso. Tutte le grosse librerie di calcolo si basano su python. Diversamente da c++, python è in continua evoluzione, quindi bisogna usare la versione più recente.
### Nella pratica
Per far partire python dal terminale bisogna andare sul terminale e digitare:
```
python3
```
E si apre un "menù interattivo", che non può essere niente se non interattivo.
Ovviamente è pratico perchè non bisogna compilare, eiste quindi un errore in fase di esecuzione.
La seconda differenza fondamentale è la "performance". Volendo si può anche non scaricare python e fare le cose online diciamo.(jupyter)
### Python interpreter
Abbiamo un linguaggio di programmazione interpretato, la meccanica è diversa, il codice è già pronto e si fa eseguire il programma da una macchina che fa l'interpretazione in tempo reale e si occupa di far fare il tutto alla macchina.
Il problema è che è "lento", dicono, ma se è usato con le librerie ottimizzate il tutto si semplifica, le librerie obv sono scritte in c/c++, non è che si usa il linguaggio per fare tutto quello che serve, ma si scrive quello che serve per poi far fare le cose.
### Esempio
```
code main.cc main.py
```
### main.cc
```cpp
#include <iostream>
using namespace std;
int main()
{
    cout << "hello world C++" << endl;

    return 0;
}
```
### Esecuzione:
```
g++ main.cc -o prog
./prog
hello world C++
```
## main.py
```py
print("Hello world Python")
```
### Esecuzione:
```
python main.py
Hello world Python
```
### Altri esempi:
## main.cc
```cpp
#include <iostream>
#include <string>
using namespace std;
int main() 
{
    double a = 5.3;
    double b = -12;
    int c = 100;
    string d = "ciao";
    cout << a + b / c << endl;

    return 0;
}
```
## main.py
```py
a = 5.3
b = -12
c = 100
d = ciao
print(a + b / c)
```
Quindi differenza principale: non bisogna dichiarare le variabili int, double, eccetera, non c'è "strong datatype", poi non ci sono in punti e virgola.
### Rappresentare una funzione
## main.cc
```c++
#include <iostream>
using namespace std;
double y(double x)
{
    return 2 * x -5;
}
int main() 
{
    cout y(10) << endl;

    return 0;
}
```
## main.py
```py
def y(x):
    return 2 * x - 5
print(y(10))
```
La cosa più importante è che bisogna andare a capo con la tab, come nel makefile.
### Ciclo for
## main.cc
```c++
for(int i = 0; i < 5; i++)
    cout << i << endl;
```
## main.py
```py 
for i in range(5):
    print(i)
```
Tuttavia programmare in c++ è estremamente più veloce, per quaanto riguarda la compilazione, questo perchè python non ha una "visione d'insieme".
## Altra cosa importante
## I moduli
Moltissime persone lavorano alle librerie python, qunidi si possono scaricare in modo molto utile
## matplotlib
Questa libreria è fondamentale, serve per creare grafici, basta andare sul sito e copiare il grafico che vogliamo fare, è davvero importantissimo.
