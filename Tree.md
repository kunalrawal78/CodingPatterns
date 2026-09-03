
-------Category-------
1.Traversal
2.Mirror/Symmetric
3.Search
4.Validation
5.Path sum
6.Construction Tree with given things
------------------------
1. PreOrder (N L R)--> Using Recursion and While loop with Stack
2. InOrder (L N R)--->Using Recursion and While loop with Stack
3. PostOrder (R L N) -- reverse of PreOrder --> Using Recursion and While loop with 2 Stack
-----------------------
1. void h(TreeNode root, List<Integer> ans) {
    if (root == null) return;
    ans.add(root.val);
    h(root.left, ans);
    h(root.right, ans);
}
void helper(TreeNode root, List<Integer> ans) {
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
---
2.void h(TreeNode root, List<Integer> ans) {
    if (root == null) return;
    h(root.left, ans);
    ans.add(root.val);
    h(root.right, ans);
}
void helper(TreeNode root, List<Integer> ans) {
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
---
3.void h(TreeNode root, List<Integer> ans) {
    if (root == null) return;
    h(root.left, ans);
    h(root.right, ans);
    ans.add(root.val);
}
---2 stack solution---
void helper(TreeNode root, List<Integer> ans) {
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
--- 1 stack solution-----

void helper(TreeNode root, List<Integer> ans) {
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
------------------------
3. Level Order Traversal

public List<List<Integer>> levelOrder(TreeNode root) {
        if(root==null)return Collections.emptyList();
        Queue<TreeNode>q=new LinkedList<>();
        List<List<Integer>>ans=new ArrayList<>();
        q.add(root);
        while(!q.isEmpty()){
            int t=q.size();
            List<Integer>l=new ArrayList<>();
            while(t>0){
                TreeNode p=q.poll();
                if(p.left!=null){
                    q.add(p.left);
                }
                if(p.right!=null){
                    q.add(p.right);
                }
                l.add(p.val);
                t--;
            }
            ans.add(l);
        }
        return ans;
    }






