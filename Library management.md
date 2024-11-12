#include <iostream>
#include <vector>
#include <string>

using namespace std;

struct Book {
    string title;
    string author;
    string ISBN;
    bool isAvailable;
};

struct Borrower {
    string name;
    string phoneNumber;
};

vector<Book> books;
vector<Borrower> borrowers;

void addBook() {
    Book newBook;
    cout << "Enter book title: ";
    cin >> newBook.title;
    cout << "Enter book author: ";
    cin >> newBook.author;
    cout << "Enter book ISBN: ";
    cin >> newBook.ISBN;
    newBook.isAvailable = true;
    books.push_back(newBook);
}

void searchBook() {
    string query;
    cout << "Enter book title, author, or ISBN: ";
    cin >> query;

    for (const auto &book : books) {
        if (book.title.find(query) != string::npos ||
            book.author.find(query) != string::npos ||
            book.ISBN.find(query) != string::npos) {
            cout << "Book found!" << endl;
            cout << "Title: " << book.title << endl;
            cout << "Author: " << book.author << endl;
            cout << "ISBN: " << book.ISBN << endl;
            cout << "Availability: " << (book.isAvailable ? "Yes" : "No") << endl;
            return;
        }
    }

    cout << "Book not found!" << endl;
}

void checkOutBook() {
    string ISBN;
    cout << "Enter book ISBN: ";
    cin >> ISBN;

    for (auto &book : books) {
        if (book.ISBN == ISBN) {
            if (book.isAvailable) {
                book.isAvailable = false;
                cout << "Book checked out successfully!" << endl;
                return;
            } else {
                cout << "Book is not available!" << endl;
                return;
            }
        }
    }

    cout << "Book not found!" << endl;
}

void returnBook() {
    string ISBN;
    cout << "Enter book ISBN: ";
    cin >> ISBN;

    for (auto &book : books) {
        if (book.ISBN == ISBN) {
            if (!book.isAvailable) {
                book.isAvailable = true;
                cout << "Book returned successfully!" << endl;
                return;
            } else {
                cout << "Book is already available!" << endl;
                return;
            }
        }
    }

    cout << "Book not found!" << endl;
}

void calculateFine() {
    string ISBN;
    cout << "Enter book ISBN: ";
    cin >> ISBN;

    for (const auto &book : books) {
        if (book.ISBN == ISBN) {
            if (!book.isAvailable) {
                cout << "Fine: $5" << endl; // Simplified fine calculation
                return;
            } else {
                cout << "Book is available!" << endl;
                return;
            }
        }
    }

    cout << "Book not found!" << endl;
}

int main() {
    while (true) {
        cout << "\nLibrary Management System" << endl;
        cout << "1. Add Book" << endl;
        cout << "2. Search Book" << endl;
        cout << "3. Check Out Book" << endl;
        cout << "4. Return Book" << endl;
        cout << "5. Calculate Fine" << endl;
        cout << "6. Exit" << endl;
        cout << "Choose an option: ";

        int option;
        cin >> option;

        switch (option) {
            case 1:
                addBook();
                break;
            case 2:
                searchBook();
                break;
            case 3:
                checkOutBook();
                break;
            case 4:
                returnBook();
                break;
            case 5:
                calculateFine();
                break;
            case 6:
                return 0;
            default:
                cout << "Invalid option. Please choose again." << endl;
        }
    }

    return 0;
}
