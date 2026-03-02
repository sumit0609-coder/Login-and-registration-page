#include <iostream>
#include <fstream>
#include <string>
using namespace std;

// Function to check whether username already exists in file
bool usernameExists(string username) {
    ifstream file("users.txt");   // Open file in read mode
    string u, p;
      // Read username and password from file
    while (file >> u >> p) {
        if (u == username) {
            return true;          // Username found
        }
    }
    return false;                 // Username not found
}
// Function to register a new user
void registerUser() {
    string username, password;

    cout << "Enter Username: ";
    cin >> username;

    // Check if username already exists
    if (usernameExists(username)) {
        cout << "Username already exists!\n";
        return;   // Stop registration
    }
    cout << "Enter Password: ";
    cin >> password;

    // Open file in append mode to add new user
    ofstream file("users.txt", ios::app);
    file << username << " " << password << endl;

    cout << "Registration Successful!\n";
}

// Function to login an existing user
void loginUser() {
    string username, password;
    string u, p;

    cout << "Enter Username: ";
    cin >> username;

    cout << "Enter Password: ";
    cin >> password;

    ifstream file("users.txt");   // Open file in read mode
        // Check credentials
    while (file >> u >> p) {
        if (u == username && p == password) {
            cout << "Login Successful!\n";
            return;
        }
    }

    cout << "Invalid Username or Password!\n";
}

int main() {
    int choice;

    do {
        cout << "\n===== Login & Registration System =====\n";
        cout << "1. Register\n";
        cout << "2. Login\n";
        cout << "3. Exit\n";
        cout << "Enter choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                registerUser();
                break;
            case 2:
                loginUser();
                break;
            case 3:
                cout << "Exiting Program...\n";
                break;
            default:
                cout << "Invalid Choice! Try again.\n";
        }

    } while (choice != 3);

    return 0;
    
