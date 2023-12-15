Lezione 3
3.1) iostream
     Con #include <iostream> si inserisce cin e cout (appunto input e output)
     si scrive sempre using namespace std; perche' si;
     int main () {
        codice
        return 0;
     } questo e' il body della funzione
    significato using namespace std (prima scrivo con e poi senza), si puo' fare senza ma e' [piu' difficile]
     #include <iostream>
     using namespace std;
     int main () {
        cout << "afammoc" << endl;
        return 0;
     }
     ora facciamo quindi senza:
     #include <iostream>
     int main (){
        std :: cout << afammoc << std :: endl;
        return 0;
     } in questo caso abbiamo spostato il std ogni volta all'interno del programma. ' 
     iostream e' il grande contenitore che contiene std (libreria standard di c++), che contiene cout, cin eccetera.
     A volte non e' possibile utilizzare std, molto piu' avanti con la carriera' 
     c'e' una terza possibilita', ovvero dichiarare tutti i namesapce che si vuole usare:
     ad es: using std :: cout; //in questo caso quindi si include SOLAMENTE il cout senza doverlo "introdurre"
3.2) cmath
     si puo' fare #include un numero illimitato di volte 
     es #include <iostream>
        #include <cmath>
        using namespace std;
        itn main (){
            sin (5);
            cos (7);
        }
    ' cmath contiene le funzioni trigonometriche standard, le funzioni trigonometriche iperboliche, poi : asin, acos, atan, exp (Ex = e^x == esp (x))
    poi log, log10..., abs (valori assoluti), fabs, le potenze (square, radice di due,) pow, la potenza (es pow (base, expo)), radice quadrata: sqrt (n), 
      es.voglio calcolare 2^(1/3): 
          double b = 2;
          double e = 1/3.0;
          cout << pow (b,e) ,, endl; // cosi pero non la abbiamo "salvata"
          double c = pow (b,e); //diciamo questo per avere la variabile disponibile all'interno del programma
          cout << c << endl;
3.3) string 
     char n = 'a';
     char n [] = "hallo"; (la n va dichiarata sulla stessa riga)           (le parentesi quadre sono da tenere vuote se no si sa la "dimensione" del coso la',)
     in quessto caso la size e' semplice, i blocchi di memoria sono pochi e li conosciamo (blocchi di memoria si intende le lettere) quindi: char n [6]= "hello"; cout << n ;
     si possono anche stampare componenti specifiche, nel cout mettiamo: cout << n [3]; ed esce "l". (questo perche' la prima lettera e' lo zero, in c++ si inizia a contare dallo zero)
    la costruzioen di questo char e' basato su blokki di memoria.
    problema 1: se si definisce una n non si puo' modificare ' il contenuto di sta roba, quiiiiiindi
    c++ ha introdotto #include <string>, quindi poi si puo' fare ' string n = "hello"; cout << n; poi si puo' fare dopo' n = "cioao!!!", si puo'' modificare la string.
3.4) cin/cout
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
            quindi si fa cout <<b<< <<c ; --> 7 8
         cout << "b=" << b << " ", c=" << c ;
     }
3.5) makefile
    $ make (con il dollaro si indic il terminale)
    sintassi: 
      target:dependence (invio)
      (si fa tab, fondamentale) cmd1    
                                cmd2
                                .
                                .
                                .
      all: prog1
      prog1: main.cc
      (tab) g++ -o prog1 main.cc
    $ make prog 1
    $ make (se si scrive solo make si fanno partire tutti i programmi)
    NB non ho seguito piu un cazz su make, sarebbe da rivedere.
 3.6) I/O files
      serve per riportare salvati i risultati stampati su schermo.
      #include <fstream> 
      using namespace std;
      int main () {
         fstream g; (come se fosse un intero, un double, un chart, ecc) 
         (input)
         g.open ("nome_file_da_aprire.txt/dat", ios :: in); (per leggere il file)
         (output)
         g.open("nomefile.txt", ios :: out); (per aprire il file)
         poi pero' se il programma non riesce ad aprire il file non lo dice, si deve fare:
         g.good (), si mettono true e false, variabilli bool (bool k = g.good)
         g.close (); (serve per chiudere il file)
         g.eof (); (end of file, per dire se la lettura e' arrivata fino alla fine)

   read from:
      g >> d; (==cin >> d) (g dal file), tutto questo e' uguale a scrivere ios :: in
   write to:
      g << d;
      g << "hello"
      = a ios :: out
 3.7) funzioni di controllo
      int a = 10;
      if ("condizione di controllo"), quindi if (a==10) {
       cout << "si, e uguale a 10" ; 
      } (se il controllo non da esito positivo, semplicemente cosi si salta il programma, e continua a controllare piu avanti)    
     opp per piu variabili
     int a,b;
     if(a==10 && b<5) {
      comando1
     } else {
      comando2
     } (questo per non mandare avanti alla compilazione)
   esempio:
      #include <iostream>
      using namespace std; 
      int main () {
         fstream g;
         g.open (file.dot, ios :: in);
         if (g.good()==false) {
            cout <<"bad file";
            return -1; (non fa return 0 perche il file non e andato a buon fine, serve per non far andare avanti il programma)

         } 
         return 0;
      }  

    
 
