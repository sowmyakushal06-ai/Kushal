1. Initialization if malloc into zero 
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main()
{
    int n, i;
    int *ptr;

    printf("Enter number of elements: ");
    scanf("%d", &n);

    
    ptr = (int *)malloc(n * sizeof(int));

    
    if (ptr == NULL)
    {
        printf("Memory allocation failed\n");
        return 1;
    }

    
    memset(ptr, 0, n * sizeof(int));

   
    printf("\nValues after initialization:\n");
    for (i = 0; i < n; i++)
    {
        printf("ptr[%d] = %d\n", i, ptr[i]);
    }

    printf("\nGetting MAC address:\n");
    system("getmac");

    
    free(ptr);

    return 0;
}

2.printing the address of the pointer 

#include <stdio.h>
#include <stdlib.h>

int main()
{
    int x = 10;
    int *ptr;

    
    ptr = &x;

    
    printf("Value of x = %d\n", x);

    
    printf("Address of x = %p\n", (void *)&x);

    printf("Address stored in ptr = %p\n", (void *)ptr);

    
    printf("Address of ptr = %p\n", (void *)&ptr);

    
    printf("\nGetting MAC address:\n");
    system("getmac");

    return 0;
}

3.selection sort with dynamic memory allocation 

#include <stdio.h>
#include <stdlib.h>

int main()
{
    int n, i, j, min, temp;
    int *arr;

    printf("Enter number of elements: ");
    scanf("%d", &n);

    
    arr = (int *)malloc(n * sizeof(int));

    
    if (arr == NULL)
    {
        printf("Memory allocation failed\n");
        return 1;
    }

    
    printf("Enter %d elements:\n", n);
    for (i = 0; i < n; i++)
    {
        scanf("%d", &arr[i]);
    }

    
    for (i = 0; i < n - 1; i++)
    {
        min = i;
        for (j = i + 1; j < n; j++)
        {
            if (arr[j] < arr[min])
            {
                min = j;
            }
        }

        
        if (min != i)
        {
            temp = arr[i];
            arr[i] = arr[min];
            arr[min] = temp;
        }
    }

    
    printf("\nSorted array:\n");
    for (i = 0; i < n; i++)
    {
        printf("%d ", arr[i]);
    }

    
    printf("\n\nGetting MAC address:\n");
    system("getmac");

    
    free(arr);

    return 0;
}

4.selection sort without dynamic memory allocation 

#include <stdio.h>
#include <stdlib.h>

int main()
{
    int n, i, j, min, temp;
    int arr[100];   

    printf("Enter number of elements: ");
    scanf("%d", &n);

    
    printf("Enter %d elements:\n", n);
    for (i = 0; i < n; i++)
    {
        scanf("%d", &arr[i]);
    }

    
    for (i = 0; i < n - 1; i++)
    {
        min = i;
        for (j = i + 1; j < n; j++)
        {
            if (arr[j] < arr[min])
            {
                min = j;
            }
        }

        
        if (min != i)
        {
            temp = arr[i];
            arr[i] = arr[min];
            arr[min] = temp;
        }
    }

    
    printf("\nSorted array:\n");
    for (i = 0; i < n; i++)
    {
        printf("%d ", arr[i]);
    }

    
    printf("\n\nGetting MAC address:\n");
    system("getmac");

    return 0;
}

5. declaration of two dimensional array using dynamic memory allocation 

#include <stdio.h>
#include <stdlib.h>

int main()
{
    int rows, cols, i, j;
    int **arr;

    printf("Enter number of rows: ");
    scanf("%d", &rows);

    printf("Enter number of columns: ");
    scanf("%d", &cols);

    
    arr = (int **)malloc(rows * sizeof(int *));

    
    if (arr == NULL)
    {
        printf("Memory allocation failed\n");
        return 1;
    }

    for (i = 0; i < rows; i++)
    {
        arr[i] = (int *)malloc(cols * sizeof(int));

        if (arr[i] == NULL)
        {
            printf("Memory allocation failed\n");
            return 1;
        }
    }

    
    printf("Enter elements of the 2D array:\n");
    for (i = 0; i < rows; i++)
    {
        for (j = 0; j < cols; j++)
        {
            scanf("%d", &arr[i][j]);
        }
    }

    
    printf("\n2D Array elements:\n");
    for (i = 0; i < rows; i++)
    {
        for (j = 0; j < cols; j++)
        {
            printf("%d ", arr[i][j]);
        }
        printf("\n");
    }

    
    printf("\nGetting MAC address:\n");
    system("getmac");

    
    for (i = 0; i < rows; i++)
    {
        free(arr[i]);
    }
    free(arr);

    return 0;
}

6. pattern matching 

#include <stdio.h>
#include <string.h>
#include <stdlib.h>

int main()
{
    char text[100], pattern[50];
    int i, j, found = 0;

    printf("Enter the main string: ");
    gets(text);   // used for exam simplicity

    printf("Enter the pattern: ");
    gets(pattern);

    int n = strlen(text);
    int m = strlen(pattern);

    
    for (i = 0; i <= n - m; i++)
    {
        for (j = 0; j < m; j++)
        {
            if (text[i + j] != pattern[j])
                break;
        }

        if (j == m)
        {
            printf("Pattern found at position %d\n", i + 1);
            found = 1;
        }
    }

    if (!found)
        printf("Pattern not found\n");

    
    printf("\nGetting MAC address:\n");
    system("getmac");

    return 0;
}

7. self referential structure 

#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node *next;   
};

int main()
{
    struct Node *head = NULL;
    struct Node *second = NULL;
    struct Node *third = NULL;

    
    head = (struct Node *)malloc(sizeof(struct Node));
    second = (struct Node *)malloc(sizeof(struct Node));
    third = (struct Node *)malloc(sizeof(struct Node));

    if (head == NULL || second == NULL || third == NULL) {
        printf("Memory allocation failed\n");
        return 1;
    }

    
    head->data = 10;
    head->next = second;

    second->data = 20;
    second->next = third;

    third->data = 30;
    third->next = NULL;

    
    struct Node *ptr = head;
    printf("Linked List Elements:\n");
    while (ptr != NULL) {
        printf("%d -> ", ptr->data);
        ptr = ptr->next;
    }
    printf("NULL\n");

    
    printf("\nGetting MAC address:\n");
    system("getmac");

    
    free(head);
    free(second);
    free(third);

    return 0;
}

