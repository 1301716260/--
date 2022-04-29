##### AVL模板

```C++
#include<bits/stdc++.h>
using namespace std;

#include<bits/stdc++.h>
using namespace std;

struct node{
    int val;
    node *lchild, *rchild;
    node(int v, node* l, node *r): val(v), lchild(l), rchil (r) {}
};


node* rotateLeft(node* root){
    node* t = root->rchild;
    root->rchild = t->lchild;
    t->lchild = root;
    return t;
}

node* rotateRight(node* root){
    node* t = root->lchild;
    root->lchild = t->rchild;
    t->rchild=root;
    return t;
}

node* rotateLeftRight(node* root){
    root->lchild = rotateLeft(root->lchild);
    return rotateRight(root);
}

node* rotateRightLeft(node* root){
    root->rchild = rotateRight(root->rchild);
    return rotateLeft(root);
}

int getHeight(node* root){
    if(root == NULL) return 0;
    return max(getHeight(root->lchild), getHeight(root->rchild)) + 1;
}

node* insert(node* root, int val){
    if(root == NULL){
        root = new node(val, NULL, NULL);
    }else if(val < root->val){ //这里不是root->lchild->val;
        root->lchild = insert(root->lchild, val);
        //判断插入节点后是否还平衡
        if(getHeight(root->lchild) - getHeight(root->rchild)    == 2){
            root = val < root->lchild->val ? rotateRigh (root) : rotateLeftRight(root);
        }
    }else{
        root->rchild = insert(root->rchild, val);
        //判断插入节点后是否还平衡
        if(getHeight(root->lchild) - getHeight(root->rchild) == -2){
            root = val > root->rchild->val ? rotateLeft(root) : rotateRightLeft(root);
        }
    }
    return root; // 注意返回的位置 不要放到if判断作用域内
}

int main(){
    int n, val;
    cin >> n;
    node* root = NULL;
    for(int i = 0; i < n; i++){
        cin >> val;
        root = insert(root, val);
    }
    printf("%d", root->val);
    return 0;
}
```

###### LL型(右旋)

![20220429195506](https://cdn.jsdelivr.net/gh/1301716260/notes@main/pictures/20220429195506.png)

###### RR型(左旋）

![20220429195636](https://cdn.jsdelivr.net/gh/1301716260/notes@main/pictures/20220429195636.png)

###### LR型(先左旋，再右旋)

![20220429195723](https://cdn.jsdelivr.net/gh/1301716260/notes@main/pictures/20220429195723.png)

###### LR型(先左旋，再右旋)

![20220429195753](https://cdn.jsdelivr.net/gh/1301716260/notes@main/pictures/20220429195753.png)