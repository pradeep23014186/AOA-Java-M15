
# EX 5B Topological Sort - Khan's Algorithm
## DATE: 20/05/2026
## AIM:
To write a Java program to for given constraints.
Problem Description:
A software development team is preparing for a product release. The release consists of multiple tasks, each dependent on other tasks being completed first. You are to determine a valid order in which all tasks can be completed. If it's not possible due to cyclic dependencies, output that the release cannot be scheduled.

Each task is labeled from 0 to n-1. The dependencies are provided in the form of pairs [a, b] which means task a depends on task b.

Implement a program to find a valid task execution order using topological sort.

Input Format:

An integer n — number of tasks.

An integer m — number of dependencies.

m lines follow with two integers a and b — representing a depends on b.

Output Format:

If a valid order exists, print the task numbers in a possible execution order (space-separated).

If not, print "Release cannot be scheduled".

<img width="341" height="363" alt="image" src="https://github.com/user-attachments/assets/f0355541-4f66-49da-bcd3-171a799a7c1f" />

## Algorithm
1. Start the program and read the number of tasks n and dependencies m from the user.
2. Create an adjacency list to represent the graph and an indegree array to store the number of incoming edges for each task.
3. Add all tasks with indegree 0 into a queue, as they have no dependencies.
4. Repeatedly remove a task from the queue, add it to the result, and reduce the indegree of its neighboring tasks. If any neighbor’s indegree becomes 0, add it to the queue.
5. If all tasks are included in the result, print the topological order; otherwise, print "Release cannot be scheduled" and stop the program.  

## Program:
```
Program to implement Reverse a String
Developed by: Krishna Prasad S
Register Number: 212223230108
```
```java
import java.util.*;

public class prog{

    public static List<Integer> findTaskOrder(int n, int[][] dependencies) 
    {
        List<List<Integer>> graph = new ArrayList<>();
        for (int i = 0; i < n; i++) graph.add(new ArrayList<>());
        int[] indegree = new int[n];
    
        for (int[] dep : dependencies) 
        {
            int a = dep[0], b = dep[1];
            graph.get(b).add(a);
            indegree[a]++;
        }
    
        PriorityQueue<Integer> q = new PriorityQueue<>();
        for (int i = 0; i < n; i++) 
        {
            if (indegree[i] == 0) q.add(i);
        }
    
        List<Integer> order = new ArrayList<>();
        while (!q.isEmpty()) 
        {
            int curr = q.poll();
            order.add(curr);
            for (int next : graph.get(curr)) 
            {
                indegree[next]--;
                if (indegree[next] == 0) q.add(next);
            }
        }
    
        if (order.size() == n) return order;
        return null; 
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt(); // number of tasks
        int m = sc.nextInt(); // number of dependencies

        int[][] dependencies = new int[m][2];
        for (int i = 0; i < m; i++) {
            dependencies[i][0] = sc.nextInt(); // a
            dependencies[i][1] = sc.nextInt(); // b
        }

        List<Integer> result = findTaskOrder(n, dependencies);

        if (result == null) {
            System.out.println("Release cannot be scheduled");
        } else {
            for (int task : result) {
                System.out.print(task + " ");
            }
        }
    }
}

```

## Output:

<img width="721" height="528" alt="output2" src="https://github.com/user-attachments/assets/109ad369-e1da-4310-ac94-4096241a3a7c" />


## Result:
The program successfully implemented and the expected output is verified.