8th. implement pre increment and post increment 

#include <stdio.h>
#include <stdlib.h>

int main()
{
    int a, b;

    printf("Enter a value for a: ");
    scanf("%d", &a);

    printf("Enter a value for b: ");
    scanf("%d", &b);

    printf("\nDemonstrating Pre-Increment and Post-Increment:\n");

    
    printf("Pre-increment of a: %d\n", ++a); 
    printf("Value of a after pre-increment: %d\n", a);

    
    printf("Post-increment of b: %d\n", b++); 
    printf("Value of b after post-increment: %d\n", b);

    
    printf("\nGetting MAC address:\n");
    system("getmac");

    return 0;
}

9. implement pre decrement and post decrement 

#include <stdio.h>
#include <stdlib.h>

int main()
{
    int a, b;

    printf("Enter a value for a: ");
    scanf("%d", &a);

    printf("Enter a value for b: ");
    scanf("%d", &b);

    printf("\nDemonstrating Pre-Decrement and Post-Decrement:\n");

    
    printf("Pre-decrement of a: %d\n", --a); 
    printf("Value of a after pre-decrement: %d\n", a);

    
    printf("Post-decrement of b: %d\n", b--); 
    printf("Value of b after post-decrement: %d\n", b);

    
    printf("\nGetting MAC address:\n");
    system("getmac");

    return 0;
}

10. implement regular queues 

#include <stdio.h>
#include <stdlib.h>

#define MAX 5  

int queue[MAX];
int front = -1, rear = -1;


int isFull() {
    return rear == MAX - 1;
}


int isEmpty() {
    return front == -1 || front > rear;
}


void enqueue(int value) {
    if (isFull()) {
        printf("Queue Overflow! Cannot insert %d\n", value);
        return;
    }
    if (front == -1) front = 0;
    rear++;
    queue[rear] = value;
    printf("Inserted %d\n", value);
}
void dequeue() {
    if (isEmpty()) {
        printf("Queue Underflow! Nothing to delete\n");
        return;
    }
    printf("Deleted %d\n", queue[front]);
    front++;
}
void display() {
    if (isEmpty()) {
        printf("Queue is empty\n");
        return;
    }
    printf("Queue elements: ");
    for (int i = front; i <= rear; i++) {
        printf("%d ", queue[i]);
    }
    printf("\n");
}

int main() {
    int choice, value;

    do {
        printf("\nQueue Operations:\n");
        printf("1. Enqueue\n2. Dequeue\n3. Display\n4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                printf("Enter value to insert: ");
                scanf("%d", &value);
                enqueue(value);
                break;
            case 2:
                dequeue();
                break;
            case 3:
                display();
                break;
            case 4:
                printf("Exiting...\n");
                break;
            default:
                printf("Invalid choice! Try again.\n");
        }
    } while (choice != 4);
    printf("\nGetting MAC address:\n");
    system("getmac");

    return 0;
}


11. implement the operations of linkedlist 

#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* next;
};

void traverse(struct Node* head) {
    if (head == NULL) {
        printf("List is empty.\n");
        return;
    }
    struct Node* temp = head;
    printf("Linked List Elements: ");
    while (temp != NULL) {
        printf("%d -> ", temp->data);
        temp = temp->next;
    }
    printf("NULL\n");
}

void insertAtBeginning(struct Node** head, int value) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = value;
    newNode->next = *head;
    *head = newNode;
    printf("Inserted %d at beginning\n", value);
}

void deleteNode(struct Node** head, int value) {
    struct Node* temp = *head;
    struct Node* prev = NULL;

    if (temp != NULL && temp->data == value) {
        *head = temp->next;
        free(temp);
        printf("Deleted %d\n", value);
        return;
    }

    while (temp != NULL && temp->data != value) {
        prev = temp;
        temp = temp->next;
    }

    if (temp == NULL) {
        printf("%d not found in the list\n", value);
        return;
    }

    prev->next = temp->next;
    free(temp);
    printf("Deleted %d\n", value);
}

int main() {
    struct Node* head = NULL;
    int choice, value;

    do {
        printf("\nLinked List Operations:\n");
        printf("1. Insert at beginning\n2. Delete a node\n3. Traverse\n4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                printf("Enter value to insert: ");
                scanf("%d", &value);
                insertAtBeginning(&head, value);
                break;
            case 2:
                printf("Enter value to delete: ");
                scanf("%d", &value);
                deleteNode(&head, value);
                break;
            case 3:
                traverse(head);
                break;
            case 4:
                printf("Exiting...\n");
                break;
            default:
                printf("Invalid choice! Try again.\n");
        }
    } while (choice != 4);

    printf("\nGetting MAC address:\n");
    system("getmac");

    struct Node* temp;
    while (head != NULL) {
        temp = head;
        head = head->next;
        free(temp);
    }

    return 0;
}

12. implement Linked list using stacks 

#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* next;
};

void push(struct Node** top, int value) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    if (newNode == NULL) {
        printf("Memory allocation failed\n");
        return;
    }
    newNode->data = value;
    newNode->next = *top;
    *top = newNode;
    printf("Pushed %d onto stack\n", value);
}

void pop(struct Node** top) {
    if (*top == NULL) {
        printf("Stack Underflow!\n");
        return;
    }
    struct Node* temp = *top;
    printf("Popped %d from stack\n", temp->data);
    *top = (*top)->next;
    free(temp);
}

void display(struct Node* top) {
    if (top == NULL) {
        printf("Stack is empty\n");
        return;
    }
    printf("Stack elements (top to bottom): ");
    while (top != NULL) {
        printf("%d ", top->data);
        top = top->next;
    }
    printf("\n");
}

