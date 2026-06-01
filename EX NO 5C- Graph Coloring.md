
# EX 5C Graph coloring
## DATE: 20/05/2026
## AIM:
To write a Java program to for given constraints.
Problem Description:
In a hilly region, several radio towers are installed to provide communication services. However, due to signal interference, two adjacent towers (i.e., in communication range of each other) must not use the same frequency channel.

You are given N radio towers and their communication ranges represented as an undirected graph. Your task is to assign channels (colors) to these towers using at most M channels such that no two adjacent towers use the same channel.

Write a program to determine if such an assignment is possible or not.

Input Format:
First line contains two integers: N (number of towers), and M (number of available frequency channels).

Next line contains an integer E — number of edges representing the communication range.

Next E lines contain two integers u and v — representing that tower u and tower v are within range (0-based index).

Output Format:
Print "YES" if it's possible to assign frequencies to towers such that no two adjacent towers have the same frequency.

Otherwise, print "NO".

<img width="182" height="440" alt="image" src="https://github.com/user-attachments/assets/b32078a2-c79d-4a25-88c4-e51144b5456f" />


## Algorithm
1. Start the program and read the number of towers N, number of channels M, and the connections between towers.
2. Represent the communication ranges using an adjacency list and initialize a color array with 0 to indicate unassigned channels.
3. Use a backtracking function to assign a valid channel to each tower one by one.
4. For every tower, check all available channels and assign a channel only if none of its adjacent towers has the same channel. If no valid channel is possible, backtrack and try another assignment.
5. If all towers are successfully assigned channels, print "YES"; otherwise, print "NO" and stop the program.  

## Program:
```
Program to implement Reverse a String
Developed by: Krishna Prasad S
Register Number: 212223230108
```
```java
import java.util.*;

public class RadioTowerChannelAssignment {

    public static boolean isColorable(List<List<Integer>> graph, int[] color, int node, int m, int n) 
    {
        if (node == n) return true;
        for (int c = 1; c <= m; c++) {
            boolean safe = true;
            for (int neighbor : graph.get(node)) 
            {
                if (color[neighbor] == c) 
                {
                    safe = false;
                    break;
                }
            }
            if (safe) 
            {
                color[node] = c;
                if (isColorable(graph, color, node + 1, m, n)) return true;
                color[node] = 0; 
            }
        }
        return false;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt(); // number of towers
        int m = sc.nextInt(); // number of channels
        int e = sc.nextInt(); // number of connections

        List<List<Integer>> graph = new ArrayList<>();
        for (int i = 0; i < n; i++)
            graph.add(new ArrayList<>());

        for (int i = 0; i < e; i++) {
            int u = sc.nextInt();
            int v = sc.nextInt();
            graph.get(u).add(v);
            graph.get(v).add(u);
        }

        int[] color = new int[n];

        if (isColorable(graph, color, 0, m, n))
            System.out.println("YES");
        else
            System.out.println("NO");

        sc.close();
    }
}

```

## Output:

<img width="353" height="492" alt="output3" src="https://github.com/user-attachments/assets/aac1e0cc-fe8f-49da-9096-dccfdf123fd8" />


## Result:
The program successfully implemented and the expected output is verified.
