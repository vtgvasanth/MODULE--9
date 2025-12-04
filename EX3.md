# Ex.No:3

# Ex.Name: Write the InsertInternal Module of the BPlus Tree in CPP

## Date:
## Aim:
To implement the insertInternal function of a B+ Tree in C++ that inserts a key into an internal node. If the internal node overflows, it splits the node and propagates the median key upward, maintaining the properties of a B+ Tree.


## Algorithm:
STEP 1: Start the program.

STEP 2: Define a Node structure with members:

key[] → array of keys in the node

ptr[] → array of child pointers

size → current number of keys

IS_LEAF → boolean flag indicating leaf node

STEP 3: Check if the internal node cursor has space (cursor->size < MAX).

STEP 4: If space is available:

Find the correct position i to insert the key x.

Shift existing keys and pointers to make space.

Insert the key x at position i and update cursor->size.

Set cursor->ptr[i+1] = child.

STEP 5: If the internal node is full (cursor->size == MAX):

Create a new internal node newInternal.

Create temporary arrays virtualKey[] and virtualPtr[] to hold keys and pointers including the new key and child.

Insert x and child into the temporary arrays at the correct position.

Split the node:

cursor keeps the first half of keys/pointers

newInternal keeps the second half

Set newInternal->IS_LEAF = false and update sizes.

STEP 6: If cursor is the root:

Create a new root node.

Place the median key at the root.

Set root->ptr[0] = cursor and root->ptr[1] = newInternal.

STEP 7: If cursor is not root, recursively call insertInternal on the parent node with the median key and the new internal node.

STEP 8: End the function.

STEP 9: Ensure all keys in internal nodes remain sorted.

STEP 10: Maintain B+ Tree properties after insertion.




## Program:
```
void BPTree::insertInternal(int x, Node *cursor, Node *child)
{
    if (cursor->size < MAX)
    {
        int i = 0;
        while (x > cursor->key[i] && i < cursor->size)
            i++;
        for (int j = cursor->size; j > i; j--)
        {
            cursor->key[j] = cursor->key[j - 1];
        }
        for (int j = cursor->size + 1; j > i + 1; j--)
        {
            cursor->ptr[j] = cursor->ptr[j - 1];
        }
        cursor->key[i] = x;
        cursor->size++;
        cursor->ptr[i + 1] = child;
    }
    else
    {
        Node *newInternal = new Node;
        int virtualKey[MAX + 1];
        Node *virtualPtr[MAX + 2];
        for (int i = 0; i < MAX; i++) 
        {
          virtualKey[i] = cursor->key[i];
        }
        for (int i = 0; i < MAX + 1; i++) 
        {
            virtualPtr[i] = cursor->ptr[i];
        }
        int i = 0, j;
        while (x > virtualKey[i] && i < MAX)
            i++;
        for (int j = MAX + 1; j > i; j--) 
        {
            virtualKey[j] = virtualKey[j - 1];
        }
        virtualKey[i] = x;
        for (int j = MAX + 2; j > i + 1; j--)
        {
            virtualPtr[j] = virtualPtr[j - 1];
        }
        virtualPtr[i + 1] = child;
        newInternal->IS_LEAF = false;
        cursor->size = (MAX + 1) / 2;
        newInternal->size = MAX - (MAX + 1) / 2;
        for (i = 0, j = cursor->size + 1; i < newInternal->size; i++, j++)
        {
            newInternal->key[i] = virtualKey[j];
        }
        for (i = 0, j = cursor->size + 1; i < newInternal->size + 1; i++, j++)
        {
            newInternal->ptr[i] = virtualPtr[j];
        }
        if (cursor == root)
        {
            Node *newRoot = new Node;
            newRoot->key[0] = cursor->key[cursor->size];
            newRoot->ptr[0] = cursor;
            newRoot->ptr[1] = newInternal;
            newRoot->IS_LEAF = false;
            newRoot->size = 1;
            root = newRoot;
        }
        else
        {
            insertInternal(cursor->key[cursor->size], findParent(root, cursor), newInternal);
        }
    }
}
```


## Output:
<img width="938" height="647" alt="{5BE91052-E4F7-494B-B573-8BB8C83E966D}" src="https://github.com/user-attachments/assets/a096a2aa-8bc8-45d7-b1fd-c13948585121" />



 ## Result:
The insertInternal function successfully inserts a key into an internal node of a B+ Tree. If the node overflows, it splits the node and propagates the median key upward. After multiple insertions:

All internal nodes have at most MAX keys.

All leaf nodes remain at the same depth.

The tree remains balanced.