int main() {
    struct Node* top = NULL;
    int choice, value;

    do {
        printf("\nStack Operations using Linked List:\n");
        printf("1. Push\n2. Pop\n3. Display\n4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                printf("Enter value to push: ");
                scanf("%d", &value);
                push(&top, value);
                break;
            case 2:
                pop(&top);
                break;
            case 3:
                display(top);
                break;
            case 4:
                printf("Exiting...\n");
                break;
            default:
                printf("Invalid choice! Try again.\n");
        }
    } while (choice != 4);

    printf("\nGetting MAC address:\n");
    system("getmac");

    struct Node* temp;
    while (top != NULL) {
        temp = top;
        top = top->next;
        free(temp);
    }

    return 0;
}

13. implement Linked list using queues 

#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* next;
};

struct Node* front = NULL;
struct Node* rear = NULL;

void enqueue(int value) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    if (newNode == NULL) {
        printf("Memory allocation failed\n");
        return;
    }
    newNode->data = value;
    newNode->next = NULL;

    if (rear == NULL) {
        front = rear = newNode;
    } else {
        rear->next = newNode;
        rear = newNode;
    }
    printf("Enqueued %d\n", value);
}

void dequeue() {
    if (front == NULL) {
        printf("Queue Underflow!\n");
        return;
    }
    struct Node* temp = front;
    printf("Dequeued %d\n", temp->data);
    front = front->next;

    if (front == NULL)
        rear = NULL;

    free(temp);
}

void display() {
    if (front == NULL) {
        printf("Queue is empty\n");
        return;
    }
    struct Node* temp = front;
    printf("Queue elements: ");
    while (temp != NULL) {
        printf("%d ", temp->data);
        temp = temp->next;
    }
    printf("\n");
}

int main() {
    int choice, value;

    do {
        printf("\nQueue Operations using Linked List:\n");
        printf("1. Enqueue\n2. Dequeue\n3. Display\n4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                printf("Enter value to enqueue: ");
                scanf("%d", &value);
                enqueue(value);
                break;
            case 2:
                dequeue();
                break;
            case 3:
                display();
                break;
            case 4:
                printf("Exiting...\n");
                break;
            default:
                printf("Invalid choice! Try again.\n");
        }
    } while (choice != 4);

    printf("\nGetting MAC address:\n");
    system("getmac");

    struct Node* temp;
    while (front != NULL) {
        temp = front;
        front = front->next;
        free(temp);
    }

    return 0;
}

14. time taken for linked list during insertion and deletion 

#include <stdio.h>
#include <stdlib.h>
#include <time.h>

struct Node {
    int data;
    struct Node* next;
};

void insertLinkedList(struct Node** head, int value) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = value;
    newNode->next = *head;
    *head = newNode;
}

void deleteLinkedList(struct Node** head) {
    if (*head == NULL) return;
    struct Node* temp = *head;
    *head = (*head)->next;
    free(temp);
}

int main() {
    int n, i;
    printf("Enter number of elements: ");
    scanf("%d", &n);

    int* arr = (int*)malloc(n * sizeof(int));

    clock_t startArray, endArray;
    double timeArray;

    startArray = clock();
    for (i = n - 1; i >= 0; i--) {
        arr[i] = i;
    }
    endArray = clock();
    timeArray = ((double)(endArray - startArray)) / CLOCKS_PER_SEC;
    printf("Time taken for insertion in array: %f seconds\n", timeArray);

    startArray = clock();
    for (i = 0; i < n; i++) {
        for (int j = 0; j < n - 1 - i; j++) {
            arr[j] = arr[j + 1];
        }
    }
    endArray = clock();
    timeArray = ((double)(endArray - startArray)) / CLOCKS_PER_SEC;
    printf("Time taken for deletion in array: %f seconds\n", timeArray);

    free(arr);

    struct Node* head = NULL;

    clock_t startLL, endLL;
    double timeLL;

    startLL = clock();
    for (i = 0; i < n; i++) {
        insertLinkedList(&head, i);
    }
    endLL = clock();
    timeLL = ((double)(endLL - startLL)) / CLOCKS_PER_SEC;
    printf("Time taken for insertion in linked list: %f seconds\n", timeLL);

    startLL = clock();
    for (i = 0; i < n; i++) {
        deleteLinkedList(&head);
    }
    endLL = clock();
    timeLL = ((double)(endLL - startLL)) / CLOCKS_PER_SEC;
    printf("Time taken for deletion in linked list: %f seconds\n", timeLL);

    printf("\nGetting MAC address:\n");
    system("getmac");

    return 0;
}

15. implement sparse matrix

#include <stdio.h>
#include <stdlib.h>

struct Sparse {
    int row;
    int col;
    int value;
};

int main() {
    int rows, cols, i, j, count = 0;

    printf("Enter number of rows: ");
    scanf("%d", &rows);
    printf("Enter number of columns: ");
    scanf("%d", &cols);

    int matrix[rows][cols];

    printf("Enter elements of the matrix:\n");
    for (i = 0; i < rows; i++) {
        for (j = 0; j < cols; j++) {
            scanf("%d", &matrix[i][j]);
            if (matrix[i][j] != 0) count++;
        }
    }

    struct Sparse* sparse = (struct Sparse*)malloc(count * sizeof(struct Sparse));
    if (sparse == NULL) {
        printf("Memory allocation failed\n");
        return 1;
    }

    int k = 0;
    for (i = 0; i < rows; i++) {
        for (j = 0; j < cols; j++) {
            if (matrix[i][j] != 0) {
                sparse[k].row = i;
                sparse[k].col = j;
                sparse[k].value = matrix[i][j];
                k++;
            }
        }
    }

    printf("\nSparse Matrix Representation (row, column, value):\n");
    printf("Row\tCol\tValue\n");
    for (i = 0; i < count; i++) {
        printf("%d\t%d\t%d\n", sparse[i].row, sparse[i].col, sparse[i].value);
    }

    printf("\nGetting MAC address:\n");
    system("getmac");

    free(sparse);
    return 0;
}
16. implement polynomial representation 


