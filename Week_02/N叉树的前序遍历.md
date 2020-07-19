## N叉树的前序遍历

### 方法一

class Solution {
    public List<Integer> preorder(Node root) {
        LinkedList<Node> stack = new LinkedList<>();
        LinkedList<Integer> res = new LinkedList<>();

        if (root == null) return res;

        stack.add(root);

        while (!stack.isEmpty()) {
            Node node = stack.pollLast();

            res.add(node.val);
            Collections.reverse(node.children);

            for (Node item : node.children) {
                if (item != null) {
                    stack.add(item);
                }
            }
        }
        return res;
    }
    
}

### 方法二


import java.util.ArrayList;
import java.util.List;

class Solution {
    public List<Integer> preorder(Node root) {
        List<Integer> result = new ArrayList<>();

        if (root == null) {
            return result;
        }

        helper(root, result);

        return  result;
    }

    private void helper(Node node, List<Integer> res) {
        if (node == null) {
            return;
        }
        res.add(node.val);
        for (Node item : node.children) {
            if (item != null) {
                helper(item, res);
            }
        }
    }
}