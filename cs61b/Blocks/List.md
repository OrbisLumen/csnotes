```java
public interface List<Item> {

    public void insert(Item x, int position);

    public void addFirst(Item x);

    public Item addLast(Item x);

    public Item getFirst();

    public Item getLast();

    public Item get(int i);

    public int size();

    public Item removeLast();

}