#include <stdio.h>
#include <stdlib.h>

struct Node {
    int coeff;
    int exp;
    struct Node* next;
};

struct Node* createNode(int c, int e) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->coeff = c;
    newNode->exp = e;
    newNode->next = NULL;
    return newNode;
}

void insertTerm(struct Node** head, int coeff, int exp) {
    struct Node* newNode = createNode(coeff, exp);
    if (*head == NULL) {
        *head = newNode;
        return;
    }
    struct Node* temp = *head;
    while (temp->next != NULL) {
        temp = temp->next;
    }
    temp->next = newNode;
}

void displayPolynomial(struct Node* head) {
    if (head == NULL) {
        printf("Polynomial is empty.\n");
        return;
    }
    struct Node* temp = head;
    while (temp != NULL) {
        printf("%dx^%d", temp->coeff, temp->exp);
        if (temp->next != NULL) printf(" + ");
        temp = temp->next;
    }
    printf("\n");
}

int main() {
    struct Node* poly = NULL;
    int n, coeff, exp;

    printf("Enter number of terms in polynomial: ");
    scanf("%d", &n);

    for (int i = 0; i < n; i++) {
        printf("Enter coefficient and exponent for term %d: ", i + 1);
        scanf("%d %d", &coeff, &exp);
        insertTerm(&poly, coeff, exp);
    }

    printf("\nPolynomial is: ");
    displayPolynomial(poly);

    printf("\nGetting MAC address:\n");
    system("getmac");

    struct Node* temp;
    while (poly != NULL) {
        temp = poly;
        poly = poly->next;
        free(temp);
    }

    return 0;
}

17. creation of tree 

#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

struct Node* createNode(int value) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = value;
    newNode->left = newNode->right = NULL;
    return newNode;
}

void inorderTraversal(struct Node* root) {
    if (root != NULL) {
        inorderTraversal(root->left);
        printf("%d ", root->data);
        inorderTraversal(root->right);
    }
}

void preorderTraversal(struct Node* root) {
    if (root != NULL) {
        printf("%d ", root->data);
        preorderTraversal(root->left);
        preorderTraversal(root->right);
    }
}

void postorderTraversal(struct Node* root) {
    if (root != NULL) {
        postorderTraversal(root->left);
        postorderTraversal(root->right);
        printf("%d ", root->data);
    }
}

int main() {
    struct Node* root = NULL;
    int n, value;

    printf("Enter number of nodes: ");
    scanf("%d", &n);

    for (int i = 0; i < n; i++) {
        printf("Enter value for node %d: ", i + 1);
        scanf("%d", &value);

        struct Node* newNode = createNode(value);

        if (root == NULL) {
            root = newNode;
        } else {
            struct Node* queue[100];
            int front = 0, rear = 0;
            queue[rear++] = root;

            while (front < rear) {
                struct Node* temp = queue[front++];

                if (temp->left == NULL) {
                    temp->left = newNode;
                    break;
                } else {
                    queue[rear++] = temp->left;
                }

                if (temp->right == NULL) {
                    temp->right = newNode;
                    break;
                } else {
                    queue[rear++] = temp->right;
                }
            }
        }
    }

    printf("\nInorder Traversal: ");
    inorderTraversal(root);
    printf("\nPreorder Traversal: ");
    preorderTraversal(root);
    printf("\nPostorder Traversal: ");
    postorderTraversal(root);

    printf("\n\nGetting MAC address:\n");
    system("getmac");

    struct Node* stack[100];
    int top = -1;
    if (root != NULL) stack[++top] = root;
    while (top >= 0) {
        struct Node* temp = stack[top--];
        if (temp->left) stack[++top] = temp->left;
        if (temp->right) stack[++top] = temp->right;
        free(temp);
    }

    return 0;
}

18. implement a tree using arrays 

#include <stdio.h>
#include <stdlib.h>

#define MAX 100

int tree[MAX];
int size = 0;

void inorder(int index) {
    if (index >= size || tree[index] == -1)
        return;
    inorder(2 * index + 1);
    printf("%d ", tree[index]);
    inorder(2 * index + 2);
}

void preorder(int index) {
    if (index >= size || tree[index] == -1)
        return;
    printf("%d ", tree[index]);
    preorder(2 * index + 1);
    preorder(2 * index + 2);
}

void postorder(int index) {
    if (index >= size || tree[index] == -1)
        return;
    postorder(2 * index + 1);
    postorder(2 * index + 2);
    printf("%d ", tree[index]);
}

int main() {
    int n, value;

    printf("Enter number of nodes: ");
    scanf("%d", &n);
    size = n;

    printf("Enter %d node values (-1 for NULL):\n", n);
    for (int i = 0; i < n; i++) {
        scanf("%d", &tree[i]);
    }

    printf("\nInorder Traversal: ");
    inorder(0);

    printf("\nPreorder Traversal: ");
    preorder(0);

    printf("\nPostorder Traversal: ");
    postorder(0);

    printf("\n\nGetting MAC address:\n");
    system("getmac");

    return 0;
}

19. implement a binary tree using queues 
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

struct Queue {
    struct Node* nodes[100];
    int front, rear;
};

void initQueue(struct Queue* q) {
    q->front = 0;
    q->rear = 0;
}

void enqueue(struct Queue* q, struct Node* node) {
    q->nodes[q->rear++] = node;
}

struct Node* dequeue(struct Queue* q) {
    return q->nodes[q->front++];
}

int isEmpty(struct Queue* q) {
    return q->front == q->rear;
}

struct Node* createNode(int value) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = value;
    newNode->left = newNode->right = NULL;
    return newNode;
}

void inorder(struct Node* root) {
    if (root != NULL) {
        inorder(root->left);
        printf("%d ", root->data);
        inorder(root->right);
    }
}

