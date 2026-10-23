
#include <iostream>
using namespace std;

struct node {
    int data;
    node *left;
    node *right;

    node(int value) {
        data = value;
        left = nullptr;
        right = nullptr;
    }
};

node* root = nullptr;

node* insert(node *root, int value) {
    if (root == nullptr) {
        return new node(value);
    }
    else if (value < root->data) {
        root->left = insert(root->left, value);
    }
    else if (value > root->data) {
        root->right = insert(root->right, value);
    }
    else {
        cout << "Duplicates are not allowed" << endl;
    }

    return root;
}

void insertValue() {
    int value;

    cout << "Enter the value in the BST: ";

    if (!(cin >> value)) {
        cout << "Invalid Input" << endl;
        cin.clear();
        cin.ignore(10000, '\n');
        return;
    }

    root = insert(root, value);
}

void display(node *root) {
    if (root != nullptr) {
        display(root->left);
        cout << root->data << " ";
        display(root->right);
    }
}

int main() {
    int choice;

    do {
        cout << "\n============== BINARY SEARCH TREE ==============\n";
        cout << "1. INSERT\n";
        cout << "2. DISPLAY\n";
        cout << "3. EXIT\n";
        cout << "================================================\n";
        cout << "Enter your choice: ";

        if (!(cin >> choice)) {
            cout << "Invalid input!" << endl;
            cin.clear();
            cin.ignore(10000, '\n');
            continue;
        }

        switch (choice) {
            case 1:
                insertValue();
                break;

            case 2:
                if (root == nullptr) {
                    cout << "BST is empty!" << endl;
                }
                else {
                    cout << "Binary search tree elements: ";
                    display(root);
                    cout << endl;
                }
                break;

            case 3:
                cout << "Exiting..." << endl;
                break;

            default:
                cout << "Invalid choice!" << endl;
        }

    } while (choice != 3);

    return 0;
}
