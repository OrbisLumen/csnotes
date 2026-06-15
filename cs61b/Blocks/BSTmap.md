```java
public class BSTMap<K extends Comparable<K>, V> {

    private class Node {
        K key;
        V value;
        Node left, right;

        Node(K k, V v) {
            key = k;
            value = v;
        }
    }

    private Node root;

    /* ===================== FIND (GET) ===================== */

    public V get(K key) {
        return get(root, key);
    }

    private V get(Node x, K key) {
        if (x == null) return null;

        int cmp = key.compareTo(x.key);
        if (cmp < 0) return get(x.left, key);
        else if (cmp > 0) return get(x.right, key);
        else return x.value;
    }

    /* ===================== INSERT (PUT) ===================== */

    public void put(K key, V value) {
        root = put(root, key, value);
    }

    private Node put(Node x, K key, V value) {
        if (x == null) return new Node(key, value);

        int cmp = key.compareTo(x.key);
        if (cmp < 0) x.left = put(x.left, key, value);
        else if (cmp > 0) x.right = put(x.right, key, value);
        else x.value = value; // update existing key

        return x;
    }

    /* ===================== DELETE (REMOVE) ===================== */

    public void remove(K key) {
        root = remove(root, key);
    }

    private Node remove(Node x, K key) {
        if (x == null) return null;

        int cmp = key.compareTo(x.key);

        if (cmp < 0) {
            x.left = remove(x.left, key);
        } else if (cmp > 0) {
            x.right = remove(x.right, key);
        } else {
            // FOUND NODE

            // Case 1: no left child
            if (x.left == null) return x.right;

            // Case 2: no right child
            if (x.right == null) return x.left;

            // Case 3: two children (Hibbard deletion)
            Node t = x;
            x = min(t.right);                 // successor
            x.right = deleteMin(t.right);    // remove successor
            x.left = t.left;
        }

        return x;
    }

    /* ===================== HELPERS ===================== */

    private Node min(Node x) {
        if (x.left == null) return x;
        return min(x.left);
    }

    private Node deleteMin(Node x) {
        if (x.left == null) return x.right;
        x.left = deleteMin(x.left);
        return x;
    }
}
```