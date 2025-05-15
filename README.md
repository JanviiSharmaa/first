#include <iostream>
#include <fstream>
#include <string>

using namespace std;

// Function to write (overwrite) data to file
void writeToFile(const string& filename) {
    ofstream outfile(filename);  // Overwrites existing content
    if (!outfile) {
        cerr << "Error opening file for writing.\n";
        return;
    }

    string data;
    cout << "Enter text to write to the file (type 'exit' to finish):\n";
    while (true) {
        getline(cin, data);
        if (data == "exit") break;
        outfile << data << endl;
    }

    outfile.close();
    cout << "Data written successfully.\n";
}

// Function to append data to file
void appendToFile(const string& filename) {
    ofstream outfile(filename, ios::app);  // Append mode
    if (!outfile) {
        cerr << "Error opening file for appending.\n";
        return;
    }

    string data;
    cout << "Enter text to append to the file (type 'exit' to finish):\n";
    while (true) {
        getline(cin, data);
        if (data == "exit") break;
        outfile << data << endl;
    }

    outfile.close();
    cout << "Data appended successfully.\n";
}

// Function to read data from file
void readFromFile(const string& filename) {
    ifstream infile(filename);
    if (!infile) {
        cerr << "Error opening file for reading.\n";
        return;
    }

    string line;
    cout << "\n--- File Content ---\n";
    while (getline(infile, line)) {
        cout << line << endl;
    }

    infile.close();
    cout << "--- End of File ---\n";
}

int main() {
    string filename;
    int choice;

    cout << "Enter filename (with .txt extension): ";
    getline(cin, filename);

    do {
        cout << "\nChoose an operation:\n";
        cout << "1. Write to file (overwrite)\n";
        cout << "2. Append to file\n";
        cout << "3. Read from file\n";
        cout << "4. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;
        cin.ignore();  // Ignore leftover newline

        switch (choice) {
            case 1:
                writeToFile(filename);
                break;
            case 2:
                appendToFile(filename);
                break;
            case 3:
                readFromFile(filename);
                break;
            case 4:
                cout << "Exiting...\n";
                break;
            default:
                cout << "Invalid choice. Try again.\n";
        }

    } while (choice != 4);

    return 0;
}
