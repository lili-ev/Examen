# Examen

Exercice 1 : Passage par valeur et par référence

1. Résultat affiché
15 20

2. Différence entre passage par valeur et par référence: 
Par valeur : la fonction reçoit une copie de la variable. Modifier le paramètre ne change pas la variable d'origine.
Par référence : la fonction reçoit un alias de la variable d'origine. Modifier le paramètre modifie la variable d'origine.

3. Fonction modifiée:
void modifier(int &a, int &b) {
    a += 5;
    b += 10;
}

Le programme affiche alors 15 30.

4. Rôle de l'opérateur &:
Dans la déclaration d'un paramètre, & crée une référence : le paramètre devient un autre nom pour la variable passée en argument. Aucune copie n'est faite, donc la fonction modifie directement la variable d'origine.

Exercice 2 : Classes et encapsulation

1.
class CompteBancaire {
private:
    int numero;
    string titulaire;
    double solde;

public:

};

2.
CompteBancaire(int num, string tit, double s) {
    numero = num;
    titulaire = tit;
    solde = s;
}

3.
void deposer(double montant) {
    if (montant > 0)
        solde += montant;
}

void retirer(double montant) {
    if (montant > 0 && solde >= montant)
        solde -= montant;
    else
        cout << "Retrait impossible" << endl;
}

void afficher() {
    cout << "Compte n°" << numero
         << " | Titulaire : " << titulaire
         << " | Solde : " << solde << endl;
}

4.
int main() {
    CompteBancaire c1(1, "Ali", 1000);
    CompteBancaire c2(2, "Sara", 500);

    c1.deposer(300);
    c2.retirer(200);

    c1.afficher();
    c2.afficher();
    return 0;
}

<img width="447" height="55" alt="image" src="https://github.com/user-attachments/assets/2ce9488e-d175-4c81-a326-d8f7d0303334" />


Exercice 3 : Héritage et polymorphisme

1.
class Vehicule {
protected:
    string immatriculation;
    string marque;
    double vitesseMax;
  
};      

2.
public:
    Vehicule(string im, string ma, double v) {
        immatriculation = im;
        marque = ma;
        vitesseMax = v;
    }

3. 
class Voiture : public Vehicule {
private:
    int nombrePortes;
    string typeCarburant;

public:
    Voiture(string im, string ma, double v, int np, string tc)
        : Vehicule(im, ma, v) {
        nombrePortes = np;
        typeCarburant = tc;
    }
};

class Camion : public Vehicule {
private:
    double capaciteCharge;
    int nombreEssieux;

public:
    Camion(string im, string ma, double v, double cc, int ne)
        : Vehicule(im, ma, v) {
        capaciteCharge = cc;
        nombreEssieux = ne;
    }
}; 

4. 
Dans virtual :
virtual void afficherDetails() {
    cout << "Immatriculation : " << immatriculation
         << " | Marque : " << marque
         << " | Vitesse max : " << vitesseMax << endl;
}

Dans Voiture :
void afficherDetails() override {
    Vehicule::afficherDetails();
    cout << "Portes : " << nombrePortes
         << " | Carburant : " << typeCarburant << endl;
}

Dans Camion :
void afficherDetails() override {
    Vehicule::afficherDetails();
    cout << "Charge : " << capaciteCharge
         << " | Essieux : " << nombreEssieux << endl;
}

5.
int main() {
    Vehicule* tab[2];
    tab[0] = new Voiture("A-123-B", "Toyota", 180, 5, "Diesel");
    tab[1] = new Camion("C-456-D", "Volvo", 110, 20.5, 3);

    for (int i = 0; i < 2; i++)
        tab[i]->afficherDetails();   // polymorphisme

    for (int i = 0; i < 2; i++)
        delete tab[i];

    return 0;
}

<img width="442" height="65" alt="image" src="https://github.com/user-attachments/assets/509cf1fa-ebfc-4e54-8a22-9e3019474af4" />

6.
virtual ~Vehicule() {}
Sans virtual : delete sur un Vehicule* n’appelle que le destructeur de Vehicule. La partie dérivée n’est pas détruite correctement (comportement indéfini, fuite mémoire).
Avec virtual : le destructeur de la classe dérivée est appelé d’abord, puis celui de la mère. L’objet est entièrement détruit.

 
