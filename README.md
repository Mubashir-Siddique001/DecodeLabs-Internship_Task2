#include <iostream>
#include <fstream>
#include <string>

using namespace std;

void registerUser()
{
    string username, password;
    string user, pass;

    cout << "Enter username: ";
    cin >> username;

    cout << "Enter password: ";
    cin >> password;

    if (username == "" || password == "")
    {
        cout << "Username and password cannot be empty.\n";
        return;
    }

    if (password.length() < 6)
    {
        cout << "Password must be at least 6 characters long.\n";
        return;
    }

    ifstream file("users.txt");

    while (file >> user >> pass)
    {
        if (user == username)
        {
            cout << "Username already exists.\n";
            file.close();
            return;
        }
    }

    file.close();

    ofstream outFile("users.txt", ios::app);
    outFile << username << " " << password << endl;
    outFile.close();

    cout << "Registration successful!\n";
}

void loginUser()
{
    string username, password;
    string user, pass;

    cout << "Enter username: ";
    cin >> username;

    cout << "Enter password: ";
    cin >> password;

    ifstream file("users.txt");

    while (file >> user >> pass)
    {
        if (user == username)
        {
            if (pass == password)
            {
                cout << "Login successful! Welcome " << username << "!\n";
            }
            else
            {
                cout << "Incorrect password.\n";
            }

            file.close();
            return;
        }
    }

    file.close();
    cout << "Username not found.\n";
}

int main()
{
    int choice;

    while (true)
    {
        cout << "\n1. Register\n";
        cout << "2. Login\n";
        cout << "3. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        if (choice == 1)
        {
            registerUser();
        }
        else if (choice == 2)
        {
            loginUser();
        }
        else if (choice == 3)
        {
            cout << "Program ended.\n";
            break;
        }
        else
        {
            cout << "Invalid choice.\n";
        }
    }

    return 0;
}
