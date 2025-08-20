    class Solution {
    public List<Integer> distanceK(TreeNode root, TreeNode target, int k) {
        List<Integer> res=new ArrayList<>();
        if(root==null){
            return res;
        }
        HashMap<TreeNode,TreeNode> parentmap=new HashMap<>();
        findParent(parentmap,root);
        Queue<TreeNode> q=new LinkedList<>();
        HashSet<TreeNode> visited =new HashSet<>();
        q.add(target);

        while(!q.isEmpty()){
            int size=q.size();
            for(int i=0;i<size;i++){
                TreeNode curr=q.poll();
                visited.add(curr);
                if(k==0){
                    res.add(curr.val);
                }
                if(parentmap.containsKey(curr) && !visited.contains(parentmap.get(curr))){
                    q.add(parentmap.get(curr));
                }
                if(curr.left!=null && !visited.contains(curr.left)){
                    q.add(curr.left);
                }
                if(curr.right!=null && !visited.contains(curr.right)){
                    q.add(curr.right);
                }
            }
            k--;
            if(k<0){
                break;
            }
        }
        return res;
    }
    static void findParent(HashMap<TreeNode,TreeNode> hm,TreeNode root){
        if(root==null){
            return;
        }
        if(root.left!=null){
            hm.put(root.left,root);
        }
         if(root.right!=null){
            hm.put(root.right,root);
        }
        findParent(hm,root.left);
        findParent(hm,root.right);
        return;

    }
}