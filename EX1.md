
# Ex.No:1

# Ex.Name: Write the splitNode Module of B Tree in CPP.

## Date:
## Aim:
To implement the splitNode module in C++ for a B-Tree, which splits a full node into two nodes when inserting a new key, ensuring that the B-Tree properties are maintained.

## Algorithm:

STEP 1: Start the program.

STEP 2: Define a BTreeNode structure with members:

val[] → array to store keys

link[] → array of child pointers

count → current number of keys

STEP 3: Define constants:

MAX → maximum number of keys in a node

MIN → minimum number of keys in a node

STEP 4: Define the function splitNode with parameters:

void splitNode(int val, int *pval, int pos, BTreeNode *node, BTreeNode *child, BTreeNode **newNode)


where val is the new key to insert, pval returns the median key, pos is the position of insertion, node is the node to split, child is the child pointer, and newNode returns the newly created node after split.

STEP 5: Determine the median index:

if(pos > MIN)
    median = MIN + 1;
else
    median = MIN;


STEP 6: Allocate a new node (*newNode = new BTreeNode) to hold keys greater than the median.

STEP 7: Move keys and child pointers from the original node after the median to the new node. Update count of both nodes.

STEP 8: Insert the new key val into either the original node or the new node based on the position pos.

STEP 9: Set the median key (*pval = node->val[node->count]) to be pushed up to the parent.

STEP 10: Adjust child pointers and decrease the count of the original node to complete the split.



## Program:
```
void splitNode(int val, int *pval, int pos, BTreeNode *node, BTreeNode *child, BTreeNode **newNode) 
{
    int median,j;
    if(pos>MIN)
    median=MIN+1;
    else
    median=MIN;
    *newNode=new BTreeNode;
    j=median+1;
    while(j<=MAX)
    {
        (*newNode)->val[j-median]=node->val[j];
        (*newNode)->link[j-median]=node->link[j];
        j++;
    }
    node->count=median;
    (*newNode)->count=MAX-median;
    if(pos<=MIN)
    {
        insertKey(val,pos,node,child);
        
    }
    else
    {
        insertKey(val,pos-median,*newNode,child);
    }
    *pval=node->val[node->count];
    (*newNode)->link[0]=node->link[node->count];
    node->count--;
    
}
```


## Output:
<img width="1098" height="293" alt="{FBF0AD62-3046-407D-952D-6620AA971856}" src="https://github.com/user-attachments/assets/bd965bf1-12b7-42bf-a9fb-80277dec8717" />




## Result:
The splitNode function successfully splits a full node in a B-Tree into two nodes and pushes the median key up to the parent node. This ensures that the B-Tree remains balanced after insertion.
