#include <iostream>
#include <time.h>
#include <iomanip>
#define path "mydb.dat"
#define mod "wb+"
#define mod1 "rb+"
#define size 250
#pragma warning(disable:4996)
using namespace std;

struct elevi // structura de tip elevi
{
	int ID;
	char nume[30];
	char prenume[30];
	int an_nast;
	char genul[30];
};

FILE* f_stream; // declararea pointerului fisier

void afis(); // functia de afisare a tabelei cu elevi

void adaugare(elevi a[], int bb); // functia de adaugare a elevilor noi in tabela

void update(elevi a[], int bb); // functia de update a tabelei

void modify(elevi a[], int id); // functia de modificare a unui elev dupa id

void append(elevi a[], int bb); // functia de adaugare a elevilor in tabela

int verifica(int a); // functia de verificare a ceia ce introduce utilizatorul in cin

void main()
{

	char cc[50];
	int i, j, optiunea, recorduri, update1 = 0, id_ul;
	int alegere = 0;

	elevi bb[50]; // structura de tip elevi

	f_stream = fopen(path, mod1); // deschidere stream

	if (f_stream == NULL) // daca streamul nu se deschide da eroare
	{

		cout << "|---------------------|\n";
		cout << "| ERROR 404 NOT FOUND |\n";
		cout << "|---------------------|\n\n";
		f_stream = fopen(path, mod); // deschidere stream
		fclose(f_stream); // inchidere stream

	}

	else
	{
		do // prima executare a ceia ce este mai jos
		{

			cout << "|----------------|\n";
			cout << "| Upload complet |\n";
			cout << "|----------------|\n\n";

			cout << "|----------------------------|\n";
			cout << "| Avem urmatoarele optiuni:  |\n";
			cout << "| 1. Afisare                 |\n";
			cout << "| 2. Inscriere recorduri noi |\n";
			cout << "| 3. Modificare recorduri    |\n";
			cout << "| 4. Adaugare recorduri      |\n";
			cout << "| 5. Iesire din program      |\n";
			cout << "|----------------------------|\n\n";

			cout << "|------------------|\n";
			cout << "| Optiunea aleasa: ";
			cin >> alegere;
			alegere = verifica(alegere); // verificarea daca utilizatorul a introdus cea ce se cere
			cout << "|------------------|\n\n";

			switch (alegere) // verificarea numarului introdus de utilizator si executarea lui dupa case-urile de mai jos
			{

			case 1:

				afis(); // afisarea tabelei
				break;

			case 2:

				cout << "Cate recorduri doriti? ";
				cin >> recorduri;
				recorduri = verifica(recorduri); // verificarea daca utilizatorul a introdus cea ce se cere
				if ((recorduri > 0) && (recorduri <= 50)) //  daca recorduri sunt mai multe de 0 si mai putine sau egale cu 50 se va executa din if
				{

					adaugare(bb, recorduri); // executarea functie de adaugare a elevilor
					cout << "\nDoriti sa faceti update sau nu?\nPentru da apasati 1\nPentru nu apasati 2\n\nOptiunea: ";
					cin >> update1;
					update1 = verifica(update1); // verificarea daca utilizatorul a introdus cea ce se cere

					if (update1 == 1) // daca a introdus 1 dupa cum se cere se va face update
					{

						update(bb, 50); // functia pentru a face update la cea ce a introdus utilizatorul in tabel
						cout << endl;
						cout << "|---------------------------------|\n";
						cout << "| 1.      Update sa facut!!!      |\n";
						cout << "|---------------------------------|\n\n";
						cout << endl;
						cout << "|--------------------------------------|\n";
						cout << "| Apasa orice tasta pentru a continua: ";
						cin >> cc;
						cout << "|--------------------------------------|\n\n";

					}
					else // daca a introdus alta cifre nu se va face update
					{

						cout << endl;
						cout << "|------------------------------------|\n";
						cout << "| 1.      Update nu sa facut!!!      |\n";
						cout << "|------------------------------------|\n\n";
						cout << endl;
						cout << "|--------------------------------------|\n";
						cout << "| Apasa orice tasta pentru a continua: ";
						cin >> cc;
						cout << "|--------------------------------------|\n\n";

					}
				}
				else // daca numarul numarul de recorduri este 0 sau mai mare ca 50 se va executa totul de mai jos
				{

					cout << endl;
					cout << "|------------------------------------------------|\n";
					cout << "| 1. Nu poti seta mai mult de 50 de inregistrari |\n";
					cout << "| 2. Introdu un numar de la 1 la 50 fara litere  |\n";
					cout << "|------------------------------------------------|\n\n";
					cout << endl;
					cout << "|--------------------------------------|\n";
					cout << "| Apasa orice tasta pentru a continua: ";
					cin >> cc;
					cout << "|--------------------------------------|\n\n";

				}
				break;


			case 3:

				cout << "Introduce-ti ID-ul: ";
				cin >> id_ul;
				cout << endl;
				id_ul = verifica(id_ul); // verificarea daca utilizatorul a introdus cea ce se cere

				if ((id_ul > 0) && (id_ul <= 50)) //  daca id_ul este mai mare ca 0 si mai mic ca 50 se va executa totul din if
				{

					modify(bb, id_ul); // functia de modificare a elevului cu id_ul ales
					cout << "\nDoriti sa faceti update sau nu?\nPentru da apasati 1\nPentru nu apasati 2\n\nOptiunea: ";
					cin >> update1;
					update1 = verifica(update1); // verificarea daca utilizatorul a introdus cea ce se cere

					if (update1 == 1) // daca a introdus 1 dupa cum se cere se va face update
					{

						update(bb, 50); // functia pentru a face update la cea ce a introdus utilizatorul in tabel
						cout << endl;
						cout << "|---------------------------------|\n";
						cout << "| 1.      Update sa facut!!!      |\n";
						cout << "|---------------------------------|\n\n";
						cout << endl;
						cout << "|--------------------------------------|\n";
						cout << "| Apasa orice tasta pentru a continua: ";
						cin >> cc;
						cout << "|--------------------------------------|\n\n";

					}
					else // daca a introdus alta cifre nu se va face update
					{

						cout << endl;
						cout << "|------------------------------------|\n";
						cout << "| 1.      Update nu sa facut!!!      |\n";
						cout << "|------------------------------------|\n\n";
						cout << endl;
						cout << "|--------------------------------------|\n";
						cout << "| Apasa orice tasta pentru a continua: ";
						cin >> cc;
						cout << "|--------------------------------------|\n\n";

					}
				}
				else // daca numarul id_ul este 0 sau mai mare ca 50 se va executa totul de mai jos
				{

					cout << endl;
					cout << "|--------------------------------------|\n";
					cout << "| 1. Verifica cate inregistrari sunt   |\n";
					cout << "|               EROARE                 |\n";
					cout << "|--------------------------------------|\n\n";
					cout << endl;
					cout << "|--------------------------------------|\n";
					cout << "| Apasa orice tasta pentru a continua: ";
					cin >> cc;
					cout << "|--------------------------------------|\n\n";

				}
				break;

			case 4:

				cout << "Cate recorduri doriti? ";
				cin >> recorduri;
				recorduri = verifica(recorduri); // verificarea daca utilizatorul a introdus cea ce se cere

				if ((recorduri > 0) && (recorduri <= 50)) //  daca recorduri sunt mai multe de 0 si mai putine sau egale cu 50 se va executa din if
				{

					append(bb, recorduri); // executarea functie de adaugare a elevilor
					cout << "\nDoriti sa faceti update sau nu?\nPentru da apasati 1\nPentru nu apasati 2\n\nOptiunea: ";
					cin >> update1;
					update1 = verifica(update1); // verificarea daca utilizatorul a introdus cea ce se cere

					if (update1 == 1) // daca a introdus 1 dupa cum se cere se va face update
					{

						update(bb, 50); // functia pentru a face update la cea ce a introdus utilizatorul in tabel
						cout << endl;
						cout << "|---------------------------------|\n";
						cout << "| 1.      Update sa facut!!!      |\n";
						cout << "|---------------------------------|\n\n";
						cout << endl;
						cout << "|--------------------------------------|\n";
						cout << "| Apasa orice tasta pentru a continua: ";
						cin >> cc;
						cout << "|--------------------------------------|\n\n";

					}
					else // daca a introdus alta cifre nu se va face update
					{

						cout << endl;
						cout << "|------------------------------------|\n";
						cout << "| 1.      Update nu sa facut!!!      |\n";
						cout << "|------------------------------------|\n\n";
						cout << endl;
						cout << "|--------------------------------------|\n";
						cout << "| Apasa orice tasta pentru a continua: ";
						cin >> cc;
						cout << "|--------------------------------------|\n\n";

					}
				}
				else // daca numarul numarul de recorduri este 0 sau mai mare ca 50 se va executa totul de mai jos
				{

					cout << endl;
					cout << "|------------------------------------------------|\n";
					cout << "| 1. Nu poti seta mai mult de 50 de inregistrari |\n";
					cout << "| 2. Introdu un numar de la 1 la 50 fara litere  |\n";
					cout << "|------------------------------------------------|\n\n";
					cout << endl;
					cout << "|--------------------------------------|\n";
					cout << "| Apasa orice tasta pentru a continua: ";
					cin >> cc;
					cout << "|--------------------------------------|\n\n";

				}
				break;

			case 5:

				cout << "|-----------------------------------------|\n";
				cout << "| O zi placuta in continuare, la revedere |\n";
				cout << "|-----------------------------------------|\n\n";
				break;

			default:

				cout << "|------------------------------------------------------------------------|\n";
				cout << "| Aceasta optiune nu exista, va rugam sa alegeti din optiunile existente |\n";
				cout << "|------------------------------------------------------------------------|\n\n";
				cout << endl;
				cout << "|--------------------------------------|\n";
				cout << "| Apasa orice tasta pentru a continua: ";
				cin >> cc;
				cout << "|--------------------------------------|\n\n";
				break;

			}
			fclose(f_stream); // inchidere stream
		} while (alegere != 5); // reintoarcere la meniu atata timp cat alegerea e diferita de case 5 case-ul de esire
	}
}

