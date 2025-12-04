# Ex.No:5

# Ex.Name: Write the right rotate module of splay tree in CPP.

## Date:

## Aim:
To implement the right rotation function in a Splay Tree in C++, which rotates a given node to the right to maintain the splay tree properties during insertion, deletion, or splaying.


## Algorithm:
STEP 1: Start the program.

STEP 2: Define a node structure with members:

data → value of the node

left → pointer to left child

right → pointer to right child

STEP 3: Pass a node x to the rightRotate function.

STEP 4: Store the left child of x in a temporary pointer y → y = x->left.

STEP 5: Make x->left point to y->right.

STEP 6: Make y->right point to x.

STEP 7: Return y as the new root of the rotated subtree.

STEP 8: End the function.




## Program:
```
node *rightRotate(struct node *x)
{
    node *y = x->left;
    x->left = y->right;
    y->right = x;
    return y;
}
```


## Output:
<img width="1173" height="635" alt="{B3C11536-1C90-4257-8670-B0B52BCF6F49}" src="https://github.com/user-attachments/assets/c8be7eac-2cbd-4bdd-bec4-44cabffbd0a5" />




## Result:
The rightRotate function rotates a subtree rooted at node x to the right.
