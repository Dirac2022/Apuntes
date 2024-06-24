A multiway search tree of order m, or an m-way search tree, is a multiway tree in which
1. Each node has m children and $m – 1$ keys. *Or lees except for the root*
2. The keys in each node are in ascending order.
3. The keys in the first i children are smaller than the $i$th key.
4. The keys in the last $m – i$ children are larger than the $i$th key.

	A 4-way Tree
	![[4-way Tree.png]]

# Family of B-Trees

## B-Trees

A B-tree of order m is a multiway search tree with the following properties:
	1. The root has at least two subtrees unless it is a leaf.
	2. Each *non-root* and each *non-leaf* node holds $k – 1$ keys and $k$ references to subtrees where   $max[m/2] \leq k ≤ m$.
	3. Each leaf node holds $k – 1$ keys where $max[m/2] \leq k ≤ m$.
	4. All leaves are on the same level.1

According to these conditions, a B-tree is always at least half full, has few levels, and is
perfectly balanced.

![[Pasted image 20231214221007.png]]

![[Pasted image 20231214221917.png]]

### Searching in a B-Tree
An algorithm for finding a key in a B-tree is simple, and is coded as follows:
![[Pasted image 20231214222457.png]]

For $n$ keys in a $m$-order B-Tree the height $h$ satisfies the following inequality:
$$ h \leq log_q \dfrac{n+1}{2} + 1 $$
This means that for a sufficiently large order $m$, the height is small even for a large
number of keys stored in the B-tree. For example, if $m = 200$ and $n = 2,000,000$, then $h \leq 4$ 

### Inserting a Key into a B-Tree

### Deleting a Key from a B-Tree

## B*-Trees
A B*-tree is a variant of the B-tree. The number of keys in all *nonroot* nodes in a B-tree of order $m$ is now $k$ for $max[\dfrac{2m-1}{3}] \leq k \leq m-1$


## B$^+$-Trees
In a B-tree, references to data are made from any node of the tree, but in a B$^+$-tree,
these references are made only from the leaves. The internal nodes of a B$^+$-tree are indexes
for fast access of data; this part of the tree is called an index set. The leaves have a
different structure than other nodes of the B+-tree, and usually they are linked sequentially
to form a sequence set so that scanning this list of leaves results in data given in ascending
order. **A B$^+$-tree is a regular B-tree plus a linked list of data**

Figure 7.12 contains an example of a B$^+$-tree. Note that internal nodes store keys, references to other nodes, and a key count. Leaves store keys, references to records in a data file associated with the keys, and references to
the next leaf.

![[Pasted image 20231215000055.png]]

## Prefix B$^+$-Trees

![[Pasted image 20231215002545.png]]




# Tries

Traversing a binary tree was guided by full key comparisons; each node contained a key that was compared to another key to find a proper path through the tree. Prefix B-trees indicated that this is not necessary and that only a portion of a key is required to determine the path. **A tree that uses parts of the key to navigate the search is called a trie** (pronounced as "try").
Each key is a sequence of characters, and a trie is organized around these characters
rather than entire keys.

Figure 7.36 shows a trie for words that are indicated in the vertical rectangles, these rectangles represent the leaves of the trie, which are nodes with actual keys. The internal nodes can be viewed as arrays of references to subtries. At each level $i$, the position of the array that corresponds to the $i$th letter of the key being processed is checked. If the reference in this position is null, the key is not in the trie, which may mean a failure or a signal for key insertion. If not, we continue processing until a leaf containing this key is found.

![[Pasted image 20231215004222.png]]
For example, we check for the word “ERIE.”
At the first level of the trie, the reference corresponding to the first letter of this word, “E,” is checked. The reference is not null, so we go to the second level of the trie, to the child of the root accessible from position “E”; now the reference in the position indicated by the second letter, “R,” is tested. It is not null either, so we descend down the trie one more level. At the third level, the third letter, “I,” is used to access a reference in this node. The reference refers to a leaf containing the word “ERIE.” Thus, we conclude that the search is successful.

If the desired word was “ERIIE,” we would fail because we would access the same leaf as before, and obviously, the two words are different. 

If the word were “ERPIE,” we would access the same node with a leaf that contains “ERIE,” but this time “P” would be used to check the corresponding reference in the node. Because the reference is null, we would conclude that “ERPIE” is not in the trie.

