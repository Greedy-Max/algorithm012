## N叉树的层序遍历

### 

class Solution {
    public List<List<Integer>> levelOrder(Node root) {
        
       List<List<Integer>> result = new ArrayList<>();

        if (root == null) {
            return result;
        }

        Queue<Node> queue = new LinkedList<>();

        queue.add(root);

        while (!queue.isEmpty()) {
            List<Integer> cur = new ArrayList<>();

            int size = queue.size();

            for (int i=0; i<size; i++) {
                Node node = queue.poll();
                cur.add(node.val);
                queue.addAll(node.children);
            }
            result.add(cur);
        }
        return result;

        
    }
}