```java
public class RedBlackTree<T extends Comparable<T>> {

    /* Root of the tree. */
    RBTreeNode<T> root;

    static class RBTreeNode<T> {

        final T item;
        boolean isBlack;
        RBTreeNode<T> left;
        RBTreeNode<T> right;

        RBTreeNode(boolean isBlack, T item) {
            this(isBlack, item, null, null);
        }

        RBTreeNode(boolean isBlack, T item, RBTreeNode<T> left, RBTreeNode<T> right) {
            this.isBlack = isBlack;
            this.item = item;
            this.left = left;
            this.right = right;
        }
    }

    public RedBlackTree() {
        root = null;
    }

    /**
     * Null nodes are considered black.
     */
    private boolean isRed(RBTreeNode<T> node) {
        return node != null && !node.isBlack;
    }

    /**
     * Flip the color of node and its two children.
     * Assumes node.left and node.right are not null.
     */
    void flipColors(RBTreeNode<T> node) {
        node.isBlack = !node.isBlack;
        node.left.isBlack = !node.left.isBlack;
        node.right.isBlack = !node.right.isBlack;
    }

    /**
     * Rotate right.
     *
     *        node                 x
     *       /    \               / \
     *      x      C     ->      A   node
     *     / \                     /   \
     *    A   B                   B     C
     */
    RBTreeNode<T> rotateRight(RBTreeNode<T> node) {
        RBTreeNode<T> x = node.left;

        node.left = x.right;
        x.right = node;

        // Swap colors, CS61B lab style.
        boolean temp = node.isBlack;
        node.isBlack = x.isBlack;
        x.isBlack = temp;

        return x;
    }

    /**
     * Rotate left.
     *
     *      node                    x
     *     /    \                  / \
     *    A      x       ->     node  C
     *          / \             /  \
     *         B   C           A    B
     */
    RBTreeNode<T> rotateLeft(RBTreeNode<T> node) {
        RBTreeNode<T> x = node.right;

        node.right = x.left;
        x.left = node;

        // Swap colors, CS61B lab style.
        boolean temp = node.isBlack;
        node.isBlack = x.isBlack;
        x.isBlack = temp;

        return x;
    }

    /**
     * Public insert.
     * Root must always be black after insertion.
     */
    public void insert(T item) {
        root = insert(root, item);
        root.isBlack = true;
    }

    /**
     * Recursive LLRB insertion.
     */
    private RBTreeNode<T> insert(RBTreeNode<T> node, T item) {
        // Insert new node as a red leaf.
        if (node == null) {
            return new RBTreeNode<>(false, item);
        }

        // Normal BST insertion.
        int cmp = item.compareTo(node.item);

        if (cmp < 0) {
            node.left = insert(node.left, item);
        } else if (cmp > 0) {
            node.right = insert(node.right, item);
        } else {
            // Duplicate item: do nothing.
            return node;
        }

        // Case 1: right-leaning red link.
        // Fix by rotating left.
        if (isRed(node.right) && !isRed(node.left)) {
            node = rotateLeft(node);
        }

        // Case 2: two consecutive left red links.
        // Fix by rotating right.
        if (isRed(node.left) && isRed(node.left.left)) {
            node = rotateRight(node);
        }

        // Case 3: both children are red.
        // Split temporary 4-node.
        if (isRed(node.left) && isRed(node.right)) {
            flipColors(node);
        }

        return node;
    }
}
```