# Guide Détaillé de la Programmation Orientée Objet (POO) en PHP

## 1. Objectifs de la POO (Goal of OOP)

### 1.1 Définition
La POO est un paradigme de programmation qui permet de modéliser des entités du monde réel sous forme d'objets dans le code. Chaque objet contient à la fois :
- Des données (propriétés/attributs)
- Des comportements (méthodes/fonctions)

### 1.2 Avantages
```php
// Sans POO
$nomUtilisateur = "bouanaya soufiane";
$emailUtilisateur = "bouanaya@example.com";
$ageUtilisateur = 26;

function verifierAge($age) {
    return $age >= 18;
}

// Avec POO
class Utilisateur {
    private $nom;
    private $email;
    private $age;

    public function verifierMajorite() {
        return $this->age >= 18;
    }
}
```

#### Bénéfices Principaux
1. **Réutilisabilité**
   - Les classes peuvent être réutilisées dans différents projets
   - Réduction de la duplication de code

2. **Scalabilité**
   - Facilité d'extension des fonctionnalités
   - Ajout de nouvelles fonctionnalités sans modifier le code existant

3. **Maintenabilité**
   - Code plus organisé et structuré
   - Plus facile à déboguer et à maintenir

## 2. Concepts Fondamentaux de la POO

### 2.1 Encapsulation
L'encapsulation consiste à regrouper les données et les méthodes qui les manipulent dans une classe et à contrôler l'accès à ces données.

```php
class CompteBancaire {
    private $solde = 0;  // Donnée encapsulée
    
    public function deposer($montant) {
        if ($montant > 0) {
            $this->solde += $montant;
            return true;
        }
        return false;
    }
    
    public function getSolde() {
        return $this->solde;
    }
}

$compte = new CompteBancaire();
$compte->deposer(100);  // Accès contrôlé au solde
echo $compte->getSolde();  // Lecture contrôlée du solde
```

### 2.2 Abstraction
L'abstraction permet de masquer la complexité en exposant uniquement les fonctionnalités nécessaires.

```php
abstract class Vehicule {
    protected $marque;
    protected $modele;
    
    abstract public function demarrer();
    abstract public function arreter();
    
    public function getInfos() {
        return "{$this->marque} {$this->modele}";
    }
}

class Voiture extends Vehicule {
    public function demarrer() {
        return "La voiture démarre le moteur";
    }
    
    public function arreter() {
        return "La voiture coupe le moteur";
    }
}
```

### 2.3 Héritage
L'héritage permet à une classe d'hériter des propriétés et méthodes d'une autre classe.

```php
class Animal {
    protected $nom;
    
    public function manger() {
        return "{$this->nom} mange";
    }
}

class Chat extends Animal {
    public function __construct($nom) {
        $this->nom = $nom;
    }
    
    public function miauler() {
        return "{$this->nom} fait miaou";
    }
}

$chat = new Chat("Felix");
echo $chat->manger();    // Hérité de Animal
echo $chat->miauler();   // Spécifique à Chat
```

### 2.4 Polymorphisme
Le polymorphisme permet à différentes classes d'implémenter la même interface de différentes manières.

```php
interface FormeGeometrique {
    public function calculerAire();
    public function calculerPerimetre();
}

class Cercle implements FormeGeometrique {
    private $rayon;
    
    public function calculerAire() {
        return pi() * pow($this->rayon, 2);
    }
    
    public function calculerPerimetre() {
        return 2 * pi() * $this->rayon;
    }
}

class Rectangle implements FormeGeometrique {
    private $longueur;
    private $largeur;
    
    public function calculerAire() {
        return $this->longueur * $this->largeur;
    }
    
    public function calculerPerimetre() {
        return 2 * ($this->longueur + $this->largeur);
    }
}
```

## 3. Classes et Objets en Détail

### 3.1 Propriétés et Méthodes

```php
class Employe {
    // Propriétés
    private $nom;
    private $salaire;
    private $departement;
    
    // Méthodes
    public function calculerSalaireAnnuel() {
        return $this->salaire * 12;
    }
    
    public function augmenterSalaire($pourcentage) {
        $this->salaire *= (1 + $pourcentage / 100);
    }
}
```

### 3.2 Constructeurs et Destructeurs

```php
class Fichier {
    private $handle;
    private $nomFichier;
    
    public function __construct($nomFichier) {
        $this->nomFichier = $nomFichier;
        $this->handle = fopen($nomFichier, 'r');
    }
    
    public function __destruct() {
        if ($this->handle) {
            fclose($this->handle);
        }
    }
}
```

### 3.3 Modificateurs d'Accès

```php
class Produit {
    private $prix;         // Accessible uniquement dans la classe
    protected $reference;  // Accessible dans la classe et les classes enfants
    public $nom;          // Accessible partout
    
    public function setPrix($prix) {
        if ($prix > 0) {
            $this->prix = $prix;
        }
    }
    
    public function getPrix() {
        return $this->prix;
    }
}
```

## 4. Méthodes et Propriétés Statiques

```php
class Mathematiques {
    public static $pi = 3.14159;
    private static $compteur = 0;
    
    public static function carre($nombre) {
        self::$compteur++;
        return $nombre * $nombre;
    }
    
    public static function getCompteur() {
        return self::$compteur;
    }
}

// Utilisation
echo Mathematiques::$pi;
echo Mathematiques::carre(4);
```

## 5. Espaces de Noms et Autoloading

```php
// fichier: src/Services/UserService.php
namespace App\Services;

class UserService {
    public function create($data) {
        // Logique de création
    }
}

// fichier: composer.json
{
    "autoload": {
        "psr-4": {
            "App\\": "src/"
        }
    }
}

// Utilisation
use App\Services\UserService;
$userService = new UserService();
```

