#include <iostream>
#include <string>
using namespace std;

// Node for binary search tree
struct Node {
    string name;
    int quantity;
    Node* left;
    Node* right;
    Node(string name, int quantity) {
        this->name = name;
        this->quantity = quantity;
        this->left = NULL;
        this->right = NULL;
    }
};

// Binary search tree class
class Inventory {
private:
    Node* root;
    void insert(Node* node, string name, int quantity) {
        if (name < node->name) {
            if (node->left == NULL) {
                node->left = new Node(name, quantity);
            }
            else {
                insert(node->left, name, quantity);
            }
        }
        else {
            if (node->right == NULL) {
                node->right = new Node(name, quantity);
            }
            else {
                insert(node->right, name, quantity);
            }
        }
    }
    void print(Node* node) {
        if (node != NULL) {
            print(node->left);
            cout << node->name << ": " << node->quantity << endl;
            print(node->right);
        }
    }
    Node* search(Node* node, string name) {
        if (node == NULL || node->name == name) {
            return node;
        }
        else if (name < node->name) {
            return search(node->left, name);
        }
        else {
            return search(node->right, name);
        }
    }
public:
    Inventory() {
        root = NULL;
    }
    void insert(string name, int quantity) {
        if (root == NULL) {
            root = new Node(name, quantity);
        }
        else {
            insert(root, name, quantity);
        }
    }
    void print() {
        print(root);
    }
    Node* search(string name) {
        return search(root, name);
    }
};

int main() {
    Inventory inventory;

    
        inventory.insert("apple", 50);
    inventory.insert("Bananas", 20);
    inventory.insert("Oranges", 30);
    inventory.insert("Cola", 36);
    inventory.insert("Chips", 30);
    inventory.insert("Pepsi", 39);
    inventory.insert("Gum", 60);
    inventory.insert("Bread", 0);
    inventory.insert("lighter", 64);
    inventory.insert("lemon", 15);
    inventory.insert("Carrot", 2);
    inventory.insert("Water", 41);
    inventory.insert("Coffee", 80);
    inventory.insert("Tea", 5);
    inventory.insert("Mint", 77);

    inventory.print();

    string searchItem;
    cout << "Enter an item to search for: ";
    cin >> searchItem;

    Node* node = inventory.search(searchItem);
    if (node != NULL) {
        cout << "Found " << node->quantity << " " << node->name << endl;
    }
    else {
        cout << "Item not found" << endl;
    }

    return 0;
}
