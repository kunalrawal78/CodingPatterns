# Binary Tree --- Traversal Notes

## Categories of Binary Tree Problems

1.  Traversal
2.  Mirror / Symmetric
3.  Search
4.  Validation
5.  Path Sum
6.  Tree Construction (from given information)

------------------------------------------------------------------------

## 1. Depth-First Traversals

### 1.1 Preorder Traversal --- Node, Left, Right (NLR)

**Order:** Visit the current node, then the left subtree, then the right
subtree.

#### Recursive Approach

``` java
void preorder(TreeNode root, List<Integer> ans) {
    if (root == null) return;

    ans.add(root.val);
    preorder(root.left, ans);
    preorder(root.right, ans);
}
```

#### Iterative Approach --- One Stack

Push the right child before the left child so that the left child is
processed first.

``` java
void preorder(TreeNode root, List<Integer> ans) {
    if (root == null) return;

    Stack<TreeNode> st = new Stack<>();
    st.push(root);

    while (!st.isEmpty()) {
        TreeNode node = st.pop();
        ans.add(node.val);

        if (node.right != null) st.push(node.right);
        if (node.left != null) st.push(node.left);
    }
}
```

------------------------------------------------------------------------

### 1.2 Inorder Traversal --- Left, Node, Right (LNR)

**Order:** Visit the left subtree, then the current node, then the right
subtree.

#### Recursive Approach

``` java
void inorder(TreeNode root, List<Integer> ans) {
    if (root == null) return;

    inorder(root.left, ans);
    ans.add(root.val);
    inorder(root.right, ans);
}
```

#### Iterative Approach --- One Stack

``` java
void inorder(TreeNode root, List<Integer> ans) {
    Stack<TreeNode> st = new Stack<>();
    TreeNode curr = root;

    while (curr != null || !st.isEmpty()) {
        while (curr != null) {
            st.push(curr);
            curr = curr.left;
        }

        curr = st.pop();
        ans.add(curr.val);
        curr = curr.right;
    }
}
```

------------------------------------------------------------------------

### 1.3 Postorder Traversal --- Left, Right, Node (LRN)

**Order:** Visit the left subtree, then the right subtree, then the
current node.

> Note: Postorder is **LRN**. It can be obtained by reversing the result
> of the **NRL** order (Node, Right, Left), not by reversing ordinary
> preorder (NLR).

#### Recursive Approach

``` java
void postorder(TreeNode root, List<Integer> ans) {
    if (root == null) return;

    postorder(root.left, ans);
    postorder(root.right, ans);
    ans.add(root.val);
}
```

#### Iterative Approach --- Two Stacks

``` java
void postorder(TreeNode root, List<Integer> ans) {
    if (root == null) return;

    Stack<TreeNode> st1 = new Stack<>();
    Stack<TreeNode> st2 = new Stack<>();

    st1.push(root);

    while (!st1.isEmpty()) {
        TreeNode node = st1.pop();
        st2.push(node);

        if (node.left != null) st1.push(node.left);
        if (node.right != null) st1.push(node.right);
    }

    while (!st2.isEmpty()) {
        ans.add(st2.pop().val);
    }
}
```

#### Iterative Approach --- One Stack

Use `lastVisited` to determine whether the right subtree has already
been processed.

``` java
void postorder(TreeNode root, List<Integer> ans) {
    if (root == null) return;

    Stack<TreeNode> st = new Stack<>();
    TreeNode curr = root;
    TreeNode lastVisited = null;

    while (curr != null || !st.isEmpty()) {
        if (curr != null) {
            st.push(curr);
            curr = curr.left;
        } else {
            TreeNode peekNode = st.peek();

            if (peekNode.right != null && lastVisited != peekNode.right) {
                curr = peekNode.right;
            } else {
                ans.add(peekNode.val);
                lastVisited = st.pop();
            }
        }
    }
}
```

------------------------------------------------------------------------

## 2. Breadth-First Traversal

### 2.1 Level Order Traversal

**Idea:** Use a queue to process nodes level by level.

At the start of each outer-loop iteration, store `q.size()`. This
captures the number of nodes in the current level, allowing that level
to be processed separately.

``` java
public List<List<Integer>> levelOrder(TreeNode root) {
    if (root == null) return Collections.emptyList();

    Queue<TreeNode> q = new LinkedList<>();
    List<List<Integer>> ans = new ArrayList<>();

    q.add(root);

    while (!q.isEmpty()) {
        int t = q.size();
        List<Integer> level = new ArrayList<>();

        while (t > 0) {
            TreeNode node = q.poll();

            if (node.left != null) {
                q.add(node.left);
            }

            if (node.right != null) {
                q.add(node.right);
            }

            level.add(node.val);
            t--;
        }

        ans.add(level);
    }

    return ans;
}
```

------------------------------------------------------------------------

## 3. Quick Revision

  Traversal     Visit order           Common iterative data structure
  ------------- --------------------- ---------------------------------
  Preorder      Node → Left → Right   One stack
  Inorder       Left → Node → Right   One stack
  Postorder     Left → Right → Node   Two stacks or one stack
  Level order   Level by level        Queue

### Complexity

For all four traversals:

-   **Time Complexity:** `O(n)` --- each node is visited once.
-   **Auxiliary Space:**
    -   DFS iterative approaches: up to `O(h)` for stack-based traversal
        in typical implementations; the two-stack postorder approach can
        use `O(n)`.
    -   Level order: up to `O(w)` for the queue, where `w` is the
        maximum width of the tree.
    -   Recursive DFS: up to `O(h)` call-stack space.

Here, `n` is the number of nodes, `h` is the tree height, and `w` is the
maximum width.
