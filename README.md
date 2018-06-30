# Questions & Answers

1	Upload your code, diagrams and any other relevant materials to a Git repository and send me its URL, there are many free Git options you can explore;

2	What is the O() complexity of your solution?

The following recursive alghorithm can be analyzed as a binary tree, where for each time the recursive function is called, 2 calls for the same recursive function will be made (exception for the case where the node is a leaf).

To analyse its complexity, let's suppose a tree of depth 3. (see image "2 recursive calls"). In the worst case, all nodes until depth 3 will have sub-nodes, what causes the function to call itself twice. Therefore, the number of calls of the function will be equals to the number of branches in the tree. In this case, 15 branches where created. By induction, one can notice that the formula is given by 2^n-1, where n is the depth of the tree.

Since this function is not only calling itself as a recursive function, but also maxValue and minValue, we should supose that for each time the recursive function checkBST is called, maxValue and minValue are called n times (see image "auxiliary recursive functions").

Therefore, the function that best describes the "cost" of checkBST is f(n) = c1*n*(2^n) + c2. In big O: f(n) = O(n*(2^n)).



bool checkBST(Node* root)
    {	
        
        if( (root->left == NULL) && (root->right == NULL)) return true; ~~~~~> c
        bool l = checkBST(root->left); ~~~~~> 2^n-1 + c
        bool r = checkBST(root->right); ~~~~~> 2^n-1 + c
        
        if( (l && r) != true ) return false; ~~~~~> c
        
        int maxLV = maxValue(root->left); ~~~~~> n + c
        int minRV = minValue(root->right); ~~~~~> n + c
        if( (maxLV < root->data) && (root->data < minRV) ) return true; ~~~~~> c
        else return false; ~~~~~> c
	}

    int maxValue(Node* root) ~~~~~> n + c
    {
        if(root->right == NULL) return root->data;  ~~~~~> c
        return maxValue(root->right); ~~~~~> n
    }

    int minValue(Node* root) ~~~~~> n + c
    {
        if(root->left == NULL) return root->data; ~~~~~> c
        return minValue(root->left); ~~~~~> n
    }


3	How can you improve your existing solution? If that is possible, what would your new solution's O() complexity be?
It is possible to do the data comparison and obtain the minimum and maximum value at the same time, saving the use of other recursive function.

The new complexity would be f(n) = O(2^n).



4	What is the complexity class  (P, NP, NP-complete, etc) of this problem?




5	Provide us a diagram containing the state machine automata of your algorithm;





6	Bonus point: Provide us the abstract syntax tree (AST) representation of your algorithm;

