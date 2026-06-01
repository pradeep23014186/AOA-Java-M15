
# EX 5E Minimum Spanning Tree -Boruvka's Algorithm
## DATE: 20/05/2026
## AIM:
To write a Java program to for given constraints.
Boruvka's Algorithm - Minimum Spanning Tree

Find the MST using Boruvka's Algorithm for a weighted undirected graph.
<img width="292" height="235" alt="image" src="https://github.com/user-attachments/assets/06246b27-37a9-40a8-bd7a-37a1d5187cd1" />

## Algorithm
1. Start the program and read the number of vertices, edges, and edge details of the weighted undirected graph.
2. Initialize each vertex as a separate component using the Disjoint Set (Union-Find) data structure.
3. For every component, find the cheapest edge that connects it to another component.
4. Add all selected cheapest edges to the Minimum Spanning Tree (MST), merge the connected components using union operation, and update the total MST weight.
5. Repeat the process until only one component remains, then print the edges of the MST and the total weight, and stop the program.   

## Program:
```
Program to implement Reverse a String
Developed by: Krishna Prasad S
Register Number: 212223230108
```
```java
import java.util.*;

public class BoruvkaMST {
    static int[] parent;

    static int find(int i) {
        if (parent[i] != i)
            parent[i] = find(parent[i]);
        return parent[i];
    }

    static void union(int x, int y) {
        parent[find(x)] = find(y);
    }

    static int boruvkaMST(int V, List<Edge> edges) {
        parent = new int[V];
        for (int i = 0; i < V; i++) parent[i] = i;

        int numTrees = V;
        int mstWeight = 0;

        Edge[] cheapest = new Edge[V];

        while (numTrees > 1) {
            Arrays.fill(cheapest, null);

            for (Edge e : edges) {
                int set1 = find(e.src);
                int set2 = find(e.dest);

                if (set1 == set2) continue;

                if (cheapest[set1] == null || cheapest[set1].weight > e.weight)
                    cheapest[set1] = e;

                if (cheapest[set2] == null || cheapest[set2].weight > e.weight)
                    cheapest[set2] = e;
            }

            for (int i = 0; i < V; i++) {
                Edge e = cheapest[i];
                if (e != null) {
                    int set1 = find(e.src);
                    int set2 = find(e.dest);

                    if (set1 == set2) continue;

                    System.out.println("Edge: " + e.src + "-" + e.dest + " Weight: " + e.weight);
                    mstWeight += e.weight;
                    union(set1, set2);
                    numTrees--;
                }
            }
        }

        return mstWeight;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int V = sc.nextInt();
        int E = sc.nextInt();

        List<Edge> edges = new ArrayList<>();
        for (int i = 0; i < E; i++) {
            edges.add(new Edge(sc.nextInt(), sc.nextInt(), sc.nextInt()));
        }

        int totalWeight = boruvkaMST(V, edges);
        System.out.println("Total Weight of MST: " + totalWeight);

        sc.close();
    }
}

class Edge {
    int src, dest, weight;
    Edge(int s, int d, int w) {
        src = s; dest = d; weight = w;
    }
}

```

## Output:

<img width="662" height="482" alt="output5" src="https://github.com/user-attachments/assets/9b210fd0-ccdd-4028-8517-1f0d325851a2" />


## Result:
The program successfully implemented and the expected output is verified.
