```java
public class AList {

    private int[] items;
    private int size;

    /**
     * Creates an empty list.
     */
    public AList() {
        this.items = new int[100];
        this.size = 0;
    }

    /**
     * Resizes the underlying array to the target capacity.
     */
    private void resize (int capacity) {
        int[] a = new int[capacity];
        System.arraycopy(this.items, 0, a, 0, size);
        this.items = a;
    }

    /**
     * Inserts X into the back of the list.
     */
    public void addLast(int x) {
        if (this.size == this.items.length){
            this.resize(this.size * 2);
            // change resize(this.size + 1) to resize(this.size * 2)
            // O(n^2) --> O(n)
        }
        this.items[this.size] = x;
        this.size++;
    }

    /**
     * Returns the ith item in the list (0 is the front).
     */
    public int getLast() {
        return this.item[this.size - 1];
    }

    /**
     * Returns the number of items in the list.
     */
    public int size() {
        return this.size;
    }

    /**
     * Deletes item from back of the list and returns deleted item.
     */
    public int removeLast() {
        this.size--;
        return this.items[this.size];
    }

}
```
### Nulling Out Deleted Items

```java
public Glorp removeLast() {
    Glorp returnItem = getLast();
    this.size--;
    this.items[this.size] = null;
    return returnItem;
}
```
- Java only destroys unwanted objects when the last reference has been lost.
- Keeping references to unneeded objects is sometimes called loitering.