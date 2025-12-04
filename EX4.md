# Ex.No:4

# Ex.Name: Write the fixup module of the red black tree in CPP.

## Date:

## Aim:
To implement the fixup function in C++ for a Red-Black Tree that restores Red-Black Tree properties after insertion by performing recoloring and rotations.

## Algorithm:
STEP 1: Start the program.

STEP 2: Define a node structure with members:

data → value of the node

c → color (0 = RED, 1 = BLACK)

l → pointer to left child

r → pointer to right child

p → pointer to parent

STEP 3: Pass the root node and the newly inserted node pt to the fixup function.

STEP 4: While pt is not root, and pt is RED, and its parent is RED:

STEP 5: Determine parent_pt and grand_parent_pt.

STEP 6: Case A: Parent is left child of grandparent:

Set uncle_pt = grand_parent_pt->r.

Case 1: If uncle_pt is RED → recolor:

Grandparent → RED

Parent & Uncle → BLACK

Move pt = grand_parent_pt

Case 2: If pt is right child → left rotation on parent, then Case 3.

Case 3: pt is left child → right rotation on grandparent, swap colors of parent & grandparent, move pt = parent_pt.

STEP 7: Case B: Parent is right child of grandparent (mirror of Case A):

Set uncle_pt = grand_parent_pt->l.

Case 1: If uncle_pt is RED → recolor.

Case 2: If pt is left child → right rotation on parent, then Case 3.

Case 3: pt is right child → left rotation on grandparent, swap colors, move pt = parent_pt.

STEP 8: Repeat steps 4–7 until tree properties are restored.

STEP 9: Ensure the root is always BLACK: root->c = 0.

STEP 10: End the function.




## Program:
```
void fixup(node* root, node* pt)
{
    node* parent_pt = NULL;
    node* grand_parent_pt = NULL;
 
    while ((pt != root) && (pt->c != 0) && (pt->p->c == 1))
    {
        parent_pt = pt->p;
        grand_parent_pt = pt->p->p;
        /*  Case : A Parent of pt is left child of Grand-parent of pt */
        if (parent_pt == grand_parent_pt->l)
        {
            node* uncle_pt = grand_parent_pt->r;
            /* Case : 1 The uncle of pt is also red Only Recoloring required */
            if (uncle_pt != NULL && uncle_pt->c == 1)
            {
                grand_parent_pt->c = 1;
                parent_pt->c = 0;
                uncle_pt->c = 0;
                pt = grand_parent_pt;
            }
            else
            {
                /* Case : 2 pt is right child of its parent Left-rotation required */
                if (pt == parent_pt->r) 
                {
                    leftrotate(parent_pt);
                    pt = parent_pt;
                    parent_pt = pt->p;
                }
                /* Case : 3 pt is left child of its parent Right-rotation required */
                rightrotate(grand_parent_pt);
                int t = parent_pt->c;
                parent_pt->c = grand_parent_pt->c;
                grand_parent_pt->c = t;
                pt = parent_pt;
            }
        }
        /* Case : B Parent of pt is right child of Grand-parent of pt */
        else 
        {
            node* uncle_pt = grand_parent_pt->l;
            /*  Case : 1 The uncle of pt is also red Only Recoloring required */
            if ((uncle_pt != NULL) && (uncle_pt->c == 1))
            {
                grand_parent_pt->c = 1;
                parent_pt->c = 0;
                uncle_pt->c = 0;
                pt = grand_parent_pt;
            }
            else 
            {
                /* Case : 2 pt is left child of its parent Right-rotation required */
                if (pt == parent_pt->l) 
                {
                    rightrotate(parent_pt);
                    pt = parent_pt;
                    parent_pt = pt->p;
                }
                /* Case : 3 pt is right child of its parent Left-rotation required */
                leftrotate(grand_parent_pt);
                int t = parent_pt->c;
                parent_pt->c = grand_parent_pt->c;
                grand_parent_pt->c = t;
                pt = parent_pt;
            }
        }
    }
    root->c = 0;
}
```


## Output:
<img width="1185" height="495" alt="{F73C9F40-C47F-456E-A13F-9F310BD35FBF}" src="https://github.com/user-attachments/assets/28b42ddc-6922-4530-b383-2192bd609377" />



## Result:
The fixup function restores Red-Black Tree properties after insertion:

No two consecutive red nodes exist.

All paths from root to leaves have the same number of black nodes.

Tree remains balanced for logarithmic search, insertion, and deletion.
