```java
public class QuickUnionDS implements DisjointSets {
    
    private int[] parent;
    
    public QuickUnionDS(int N) {        
        parent = new int[N];
        for (int i = 0; i < N; i++) {
            parent[i] = -1;
        }
    }

    private int find(int p) {
        if (parent[p] < 0) return p;
        parent[p] = find(parent[p]);
        return parent[p];    
    }

    public boolean isConnected(int p, int q) {
        return find(p) == find(q);
    }

    public void connect(int p, int q) {
        if (isConnected(p, q)) {
            return;
        }
            int i = find(p);
            int j = find(q);
        if (parent[i] < parent[j]) { 
            // i has larger size (more negative)
            parent[i] += parent[j];
            parent[j] = i;
        } else {
            parent[j] += parent[i];
            parent[i] = j;
        }
    }
}
```