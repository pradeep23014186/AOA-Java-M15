
# EX 5D Flower Planting.
## DATE: 20/05/2026
## AIM:
To write a Java program to for given constraints.
You are given n gardens, labelled from 1 to n.

You also have a list called paths, where each element paths[i] = [xi, yi] represents a bidirectional road connectingthe  garden xi and garden yi.

You want to plant one flower in each garden, and there are exactly 4 types of flowers labelled as 1, 2, 3, and 4.

Your goal is to plant flowers such that:

No two connected gardens (i.e., connected via a path) have the same flower type.

Return any valid flower assignment as an array where:

answer[i] is the flower type planted in the (i+1) ᵗʰ garden

It is guaranteed that:

No garden is connected to more than 3 other gardens

A valid flower assignment always exists

<img width="177" height="292" alt="image" src="https://github.com/user-attachments/assets/36aa40cb-1cdd-4746-b1a6-fc51ce6e96aa" />

## Algorithm
1. Start the program and read the number of gardens n and the paths connecting the gardens.
2. Create an adjacency list to represent the connections between gardens.
3. Initialize an array to store flower types for each garden.
4. For each garden, check the flower types already assigned to its neighboring gardens and choose a flower type from 1 to 4 that is not used by any neighbor.
5. Assign the valid flower type to the garden, print the flower arrangement for all gardens, and stop the program.  

## Program:
```
Program to implement Reverse a String
Developed by: Krishna Prasad S
Register Number: 212223230108
```
```java
import java.util.*;

public class GardenFlowerPlanner {

    public static int[] assignFlowers(int n, int[][] paths) 
    {
        List<List<Integer>> graph = new ArrayList<>();
        for (int i = 0; i < n; i++) graph.add(new ArrayList<>());
        for (int[] path : paths) 
        {
            int u = path[0] - 1; 
            int v = path[1] - 1;
            graph.get(u).add(v);
            graph.get(v).add(u);
        }

        int[] flowers = new int[n];

        for (int i = 0; i < n; i++) 
        {
            boolean[] used = new boolean[5];
            for (int neighbor : graph.get(i)) 
            {
                if (flowers[neighbor] != 0) 
                {
                    used[flowers[neighbor]] = true;
                }
            }
            for (int type = 1; type <= 4; type++) 
            {
                if (!used[type]) 
                {
                    flowers[i] = type;
                    break;
                }
            }
        }
        return flowers;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt(); // number of gardens
        int m = sc.nextInt(); // number of paths
        int[][] paths = new int[m][2];
        for (int i = 0; i < m; i++) {
            paths[i][0] = sc.nextInt();
            paths[i][1] = sc.nextInt();
        }

        int[] result = assignFlowers(n, paths);
        for (int flower : result) {
            System.out.print(flower + " ");
        }
        sc.close();
    }
}

```

## Output:

<img width="403" height="461" alt="output4" src="https://github.com/user-attachments/assets/4eb6727e-2ef4-4618-a922-d049fb7fa54f" />


## Result:
The program successfully implemented and the expected output is verified.