int main() {
    struct Queue q;
    initQueue(&q);

    int value;
    printf("Enter root value: ");
    scanf("%d", &value);

    struct Node* root = createNode(value);
    enqueue(&q, root);

    char choice;
    while (!isEmpty(&q)) {
        struct Node* current = dequeue(&q);

        printf("Do you want to insert left child of %d? (y/n): ", current->data);
        scanf(" %c", &choice);
        if (choice == 'y' || choice == 'Y') {
            printf("Enter value: ");
            scanf("%d", &value);
            current->left = createNode(value);
            enqueue(&q, current->left);
        }

        printf("Do you want to insert right child of %d? (y/n): ", current->data);
        scanf(" %c", &choice);
        if (choice == 'y' || choice == 'Y') {
            printf("Enter value: ");
            scanf("%d", &value);
            current->right = createNode(value);
            enqueue(&q, current->right);
        }
    }

    printf("\nInorder traversal of tree: ");
    inorder(root);

    printf("\n\nGetting MAC address:\n");
    system("getmac");

    struct Node* stack[100];
    int top = -1;
    if (root != NULL) stack[++top] = root;
    while (top >= 0) {
        struct Node* temp = stack[top--];
        if (temp->left) stack[++top] = temp->left;
        if (temp->right) stack[++top] = temp->right;
        free(temp);
    }

    return 0;
}

20. insertion of nodes 
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

struct Queue {
    struct Node* nodes[100];
    int front, rear;
};

void initQueue(struct Queue* q) {
    q->front = 0;
    q->rear = 0;
}

void enqueue(struct Queue* q, struct Node* node) {
    q->nodes[q->rear++] = node;
}

struct Node* dequeue(struct Queue* q) {
    return q->nodes[q->front++];
}

int isEmpty(struct Queue* q) {
    return q->front == q->rear;
}

struct Node* createNode(int value) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = value;
    newNode->left = newNode->right = NULL;
    return newNode;
}

void insertNode(struct Node* root, int value) {
    struct Queue q;
    initQueue(&q);
    enqueue(&q, root);

    while (!isEmpty(&q)) {
        struct Node* temp = dequeue(&q);

        if (temp->left == NULL) {
            temp->left = createNode(value);
            printf("Inserted %d as left child of %d\n", value, temp->data);
            return;
        } else {
            enqueue(&q, temp->left);
        }

        if (temp->right == NULL) {
            temp->right = createNode(value);
            printf("Inserted %d as right child of %d\n", value, temp->data);
            return;
        } else {
            enqueue(&q, temp->right);
        }
    }
}

void inorder(struct Node* root) {
    if (root != NULL) {
        inorder(root->left);
        printf("%d ", root->data);
        inorder(root->right);
    }
}

int main() {
    int rootValue, value;

    printf("Enter root node value: ");
    scanf("%d", &rootValue);

    struct Node* root = createNode(rootValue);

    int n;
    printf("How many nodes to insert? ");
    scanf("%d", &n);

    for (int i = 0; i < n; i++) {
        printf("Enter value to insert: ");
        scanf("%d", &value);
        insertNode(root, value);
    }

    printf("\nInorder traversal of tree: ");
    inorder(root);

    printf("\n\nGetting MAC address:\n");
    system("getmac");

    struct Node* stack[100];
    int top = -1;
    if (root != NULL) stack[++top] = root;
    while (top >= 0) {
        struct Node* temp = stack[top--];
        if (temp->left) stack[++top] = temp->left;
        if (temp->right) stack[++top] = temp->right;
        free(temp);
    }

    return 0;
}


21. deletion of nodes 
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

struct Queue {
    struct Node* nodes[100];
    int front, rear;
};

void initQueue(struct Queue* q) { q->front = 0; q->rear = 0; }
void enqueue(struct Queue* q, struct Node* node) { q->nodes[q->rear++] = node; }
struct Node* dequeue(struct Queue* q) { return q->nodes[q->front++]; }
int isEmpty(struct Queue* q) { return q->front == q->rear; }

struct Node* createNode(int value) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = value;
    newNode->left = newNode->right = NULL;
    return newNode;
}

void inorder(struct Node* root) {
    if (root != NULL) {
        inorder(root->left);
        printf("%d ", root->data);
        inorder(root->right);
    }
}

void deleteDeepest(struct Node* root, struct Node* dNode) {
    struct Queue q;
    initQueue(&q);
    enqueue(&q, root);

    while (!isEmpty(&q)) {
        struct Node* temp = dequeue(&q);
        if (temp->left) {
            if (temp->left == dNode) {
                free(temp->left);
                temp->left = NULL;
                return;
            } else {
                enqueue(&q, temp->left);
            }
        }
        if (temp->right) {
            if (temp->right == dNode) {
                free(temp->right);
                temp->right = NULL;
                return;
            } else {
                enqueue(&q, temp->right);
            }
        }
    }
}

void deleteNode(struct Node* root, int key) {
    if (root == NULL) return;

    if (root->left == NULL && root->right == NULL) {
        if (root->data == key) {
            free(root);
            root = NULL;
        }
        return;
    }

    struct Queue q;
    initQueue(&q);
    enqueue(&q, root);

    struct Node *temp, *keyNode = NULL;
    while (!isEmpty(&q)) {
        temp = dequeue(&q);
        if (temp->data == key) keyNode = temp;
        if (temp->left) enqueue(&q, temp->left);
        if (temp->right) enqueue(&q, temp->right);
    }

    if (keyNode != NULL) {
        int x = temp->data;
        deleteDeepest(root, temp);
        keyNode->data = x;
        printf("Deleted node with value %d\n", key);
    } else {
        printf("Node with value %d not found\n", key);
    }
}

