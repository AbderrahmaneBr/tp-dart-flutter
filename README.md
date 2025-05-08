# Partie 1 - Syntaxe de base

```dart
// Partie 1: Structures de Données
class Book {
  String title;
  String author;
  int year;
  bool isAvailable;

  Book(this.title, this.author, this.year, this.isAvailable);

  Book.available(this.title, this.author, this.year) : isAvailable = true;
}

class Library {
  final List<Book> _books = [];

  void addBook(Book book) {
    _books.add(book);
  }

  void borrowBook(String title) {
    for (var book in _books) {
      if (book.title == title) {
        book.isAvailable = false;
        break;
      }
    }
  }

  // Retourne une liste des livres disponibles
  List<Book> getAvailableBooks() {
    return _books.where((book) => book.isAvailable).toList();
  }

  // Tous les livres
  List<Book> get allBooks => List.from(_books);

  // Surcharge de l'opérateur + pour fusionner deux bibliothèques
  Library operator +(Library other) {
    Library newLibrary = Library();

    // Ajouter les livres de la première bibliothèque
    for (var book in _books) {
      newLibrary.addBook(Book(book.title, book.author, book.year, book.isAvailable));
    }

    // Ajouter les livres de la deuxième bibliothèque
    for (var book in other._books) {
      newLibrary.addBook(Book(book.title, book.author, book.year, book.isAvailable));
    }

    return newLibrary;
  }
}

void displayBooks(List<Book> books) {
  for (var book in books) {
    print('Titre: ${book.title}, Auteur: ${book.author} (Année: ${book.year})');
  }
}

void main() {
  var book1 = Book.available('Le Petit Prince', 'Antoine de Saint-Exupéry', 1943);
  var book2 = Book.available('1984', 'George Orwell', 1949);
  var book3 = Book('L\'Étranger', 'Albert Camus', 1942, false);

  // Initialisation d'une bibliothèque et ajout des livres
  var library1 = Library();
  library1.addBook(book1);
  library1.addBook(book2);
  library1.addBook(book3);

  print('Tous les livres:');
  displayBooks(library1.allBooks);

  // Emprunt d'un livre
  library1.borrowBook('Le Petit Prince');

  print('\nLivres disponibles après emprunt:');
  displayBooks(library1.getAvailableBooks());

  // Création d'une deuxième bibliothèque
  var library2 = Library();
  library2.addBook(Book.available('Dune', 'Frank Herbert', 1965));
  library2.addBook(Book.available('Fondation', 'Isaac Asimov', 1951));

  // Fusion des deux bibliothèques
  var mergedLibrary = library1 + library2;

  print('\nLivres dans la bibliothèque fusionnée:');
  displayBooks(mergedLibrary.allBooks);
}
```

# Partie 2 - Programmation orientée objet

```dart
class Employe {
  String _nom;
  double _salaire;

  Employe({required String nom, required double salaire})
    : _nom = nom,
      _salaire = salaire;

  void afficherInfos() {
    print('Nom: $_nom, Salaire: $_salaire €');
  }
}

class Manager extends Employe {
  double _prime;

  Manager({required String nom, required double salaire, required double prime})
    : _prime = prime,
      super(nom: nom, salaire: salaire);

  @override
  void afficherInfos() {
    print('Nom: $_nom, Salaire: $_salaire €, Prime: $_prime €');
  }
}

void main() {
  // Création d'un employé et d'un manager
  var employe = Employe(nom: 'Jean Dupont', salaire: 35000);
  var manager = Manager(nom: 'Marie Martin', salaire: 50000, prime: 10000);

  // Stockage dans une liste de type List<Employe>
  List<Employe> personnel = [employe, manager];

  // Parcours de la liste et appel de afficherInfos() pour chaque élément
  print('Informations du personnel:');
  for (var personne in personnel) {
    personne.afficherInfos();  // Comportement polymorphe
  }
}
```

# Partie 3 - Programmation asynchrone

```dart
// Simulation d'une requête API
Future<String> fetchData() {
  return Future.delayed(Duration(seconds: 2), () => "Données reçues");
}

void main() async {
  print("Loading...");

  // Utilisation de async/await pour attendre la réponse
  String result = await fetchData();

  print(result);
}
```
