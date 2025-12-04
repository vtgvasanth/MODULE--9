
# Ex.No:2

# Ex.Name: Write the findMin module of the B tree in CPP.

## Date:

## Aim:
To implement a C++ function findMin that finds and displays the minimum key in a B-Tree.


## Algorithm:
STEP 1: Start the program.

STEP 2: Define a BTreeNode structure with members:

val[] → array of keys in the node

link[] → array of child pointers

count → number of keys in the node

STEP 3: Pass the root node of the B-Tree to the function findMin(BTreeNode *myNode).

STEP 4: Create a temporary pointer curr and set it to myNode.

STEP 5: Traverse down the leftmost child of the tree using:

while(curr->link[0] != NULL)
    curr = curr->link[0];


Since in a B-Tree the smallest key is always in the leftmost leaf.

STEP 6: Once the leftmost node is reached, the minimum key is the first key in the node (curr->val[1] assuming 1-based indexing).

STEP 7: Display the minimum key.

STEP 8: End the function.




## Program:
```
void findMin(BTreeNode *myNode)
{
    BTreeNode *curr = myNode;
    while(curr->link[0]!=NULL)
    {
        curr = curr->link[0];
    }
    cout<<endl<<"Min="<<curr->val[1];
    
}
```


## Output:
<img width="1073" height="310" alt="{4B35C716-4E1B-49C7-82B8-70C4DF768CE6}" src="https://github.com/user-attachments/assets/ac33d62e-fe80-4d2f-a407-a2f34b38a745" />



##  Result:
The function successfully finds and displays the minimum key of the B-Tree.