int main() {
    int rootValue;
    printf("Enter root node value: ");
    scanf("%d", &rootValue);
    struct Node* root = createNode(rootValue);

    int n, value;
    printf("How many nodes to insert? ");
    scanf("%d", &n);

    for (int i = 0; i < n; i++) {
        printf("Enter value to insert: ");
        scanf("%d", &value);

        struct Queue q;
        initQueue(&q);
        enqueue(&q, root);
        while (!isEmpty(&q)) {
            struct Node* temp = dequeue(&q);
            if (temp->left == NULL) {
                temp->left = createNode(value);
                break;
            } else enqueue(&q, temp->left);

            if (temp->right == NULL) {
                temp->right = createNode(value);
                break;
            } else enqueue(&q, temp->right);
        }
    }

    printf("\nInorder traversal before deletion: ");
    inorder(root);

    printf("\nEnter value to delete: ");
    scanf("%d", &value);
    deleteNode(root, value);

    printf("\nInorder traversal after deletion: ");
    inorder(root);

    printf("\n\nGetting MAC address:\n");
    system("getmac");

    struct Node* stack[100];
    int top = -1;
    if (root != NULL) stack[++top] = root;
    while (top >= 0) {
        struct Node* temp = stack[top--];
        if (temp->left) stack[++top] = temp->left;
        if (temp->right) stack[++top] = temp->right;
        free(temp);
    }

    return 0;
}

22. implement depth search tree 
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

struct Node* createNode(int value) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = value;
    newNode->left = newNode->right = NULL;
    return newNode;
}

void dfsPreorder(struct Node* root) {
    if (root != NULL) {
        printf("%d ", root->data);
        dfsPreorder(root->left);
        dfsPreorder(root->right);
    }
}

void dfsInorder(struct Node* root) {
    if (root != NULL) {
        dfsInorder(root->left);
        printf("%d ", root->data);
        dfsInorder(root->right);
    }
}

void dfsPostorder(struct Node* root) {
    if (root != NULL) {
        dfsPostorder(root->left);
        dfsPostorder(root->right);
        printf("%d ", root->data);
    }
}

struct Node* insertLevelOrder(struct Node* root, int value) {
    if (root == NULL) return createNode(value);

    struct Node* queue[100];
    int front = 0, rear = 0;
    queue[rear++] = root;

    while (front < rear) {
        struct Node* temp = queue[front++];

        if (temp->left == NULL) {
            temp->left = createNode(value);
            break;
        } else {
            queue[rear++] = temp->left;
        }

        if (temp->right == NULL) {
            temp->right = createNode(value);
            break;
        } else {
            queue[rear++] = temp->right;
        }
    }
    return root;
}

int main() {
    int rootValue, n, value;

    printf("Enter root node value: ");
    scanf("%d", &rootValue);
    struct Node* root = createNode(rootValue);

    printf("How many more nodes to insert? ");
    scanf("%d", &n);

    for (int i = 0; i < n; i++) {
        printf("Enter value to insert: ");
        scanf("%d", &value);
        root = insertLevelOrder(root, value);
    }

    printf("\nDFS Traversals:\n");

    printf("Preorder: ");
    dfsPreorder(root);

    printf("\nInorder: ");
    dfsInorder(root);

    printf("\nPostorder: ");
    dfsPostorder(root);

    printf("\n\nGetting MAC address:\n");
    system("getmac");

    struct Node* stack[100];
    int top = -1;
    if (root != NULL) stack[++top] = root;
    while (top >= 0) {
        struct Node* temp = stack[top--];
        if (temp->left) stack[++top] = temp->left;
        if (temp->right) stack[++top] = temp->right;
        free(temp);
    }

    return 0;
}

23. implement breadth search tree 
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

struct Queue {
    struct Node* nodes[100];
    int front, rear;
};

void initQueue(struct Queue* q) { q->front = 0; q->rear = 0; }
void enqueue(struct Queue* q, struct Node* node) { q->nodes[q->rear++] = node; }
struct Node* dequeue(struct Queue* q) { return q->nodes[q->front++]; }
int isEmpty(struct Queue* q) { return q->front == q->rear; }

struct Node* createNode(int value) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = value;
    newNode->left = newNode->right = NULL;
    return newNode;
}

struct Node* insertLevelOrder(struct Node* root, int value) {
    if (root == NULL) return createNode(value);

    struct Queue q;
    initQueue(&q);
    enqueue(&q, root);

    while (!isEmpty(&q)) {
        struct Node* temp = dequeue(&q);

        if (temp->left == NULL) {
            temp->left = createNode(value);
            break;
        } else {
            enqueue(&q, temp->left);
        }

        if (temp->right == NULL) {
            temp->right = createNode(value);
            break;
        } else {
            enqueue(&q, temp->right);
        }
    }
    return root;
}

void bfsTraversal(struct Node* root) {
    if (root == NULL) return;

    struct Queue q;
    initQueue(&q);
    enqueue(&q, root);

    printf("BFS Traversal: ");
    while (!isEmpty(&q)) {
        struct Node* temp = dequeue(&q);
        printf("%d ", temp->data);

        if (temp->left) enqueue(&q, temp->left);
        if (temp->right) enqueue(&q, temp->right);
    }
    printf("\n");
}

int main() {
    int rootValue, n, value;

    printf("Enter root node value: ");
    scanf("%d", &rootValue);
    struct Node* root = createNode(rootValue);

    printf("How many more nodes to insert? ");
    scanf("%d", &n);

    for (int i = 0; i < n; i++) {
        printf("Enter value to insert: ");
        scanf("%d", &value);
        root = insertLevelOrder(root, value);
    }

    bfsTraversal(root);

    printf("\nGetting MAC address:\n");
    system("getmac");

    struct Node* stack[100];
    int top = -1;
    if (root != NULL) stack[++top] = root;
    while (top >= 0) {
        struct Node* temp = stack[top--];
        if (temp->left) stack[++top] = temp->left;
        if (temp->right) stack[++top] = temp->right;
        free(temp);
    }

    return 0;
}

24. implement level order
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

struct Queue {
    struct Node* nodes[100];
    int front, rear;
};

void initQueue(struct Queue* q) { q->front = 0; q->rear = 0; }
void enqueue(struct Queue* q, struct Node* node) { q->nodes[q->rear++] = node; }
struct Node* dequeue(struct Queue* q) { return q->nodes[q->front++]; }
int isEmpty(struct Queue* q) { return q->front == q->rear; }

struct Node* createNode(int value) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = value;
    newNode->left = newNode->right = NULL;
    return newNode;
}

struct Node* insertLevelOrder(struct Node* root, int value) {
    if (root == NULL) return createNode(value);

