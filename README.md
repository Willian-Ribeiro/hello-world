# Questions & Answers

1	Upload your code, diagrams and any other relevant materials to a Git repository and send me its URL, there are many free Git options you can explore;

Pelase check "1st Solution" file.

-----------------------------------------------#~#~#~#~#-----------------------------------------------------------------------

2	What is the O() complexity of your solution?

The following recursive alghorithm can be analyzed as a binary tree, where for each time the recursive function is called, 2 calls for the same recursive function will be made (exception for the case where the node is a leaf).

To analyse its complexity, let's suppose a tree of depth 3. (see image "2 recursive calls"). In the worst case, all nodes until depth 3 will have sub-nodes, what causes the function to call itself twice (once for the left and once for the right sub-node).

Therefore, the number of calls of the function will be equals to the number of branches in the tree. In this case, 15 branches where created. By induction, one can notice that the formula is given by 2^(x+1)-1, where x is the depth of the tree. It is easy to see that the number of branches is exactly same as the amount of input nodes. Thus, for each node, the function is called once, resulting in a function f(n) = n + c.

Since this function is not only calling itself, but also maxValue and minValue. The cost of calling maxValue and minValue for each node in the tree is 2*(log2(nodes+1)-2). Cost of minValue and maxValues, see image "auxiliary recursive functions", is given below:

nodes  = 2^(depth+1)-1
nodes + 1 = 2 ^ (altura + 1)
log2(nodes+1) = depth + 1
depth = log2(depth+1) - 1

function calls = depth - 1 = log2(nodes+1) - 2



Therefore, the function that best describes the "cost" of checkBST is f(n) = c1*(n+c2)*(c3*log2(n+1)+c4) + c5. In big O: f(n) = O(n*log2(n)).



bool checkBST(Node* root)
    {	
        
        if( (root->left == NULL) && (root->right == NULL)) return true; ~~~~~> c
        bool l = checkBST(root->left); ~~~~~> n + c
        bool r = checkBST(root->right); ~~~~~> n + c
        
        if( (l && r) != true ) return false; ~~~~~> c
        
        int maxLV = maxValue(root->left); ~~~~~> log2(n) + c
        int minRV = minValue(root->right); ~~~~~> log2(n) + c
        if( (maxLV < root->data) && (root->data < minRV) ) return true; ~~~~~> c
        else return false; ~~~~~> c
	}

    int maxValue(Node* root) ~~~~~> log2(n) + c
    {
        if(root->right == NULL) return root->data;  ~~~~~> c
        return maxValue(root->right); ~~~~~> log2(n)
    }

    int minValue(Node* root) ~~~~~> log2(n) + c
    {
        if(root->left == NULL) return root->data; ~~~~~> c
        return minValue(root->left); ~~~~~> log2(n)
    }

-----------------------------------------------#~#~#~#~#-----------------------------------------------------------------------

3	How can you improve your existing solution? If that is possible, what would your new solution's O() complexity be?

It is possible to do the data comparison and obtain the minimum and maximum value at the same time, saving the use of other recursive function.

Two attempts were made in order to reduce the complexity, check "More Efficient Function" and "better yet function".

The function in "More Efficient Function" is a O(n), because the recursive functions minValue and maxValue used in the exercise above are not needed.

The function in "better yet function" is also O(n), but should be slightly better than the function in "More Efficient Function" because the code is more consize.

-----------------------------------------------#~#~#~#~#-----------------------------------------------------------------------

4	What is the complexity class  (P, NP, NP-complete, etc) of this problem?

	By the functions found in the previous exercise, the problem is of complexity class P.

-----------------------------------------------#~#~#~#~#-----------------------------------------------------------------------

5	Provide us a diagram containing the state machine automata of your algorithm;

Please check "" file.

-----------------------------------------------#~#~#~#~#-----------------------------------------------------------------------

6	Bonus point: Provide us the abstract syntax tree (AST) representation of your algorithm;

