# PEMBAHASAN SDITSBST
### Soal dapat dilihat dilink pada deskripsi

**Thomas Dwi A / 05111940000021**

Pada soal BSITSBST terdapat 2 tugas yaitu, memasukkan nilai dengan konsep _Binary Search Tree_ dan mencari posisi urutan dari nilai yang dicari

#### Input Nilai 
```
   BSTNode* __bst__createNode(long long value) 
    
    {
    BSTNode *newNode = (BSTNode*) malloc(sizeof(BSTNode));
    newNode->key = value;
    newNode->pos= 0;
    newNode->left = newNode->right = NULL;
    return newNode;
}

BSTNode* __bst__insert(BSTNode *root, long long value)
    {
    BSTNode *temp = NULL;
    
	if (root == NULL) 
    {
    	temp = __bst__createNode(value);
        return temp;	
	}

    if (value < root->key)
    {
        root->left = __bst__insert(root->left, value);
	}
    else if (value > root->key)
    {
    	root->pos++;
        root->right = __bst__insert(root->right, value);
	}
    
    return root;
 
```
   ### PENJELASAN
Nilai akan dimasukkan kedalam BST dengan memperhatikan besaran nilai yang akan dimasukkan. Jika nilai yang akan dimasukkan kedalam BST yang masih kosong, maka cukup dengan membuat node. Jika memasukkan nilai ke BST yang telah diisi maka,
- subtree kiri dari sebuah node hanya berisi node dengan key **LEBIH KECIL** dari Key Node
- subtree kanan dari sebuah node hanya berisi node dengan key **LEBIH BESAR** dari Key Node

`newNode->pos` bertujuan untun menyimpan jumlah node subtree/leaf kanan

#### Mencari Posisi dari Nilai
```
long long bst_post(BSTNode *bst, long long value) {
    BSTNode *temp = bst;
    if (temp == NULL)
        return -1;
    if( temp->key > value)
    {
    	long long index = bst_post(temp->left, value);
    	if(index == -1) return -1;
    	else return index + temp->pos +1;
	} else if (temp->key<value)
	{
		return bst_post(temp->right, value);
	}
    else
    {
    	printf("pos :%lld\n",temp->pos);
        return temp->pos;
	}
}
```
`return -1` menunjukkan data di node tidak ada. Konsep mencari nilai mirip dengan cara menginput nilai ke node. `index + temp->pos +1` dan di tambah 1 saat mencetak nilai karena nilai temp->pos selalu dimulai dari 0;

rumus diatas merupakan cara menghitung posisi dari nilai yang dicari. Berikut ini gambaran sederhana cara mencari posisi nilai 80
```
penggambaran temp->pos

                      100    node 100 punya 1 node kanan
                      / \
                    74  152  node 74 punya 2 node kanan
                   /  \
                 21    80    node 21 punya 1 node kanan , node 80 punya 1 node kanan
                   \     \
                    33    82 node 33 punya 0 node kanan
```
maka dengan fungsi rekursif, untuk menentukan posisi 80 

temp->pos(80) = 1

index(100) = 1 

posisi 80 = nilai return di 100 + 1 = (index(100) + temp->pos(100) + 1) +1
          =(1 + 1 + 1) + 1 = 4