    struct Queue q;
    initQueue(&q);
    enqueue(&q, root);

    while (!isEmpty(&q)) {
        struct Node* temp = dequeue(&q);

        if (temp->left == NULL) {
            temp->left = createNode(value);
            break;
        } else {
            enqueue(&q, temp->left);
        }

        if (temp->right == NULL) {
            temp->right = createNode(value);
            break;
        } else {
            enqueue(&q, temp->right);
        }
    }
    return root;
}

void levelOrderTraversal(struct Node* root) {
    if (root == NULL) return;

    struct Queue q;
    initQueue(&q);
    enqueue(&q, root);

    printf("Level-Order Traversal: ");
    while (!isEmpty(&q)) {
        struct Node* temp = dequeue(&q);
        printf("%d ", temp->data);

        if (temp->left) enqueue(&q, temp->left);
        if (temp->right) enqueue(&q, temp->right);
    }
    printf("\n");
}

int main() {
    int rootValue, n, value;

    printf("Enter root node value: ");
    scanf("%d", &rootValue);
    struct Node* root = createNode(rootValue);

    printf("How many more nodes to insert? ");
    scanf("%d", &n);

    for (int i = 0; i < n; i++) {
        printf("Enter value to insert: ");
        scanf("%d", &value);
        root = insertLevelOrder(root, value);
    }

    levelOrderTraversal(root);

    printf("\nGetting MAC address:\n");
    system("getmac");

    struct Node* stack[100];
    int top = -1;
    if (root != NULL) stack[++top] = root;
    while (top >= 0) {
        struct Node* temp = stack[top--];
        if (temp->left) stack[++top] = temp->left;
        if (temp->right) stack[++top] = temp->right;
        free(temp);
    }

    return 0;
}

25. dfs and bfs using adjacency list


#include <stdio.h>
#include <stdlib.h>

#define MAX 100

struct Node {
    int vertex;
    struct Node* next;
};

struct Graph {
    int vertices;
    struct Node* adjList[MAX];
};

struct Stack {
    int data[MAX];
    int top;
};

struct Queue {
    int data[MAX];
    int front, rear;
};

void initStack(struct Stack* s) {
    s->top = -1;
}
void push(struct Stack* s, int value) {
    s->data[++s->top] = value;
}
int pop(struct Stack* s) {
    return s->data[s->top--];
}
int isStackEmpty(struct Stack* s) {
    return s->top == -1;
}

void initQueue(struct Queue* q) {
    q->front = q->rear = 0;
}
void enqueue(struct Queue* q, int value) {
    q->data[q->rear++] = value;
}
int dequeue(struct Queue* q) {
    return q->data[q->front++];
}
int isQueueEmpty(struct Queue* q) {
    return q->front == q->rear;
}

struct Node* createNode(int v) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->vertex = v;
    newNode->next = NULL;
    return newNode;
}

struct Graph* createGraph(int vertices) {
    struct Graph* graph = (struct Graph*)malloc(sizeof(struct Graph));
    graph->vertices = vertices;

    for (int i = 0; i < vertices; i++)
        graph->adjList[i] = NULL;

    return graph;
}

void addEdge(struct Graph* graph, int src, int dest) {
    struct Node* newNode = createNode(dest);
    newNode->next = graph->adjList[src];
    graph->adjList[src] = newNode;

    newNode = createNode(src);
    newNode->next = graph->adjList[dest];
    graph->adjList[dest] = newNode;
}

void DFS(struct Graph* graph, int start) {
    int visited[MAX] = {0};
    struct Stack s;
    initStack(&s);

    push(&s, start);

    printf("DFS Traversal: ");
    while (!isStackEmpty(&s)) {
        int v = pop(&s);

        if (!visited[v]) {
            printf("%d ", v);
            visited[v] = 1;

            struct Node* temp = graph->adjList[v];
            while (temp) {
                if (!visited[temp->vertex])
                    push(&s, temp->vertex);
                temp = temp->next;
            }
        }
    }
    printf("\n");
}

void BFS(struct Graph* graph, int start) {
    int visited[MAX] = {0};
    struct Queue q;
    initQueue(&q);

    enqueue(&q, start);
    visited[start] = 1;

    printf("BFS Traversal: ");
    while (!isQueueEmpty(&q)) {
        int v = dequeue(&q);
        printf("%d ", v);

        struct Node* temp = graph->adjList[v];
        while (temp) {
            if (!visited[temp->vertex]) {
                visited[temp->vertex] = 1;
                enqueue(&q, temp->vertex);
            }
            temp = temp->next;
        }
    }
    printf("\n");
}

int main() {
    int vertices, edges, src, dest, start;

    printf("Enter number of vertices: ");
    scanf("%d", &vertices);

    struct Graph* graph = createGraph(vertices);

    printf("Enter number of edges: ");
    scanf("%d", &edges);

    for (int i = 0; i < edges; i++) {
        printf("Enter edge (src dest): ");
        scanf("%d %d", &src, &dest);
        addEdge(graph, src, dest);
    }

    printf("Enter starting vertex: ");
    scanf("%d", &start);

    DFS(graph, start);
    BFS(graph, start);

    printf("\nGetting MAC address:\n");
    system("getmac");

    return 0;
}

26. calloc() and malloc() function checking if junk is initialized 
#include <stdio.h>
#include <stdlib.h>

int main() {
    int n = 5;
    int *mallocArr, *callocArr;

    mallocArr = (int*)malloc(n * sizeof(int));
    callocArr = (int*)calloc(n, sizeof(int));

    printf("Values in malloc array (junk/garbage values):\n");
    for (int i = 0; i < n; i++) {
        printf("%d ", mallocArr[i]);
    }
    printf("\n");

    printf("Values in calloc array (initialized to 0):\n");
    for (int i = 0; i < n; i++) {
        printf("%d ", callocArr[i]);
    }
    printf("\n");

    printf("\nGetting MAC address:\n");
    system("getmac");

    free(mallocArr);
    free(callocArr);

    return 0;
}

27. implement circular linked list 
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* next;
};

