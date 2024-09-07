# week8

#include <iostream>
using namespace std;

// Node structure
class Node {
public:
    int marks;
    string gender;
    Node* left;
    Node* right;

    Node(int marks, string gender) {
        this->marks = marks;
        this->gender = gender;
        this->left = nullptr;
        this->right = nullptr;
    }
};

// BST class
class BST {
public:
    Node* root;

    BST() {
        root = nullptr;
    }

    // Insert function
    void insert(int marks, string gender) {
        root = insertRec(root, marks, gender);
    }

    // Recursive insert helper
    Node* insertRec(Node* node, int marks, string gender) {
        if (node == nullptr) {
            return new Node(marks, gender);
        }
        if (marks < node->marks) {
            node->left = insertRec(node->left, marks, gender);
        } else {
            node->right = insertRec(node->right, marks, gender);
        }
        return node;
    }

    // In-order traversal
    void inOrderTraversal() {
        inOrderRec(root);
    }

    // Recursive in-order helper
    void inOrderRec(Node* node) {
        if (node != nullptr) {
            inOrderRec(node->left);
            cout << "Marks: " << node->marks << ", Gender: " << node->gender << endl;
            inOrderRec(node->right);
        }
    }
};

int main() {
    // Data from the provided table
    int marks[] = {10, 5, 14, 3, 7, 9, 18, 15, 13, 17, 100};
    string gender[] = {"Female", "Male", "Male", "Male", "Male", "Female", "Female", "Female", "Female", "Male", "Male"};

    // Two separate BSTs for male and female students
    BST maleBST, femaleBST;

    // Inserting data into respective BSTs
    for (int i = 0; i < 11; i++) {
        if (gender[i] == "Male") {
            maleBST.insert(marks[i], gender[i]);
        } else if (gender[i] == "Female") {
            femaleBST.insert(marks[i], gender[i]);
        }
    }

    // In-order traversal for Male BST
    cout << "In-order traversal for Male BST:\n";
    maleBST.inOrderTraversal();

    // In-order traversal for Female BST
    cout << "\nIn-order traversal for Female BST:\n";
    femaleBST.inOrderTraversal();

    return 0;
}
