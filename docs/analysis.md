# Lab 23 Analysis — AVL Trees and Splay Trees

## Required Analysis

1. Explain why an AVL tree maintains `O(log n)` height. 
An AVL tree makes sure that the heights of the two subtrees of a node are within one of each other to make sure they aren't too skewed. By doing this, even though the nodes per level grow exponentially, the tree itself stays short with a height of O(log n).
2. Identify the four AVL imbalance cases:
   - LL: This means that the left subtree of the left child is too tall. It should be fixed with one right rotation.
   - RR: This means that the right subtree of the right child is too tall. It should be fixed with one left rotation.
   - LR: This means that the right subtree of the left child is too tall. It should be fixed with a right rotation on the child, and then a left rotation on the parent.
   - RL: This means that the left subtree of the right child is too tall. It should be fixed with a left rotation on the child, and then a right rotation on the parent.
3. Explain how insertion and deletion differ in their rebalancing behavior.
Both operations start from the root and will rebalance the tree once the operation is finished. For insertion, the rotation can usually restore the previous height of the tree, meaning that some elements such as the higher ancestors do not need any more rotations. Deletion, on the other hand, may reduce the height of the subtree, so rebalancing may be needed from ancestors all the way to the root.
4. Explain why each AVL `find`, `insert`, and `erase` operation is `O(log n)`.
All of the above operations follows a single path from root to leaf. Since the height of an AVL is O(log n), that means that the path also has O(log n) nodes. Since the rebalancing process takes a constant amount of operations, insertion and deletion also take O(log n). The AVL tree stores a total of O(n) nodes, and recursive calls may use up to O(log n) space.
5. Explain the purpose of a splay operation.
The purpose of a splay operation is so that an accessed node can be moved to the root via rotation. By using splaying, it has a similar effect to caching where the recently accessed nodes are quicker to reach again, and the tree can adjust to the pattern without having to store balance information or a height.
6. Describe:
   - zig: The accessed node's parent is the root. One rotation is required.
   - zig-zig: The accessed node is a left child, and the parent of the accessed node is also a left child. The grandparent must be rotated, and then the parent (both in the same direction). The same thing occurs when the accessed node is a right child and the parent of the accessed node is also a right child.
   - zig-zag: The accessed node and its parent are on opposite sides (right/left, left/right). To solve this, one must rotate the parent, and then the grandparent (in opposite directions).
7. Explain why a single splay operation can take `O(n)` in the worst case even though splay trees provide logarithmic amortized performance.
A single splay operation can take O(n) in the worst case because a splay tree can become a chain of n nodes. If one were to access the node at the very end of that chain, it may require O(n) rotations in order to bring it to the root. However, the reason the amortized time complexity per operation is O(log n) is because throughout the whole sequence of operations that occur, the rotations also improve the shape of the tree for later access, going back to our idea of caching.
8. Compare AVL and splay trees for:
   - guaranteed height
   AVL: O(log n)
   Splay: Has a chance of being O(n) since there is no guarantee for logarithmic height
   - amortized access cost
   AVL: The worst case per operation is O(log n)
   Splay: The amortized time complexity is O(log n), but the worst time may be O(n). Refer to Question 7.
   - repeated access to hot keys
   AVL: Does not move the key but is still efficient.
   Splay: Splaying moves the key to the root, caching to make repeated access very fast.
   - update overhead
   AVL: Updates the heights and maintains balance by rotating some parts of the tree
   Splay: Splays nodes (inserted, removed, accessed) by performing rotations
   - memory metadata
   AVL: Stores height
   Splay: Stores parent pointer (no balance field or height)
9. Construct an access sequence where a splay tree benefits substantially from locality of reference.
Let keys 1,2,3,....,n be inserted into a splay tree. Since the newest maximum is splayed to the root, it makes the smaller keys become a long chain. If you were to access key 1, the first access may require O(n) time, but because it splays key 1 to the root, the repeated access of key 1 after results in O(1) time per access of the key.
10. Explain why a splay tree cannot be described as having `O(log n)` worst-case time for every individual operation.
Since the O(log n) time is amortized, that means that the bound is the average cost over multiple operations. If the tree is highly skewed, it can still take O(n) time. However, splay trees are good because they improve the tree by restructuring it for future calls of operations. It does not guarantee that every individual operation will be O(log n).

## Expected Complexity

AVL:
- search: O(log n)
- insertion: O(log n)
- deletion: O(log n)
- space: O(n)

Splay:
- individual operation: O(n) worst case
- amortized operation: O(log n)
- space: O(n)