void afis() // functia de afisare a tabelei cu elevi
{
	elevi a[50];
	char cc[50];
	f_stream = fopen(path, mod1); // deschidere stream
	fread(a, sizeof(elevi), 50, f_stream); // citire stream

	cout << endl;
	cout << " |------------------------------------------------------------|\n";
	cout << " | ID   | Numele   | Prenumele   | Anul nasterii   | Genul    |" << endl;
	for (int i = 0; i < 50; i++)
	{
		if (a[i].ID != -858993460 && (a[i].ID < 50))
		{
			cout << setw(6) << a[i].ID << " ";
			cout << setw(10) << a[i].nume << " ";
			cout << setw(13) << a[i].prenume << " ";
			cout << setw(17) << a[i].an_nast << " ";
			cout << setw(10) << a[i].genul << endl << " ";
			cout << "|------------------------------------------------------------|" << endl;
		}
	}
	cout << endl;
	cout << endl;
	cout << "|--------------------------------------|\n";
	cout << "| Apasa orice tasta pentru a continua: ";
	cin >> cc;
	cout << "|--------------------------------------|\n\n";
	fclose(f_stream); // inchidere stream
}
void adaugare(elevi a[], int bb) // functia de adaugare elevi in tabel
{
	for (int i = 0; i < bb; i++)
	{
		a[i].ID = i + 1;
		cout << endl;
		cout << "Introdu numele elevului: ";
		cin >> a[i].nume;
		cout << "Introdu prenumele elevului: ";
		cin >> a[i].prenume;
		cout << "Introdu anul nasterii: ";
		cin >> a[i].an_nast;
		a[i].an_nast = verifica(a[i].an_nast);
		cout << "Introdu genul: ";
		cin >> a[i].genul;
	}
	fclose(f_stream); // inchidere stream
}
void update(elevi a[], int bb) // functia de a face update la tabel
{
	f_stream = fopen(path, mod1); // deschidere stream
	fwrite(a, sizeof(elevi), bb, f_stream); // inscriere in stream

}
void modify(elevi a[], int id) // functia de modificare a elevilor dupa id
{
	int alegere;
	char cc[50];
	f_stream = fopen(path, mod1); // deschidere stream
	fread(a, sizeof(elevi), 50, f_stream); // citire stream

	cout << "|--------------------------------------|\n";
	cout << "Ce vrei sa modifici?\n\n";
	cout << "1.Numele \n2.Prenumele \n3.Anul nasterii \n4.Genul \n5.Tot \n6.Nimic\n\n";
	cout << "|--------------------------------------|\n\n";
	cout << "Alegerea: ";
	cin >> alegere;
	alegere = verifica(alegere); // verificarea daca utilizatorul a introdus cea ce se cere
	switch (alegere)
	{
	case 1:
		a[id - 1].ID = id;
		cout << "Introdu numele elevului: ";
		cin >> a[id - 1].nume;
		break;

	case 2:
		a[id - 1].ID = id;
		cout << "Introdu prenumele elevului: ";
		cin >> a[id - 1].prenume;
		break;

	case 3:
		a[id - 1].ID = id;
		cout << "Introdu anul nasterii: ";
		cin >> a[id - 1].an_nast;
		a[id - 1].an_nast = verifica(a[id - 1].an_nast);
		break;

	case 4:
		a[id - 1].ID = id;
		cout << "Introdu genul: ";
		cin >> a[id - 1].genul;
		break;

	case 5:
		a[id - 1].ID = id;
		cout << "Introdu numele elevului: ";
		cin >> a[id - 1].nume;
		cout << "Introdu prenumele elevului: ";
		cin >> a[id - 1].prenume;
		cout << "Introdu anul nasterii: ";
		cin >> a[id - 1].an_nast;
		a[id - 1].an_nast = verifica(a[id - 1].an_nast);
		cout << "Introdu genul: ";
		cin >> a[id - 1].genul;
		break;

	case 6:
		cout << endl;
		cout << "|------------------------------------------------------------------|\n";
		cout << "|                 Ati ales optiunea Nimic                          |\n";
		cout << "|          Apasa orice tasta pentru a continua: ";
		cin >> cc;
		cout << "|------------------------------------------------------------------|\n\n";
		break;

	default:
		cout << endl;
		cout << "|-----------------------------------------------------------------------------------|\n";
		cout << "|      1. Aceasta optiune nu exista, va rugam sa alegeti din optiunile existente    |\n";
		cout << "|      2. Nu poti introduce caractere sau simboluri la alegere                      |\n";
		cout << "|          Apasa orice tasta pentru a continua: ";
		cin >> cc;
		cout << "|-----------------------------------------------------------------------------------|\n\n";
		break;
	}
	fclose(f_stream);
}
void append(elevi a[], int bb) // functia de adaugare a elevilor in tabel
{
	f_stream = fopen(path, mod1); // deschidere stream
	fread(a, sizeof(elevi), 50, f_stream); // citire stream
	int contor = 0;

	for (int i = 0; i < 50; i++)
	{
		if (a[i].ID != -858993460)
		{
			contor++;
		}
	}
	fclose(f_stream); // inchidere stream
	for (int i = contor; i < contor + bb; i++)
	{
		a[i].ID = i + 1;
		cout << endl;
		cout << "Introdu numele elevului: ";
		cin >> a[i].nume;
		cout << "Introdu prenumele elevului: ";
		cin >> a[i].prenume;
		cout << "Introdu anul nasterii: ";
		cin >> a[i].an_nast;
		a[i].an_nast = verifica(a[i].an_nast);
		cout << "Introdu genul: ";
		cin >> a[i].genul;
	}
	f_stream = fopen(path, mod1); // deschidere stream
	fwrite(a, sizeof(elevi), 1, f_stream); // inscriere stream
	fclose(f_stream); // inchidere stream
}
int verifica(int a)
{
	while (1)
	{
		int a;
		if (cin.fail()) // verifica daca este vreo greseala
		{
			cin.clear(); // stream clear
			cin.ignore(INT_MAX, '\n'); // ignorarea input buffer
		}
		if (!cin.fail()) // daca este totul ok se face esire din while
			break;
	}
	return a; // return a
}
