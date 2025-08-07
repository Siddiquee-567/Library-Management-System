# Library-Management-System
Here's a simple Library Management System implemented using Object-Oriented Programming (OOP) in Java. This is a console-based application with three main classes:

import java.util.ArrayList;
import java.util.Scanner;

// Book class
class Book {
    private int id;
    private String title;
    private boolean isAvailable;

    public Book(int id, String title) {
        this.id = id;
        this.title = title;
        this.isAvailable = true;
    }

    public int getId() {
        return id;
    }

    public String getTitle() {
        return title;
    }

    public boolean isAvailable() {
        return isAvailable;
    }

    public void issueBook() {
        isAvailable = false;
    }

    public void returnBook() {
        isAvailable = true;
    }

    public void displayInfo() {
        String status = isAvailable ? "Available" : "Issued";
        System.out.println("ID: " + id + ", Title: " + title + ", Status: " + status);
    }
}

// User class
class User {
    private String name;

    public User(String name) {
        this.name = name;
    }

    public void issueBook(Library library, int bookId) {
        library.issueBook(bookId);
    }

    public void returnBook(Library library, int bookId) {
        library.returnBook(bookId);
    }
}

// Library class
class Library {
    private ArrayList<Book> books = new ArrayList<>();

    public void addBook(Book book) {
        books.add(book);
    }

    public void viewBooks() {
        for (Book book : books) {
            book.displayInfo();
        }
    }

    public void issueBook(int id) {
        for (Book book : books) {
            if (book.getId() == id) {
                if (book.isAvailable()) {
                    book.issueBook();
                    System.out.println("Book issued successfully.");
                } else {
                    System.out.println("Book is already issued.");
                }
                return;
            }
        }
        System.out.println("Book not found.");
    }

    public void returnBook(int id) {
        for (Book book : books) {
            if (book.getId() == id) {
                if (!book.isAvailable()) {
                    book.returnBook();
                    System.out.println("Book returned successfully.");
                } else {
                    System.out.println("Book was not issued.");
                }
                return;
            }
        }
        System.out.println("Book not found.");
    }
}

// Main class
public class LibraryManagementSystem {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Library library = new Library();
        User user = new User("DefaultUser");

        // Adding some books initially
        library.addBook(new Book(1, "The Great Gatsby"));
        library.addBook(new Book(2, "1984"));
        library.addBook(new Book(3, "To Kill a Mockingbird"));

        int choice;
        do {
            System.out.println("\n--- Library Management System ---");
            System.out.println("1. View Books");
            System.out.println("2. Issue Book");
            System.out.println("3. Return Book");
            System.out.println("4. Exit");
            System.out.print("Enter your choice (1-4): ");
            choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    library.viewBooks();
                    break;
                case 2:
                    System.out.print("Enter book ID to issue: ");
                    int issueId = scanner.nextInt();
                    user.issueBook(library, issueId);
                    break;
                case 3:
                    System.out.print("Enter book ID to return: ");
                    int returnId = scanner.nextInt();
                    user.returnBook(library, returnId);
                    break;
                case 4:
                    System.out.println("Exiting system. Goodbye!");
                    break;
                default:
                    System.out.println("Invalid choice. Try again.");
            }

        } while (choice != 4);

        scanner.close();
    }
}
