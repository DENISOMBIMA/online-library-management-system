#include <iostream>
#include <vector>
using namespace std;
class Book {
private:
    int id;
    string title;
    string author;
    bool isBorrowed;

public:
    Book(int i, string t, string a) {
        id = i;
        title = t;
        author = a;
        isBorrowed = false;
    }

    int getId() {
        return id;
    }

    string getTitle() {
        return title;
    }

    string getAuthor() {
        return author;
    }

    bool getStatus() {
        return isBorrowed;
    }

    void borrowBook() {
        isBorrowed = true;
    }

    void returnBook() {
        isBorrowed = false;
    }
};

class User {
private:
    int userId;
    string name;

public:
    User(int id, string n) {
        userId = id;
        name = n;
    }

    int getUserId() {
        return userId;
    }

    string getName() {
        return name;
    }
};

class Library {
private:
    vector<Book> books;

public:
    void addBook(Book b) {
        books.push_back(b);
        cout << "Book added successfully.\n";
    }

    void removeBook(int id) {
        for (int i = 0; i < books.size(); i++) {
            if (books[i].getId() == id) {
                books.erase(books.begin() + i);
                cout << "Book removed successfully.\n";
                return;
            }
        }
        cout << "Book not found.\n";
    }

    void searchBook(string title) {
        for (Book b : books) {
            if (b.getTitle() == title) {
                cout << "Book Found: " << b.getTitle()
                     << " by " << b.getAuthor() << endl;
                return;
            }
        }
        cout << "Book not found.\n";
    }

    void borrowBook(int id) {
        for (Book &b : books) {
            if (b.getId() == id && !b.getStatus()) {
                b.borrowBook();
                cout << "Book borrowed successfully.\n";
                return;
            }
        }
        cout << "Book not available for borrowing.\n";
    }

    void returnBook(int id) {
        for (Book &b : books) {
            if (b.getId() == id && b.getStatus()) {
                b.returnBook();
                cout << "Book returned successfully.\n";
                return;
            }
        }
        cout << "Invalid return operation.\n";
    }
};

int main() {
    Library library;

    Book b1(1, "C++ Basics", "Bjarne Stroustrup");
    Book b2(2, "Object Oriented Programming", "Dennis Ritchie");

    // Test Case 1: Add books
    library.addBook(b1);
    library.addBook(b2);

    // Test Case 2: Search book (positive)
    library.searchBook("C++ Basics");

    // Test Case 3: Search book (negative)
    library.searchBook("Java Programming");

    // Test Case 4: Borrow book
    library.borrowBook(1);

    // Test Case 5: Borrow same book again (negative)
    library.borrowBook(1);

    // Test Case 6: Return book
    library.returnBook(1);

    // Test Case 7: Remove book
    library.removeBook(2);

    // Test Case 8: Remove non-existing book
    library.removeBook(5);

    return 0;
}



    
