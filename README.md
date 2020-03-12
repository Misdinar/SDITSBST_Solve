BSTNode* __bst__createNode(long long value) {
    BSTNode *newNode = (BSTNode*) malloc(sizeof(BSTNode));
    newNode->key = value;
    newNode->pos= 0;
    newNode->left = newNode->right = NULL;
    return newNode;
}
