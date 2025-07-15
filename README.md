#include <stdio.h>
#include <stdlib.h>

// Definition of a singly linked list node
typedef struct Node {
    int data;
    struct Node* next;
} Node;

// Function to create a new node
Node* newNode(int value) {
    Node* temp = (Node*)malloc(sizeof(Node));
    temp->data = value;
    temp->next = NULL;
    return temp;
}

// Function to remove duplicates from a sorted linked list
Node* removeDuplicates(Node* head) {
    Node* current = head;
    while (current && current->next) {
        if (current->data == current->next->data) {
            Node* dup = current->next;
            current->next = dup->next;
            free(dup);
        } else {
            current = current->next;
        }
    }
    return head;
}

// Function to print the linked list
void printList(Node* head) {
    Node* temp = head;
    while (temp) {
        printf("%d", temp->data);
        if (temp->next) printf(" ");
        temp = temp->next;
    }
    printf("\n");
}

// Function to free the memory
void freeList(Node* head) {
    Node* temp;
    while (head) {
        temp = head;
        head = head->next;
        free(temp);
    }
}

int main() {
    int n;
    scanf("%d", &n);

    if (n <= 0) {
        printf("\n");
        return 0;
    }

    Node* head = NULL;
    Node* tail = NULL;

    for (int i = 0; i < n; ++i) {
        int val;
        scanf("%d", &val);
        Node* new_node = newNode(val);
        if (head == NULL) {
            head = new_node;
            tail = new_node;
        } else {
            tail->next = new_node;
            tail = new_node;
        }
    }

    head = removeDuplicates(head);
    printList(head);
    freeList(head);

    return 0;
}