struct Node* createNode(int value) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = value;
    newNode->next = newNode;
    return newNode;
}

struct Node* insertEnd(struct Node* tail, int value) {
    struct Node* newNode = createNode(value);
    if (tail == NULL) {
        return newNode;
    }
    newNode->next = tail->next;
    tail->next = newNode;
    return newNode;
}

struct Node* deleteNode(struct Node* tail, int value) {
    if (tail == NULL) return NULL;

    struct Node *curr = tail->next, *prev = tail;
    do {
        if (curr->data == value) {
            if (curr == prev) {
                free(curr);
                return NULL;
            }
            prev->next = curr->next;
            if (curr == tail) tail = prev;
            free(curr);
            return tail;
        }
        prev = curr;
        curr = curr->next;
    } while (curr != tail->next);

    printf("Node with value %d not found.\n", value);
    return tail;
}

void traverse(struct Node* tail) {
    if (tail == NULL) {
        printf("List is empty.\n");
        return;
    }
    struct Node* temp = tail->next;
    printf("Circular Linked List: ");
    do {
        printf("%d ", temp->data);
        temp = temp->next;
    } while (temp != tail->next);
    printf("\n");
}

void freeList(struct Node* tail) {
    if (tail == NULL) return;

    struct Node* head = tail->next;
    struct Node* temp;
    while (head != tail) {
        temp = head;
        head = head->next;
        free(temp);
    }
    free(tail);
}

int main() {
    struct Node* tail = NULL;
    int n, value;

    printf("How many nodes to insert? ");
    scanf("%d", &n);

    for (int i = 0; i < n; i++) {
        printf("Enter value to insert: ");
        scanf("%d", &value);
        tail = insertEnd(tail, value);
    }

    traverse(tail);

    printf("Enter value to delete: ");
    scanf("%d", &value);
    tail = deleteNode(tail, value);

    traverse(tail);

    printf("\nGetting MAC address:\n");
    system("getmac");

    freeList(tail);
    return 0;
}

28. implement comparision of 2 strings 
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

int main() {
    char str1[100], str2[100];
    int result;

    printf("Enter first string: ");
    scanf("%s", str1);

    printf("Enter second string: ");
    scanf("%s", str2);

    result = strcmp(str1, str2);

    if (result == 0) {
        printf("Both strings are equal\n");
    }
    else if (result > 0) {
        printf("First string is greater than second string\n");
    }
    else {
        printf("First string is smaller than second string\n");
    }

    printf("\nGetting MAC address:\n");
    system("getmac");

    return 0;
}

29. Linked list insertion in middle and deletion in middle 
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* next;
};

struct Node* createNode(int value) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = value;
    newNode->next = NULL;
    return newNode;
}

struct Node* insertEnd(struct Node* head, int value) {
    struct Node* newNode = createNode(value);
    if (head == NULL)
        return newNode;

    struct Node* temp = head;
    while (temp->next != NULL)
        temp = temp->next;

    temp->next = newNode;
    return head;
}

struct Node* insertMiddle(struct Node* head, int value, int pos) {
    struct Node* newNode = createNode(value);

    if (pos == 1) {
        newNode->next = head;
        return newNode;
    }

    struct Node* temp = head;
    for (int i = 1; i < pos - 1 && temp != NULL; i++)
        temp = temp->next;

    if (temp == NULL) {
        printf("Position out of range\n");
        free(newNode);
        return head;
    }

    newNode->next = temp->next;
    temp->next = newNode;
    return head;
}

struct Node* deleteMiddle(struct Node* head, int pos) {
    if (head == NULL) return NULL;

    if (pos == 1) {
        struct Node* temp = head;
        head = head->next;
        free(temp);
        return head;
    }

    struct Node* temp = head;
    for (int i = 1; i < pos - 1 && temp->next != NULL; i++)
        temp = temp->next;

    if (temp->next == NULL) {
        printf("Position out of range\n");
        return head;
    }

    struct Node* del = temp->next;
    temp->next = del->next;
    free(del);
    return head;
}

void traverse(struct Node* head) {
    struct Node* temp = head;
    printf("Linked List: ");
    while (temp != NULL) {
        printf("%d -> ", temp->data);
        temp = temp->next;
    }
    printf("NULL\n");
}

int main() {
    struct Node* head = NULL;
    int n, value, pos;

    printf("Enter number of nodes: ");
    scanf("%d", &n);

    for (int i = 0; i < n; i++) {
        printf("Enter value: ");
        scanf("%d", &value);
        head = insertEnd(head, value);
    }

    traverse(head);

    printf("Enter value to insert in middle: ");
    scanf("%d", &value);
    printf("Enter position: ");
    scanf("%d", &pos);

    head = insertMiddle(head, value, pos);
    traverse(head);

    printf("Enter position to delete from middle: ");
    scanf("%d", &pos);

    head = deleteMiddle(head, pos);
    traverse(head);

    printf("\nGetting MAC address:\n");
    system("getmac");

    return 0;
}


30. implement binary tree traversal 
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

struct Node* createNode(int value) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = value;
    newNode->left = NULL;
    newNode->right = NULL;
    return newNode;
}

void inorder(struct Node* root) {
    if (root != NULL) {
        inorder(root->left);
        printf("%d ", root->data);
        inorder(root->right);
    }
}

void preorder(struct Node* root) {
    if (root != NULL) {
        printf("%d ", root->data);
        preorder(root->left);
        preorder(root->right);
    }
}

void postorder(struct Node* root) {
    if (root != NULL) {
        postorder(root->left);
        postorder(root->right);
        printf("%d ", root->data);
    }
}

int main() {
    struct Node* root = createNode(10);
    root->left = createNode(20);
    root->right = createNode(30);
    root->left->left = createNode(40);
    root->left->right = createNode(50);

    printf("Inorder Traversal: ");
    inorder(root);

    printf("\nPreorder Traversal: ");
    preorder(root);

    printf("\nPostorder Traversal: ");
    postorder(root);

    printf("\n\nGetting MAC address:\n");
    system("getmac");

    return 0;
}



