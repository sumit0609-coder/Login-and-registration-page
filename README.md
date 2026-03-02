#include <iostream>
#include <fstream>
#include <string>
using namespace std;


bool usernameExists(string username) {
    ifstream file("users.txt");   
    string u, p;
    
    while (file >> u >> p) {
        if (u == username) {
            return true;         
        }
    }
    return false;                 // Username not found
}
void registerUser() {
    string username, password;

    cout << "Enter Username: ";
    cin >> username;
    if (usernameExists(username)) {
        cout << "Username already exists!\n";
        return;   
    }
    cout << "Enter Password: ";
    cin >> password;
    ofstream file("users.txt", ios::app);
    file << username << " " << password << endl;

    cout << "Registration Successful!\n";
}
void loginUser() {
    string username, password;
    string u, p;

    cout << "Enter Username: ";
    cin >> username;

    cout << "Enter Password: ";
    cin >> password;

    ifstream file("users.txt");   
    
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
