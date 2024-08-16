## 450. Delete Node
I think the difference between a binary tree and a binary search tree is that the search tree is organized.

This problem fucked me up and makes no sense. I looked it up and was validated. Listened to the explanation and still don't undertand but it has something to do with recursively replacing and deleting child nodes of the initial node we deleted.

    def deleteNode(self, root: Optional[TreeNode], key: int) -> Optional[TreeNode]:
        if not root:
            return root

search tree so organized lower << greater


recursively call the delete function on the node to the right if key is larger

        if key > root.val:
            root.right = self.deleteNode(root.right, key)

recursively call the delete function on the node to the left if key is smaller

        elif key< root.val:
            root.left = self.deleteNode(root.left, key)

if we are at the key and there is no left or no right node, return the opposite

        else:
            if not root.left:
                return root.right
            elif not root.right:
                return root.left

this is what effectively deletes the key, it replaces the key value with it's right root value

            cur = root.right

this is a little confusing but it essentially moves the nodes around if their root got moved

            while cur.left:
                cur = cur.left
            root.val = cur.val
            root.right = self.deleteNode(root.right, root.val)
        return root
