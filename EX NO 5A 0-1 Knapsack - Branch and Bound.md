
# EX 5A 0/1 Knapsack Problem - Branch&Bound 
## DATE: 18/05/2026
## AIM:
To Write a Java program to solve 0/1 Knapsack problem using Branch and Bound Approach.
You are heading a college entrepreneurship cell that can invest in up to N student‑startups.

For each startup i you know: cost[i]  — the amount (in ₹ lakh) required to join the showcase profit[i] — the estimated profit (in ₹ lakh) you’ll gain if it succeeds You have a total budget of B ₹ lakh. Pick a subset of startups so that the sum of costs ≤ B and the sum of profits is maximised.

Because N can be as large as 50, a plain exhaustive search (2^N) is too slow.

The recommended approach is Branch & Bound with a fractional‑knapsack upper bound (but any algorithm that meets the constraints is accepted). 

Input Format

N

B

cost[1] cost[2] … cost[N]

profit[1] profit[2] … profit[N]

1 ≤ N ≤ 50

1 ≤ B ≤ 1 000 000

1 ≤ cost[i], profit[i] ≤ 10 000 

Output Format

maxProfit

For example:




## Algorithm
1. Start the program and read the number of startups N, budget B, costs, and profits of each startup.
2. Sort the startups in descending order based on the profit-to-cost ratio to obtain a better upper bound.
3. Use a Branch and Bound approach with Depth First Search (DFS) to explore possible selections of startups.
4. At each step, calculate an upper bound using the fractional knapsack method. If the bound is greater than the current best profit, continue exploring that branch; otherwise, prune the branch.
5. Update the maximum profit whenever a better valid solution is found, print the final maximum profit, and stop the program. 

## Program:
```
Program to implement Reverse a String
Developed by: Krishna Prasad S
Register Number: 212223230108
```
```java
import java.util.*;

public class StartupShowcaseOptimizer {

    // Global data 
    static int N, B;
    static int[] c, p;          
    static int best = 0;        

    // Fractional upper bound
    static double bound(int idx, int cw, int cv) {
        double result = cv;
        int totalCost = cw;

        // Greedily add items fractionally to estimate upper bound
        for (int i = idx; i < N; i++) 
        {
            if (totalCost + c[i] <= B) 
            {
                totalCost += c[i];
                result += p[i];
            } 
            else 
            {
                int remain = B - totalCost;
                result += p[i] * (double) remain / c[i];
                break;
            }
        }
        return result;
    }

    //DFS Branch & Bound
    static void dfs(int idx, int cw, int cv) 
    {
        if (idx == N) 
        {
            best = Math.max(best, cv);
            return;
        }
        if (cw + c[idx] <= B) 
        {
            dfs(idx + 1, cw + c[idx], cv + p[idx]);
        }
        if (bound(idx + 1, cw, cv) > best) 
        {
            dfs(idx + 1, cw, cv);
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        N = sc.nextInt();
        B = sc.nextInt();
        int[] cost = new int[N];
        int[] prof = new int[N];
        for (int i = 0; i < N; i++) cost[i] = sc.nextInt();
        for (int i = 0; i < N; i++) prof[i] = sc.nextInt();
        sc.close();

        // Sort by profit/cost ratio descending → tighter bounds
        Integer[] idx = new Integer[N];
        Arrays.setAll(idx, i -> i);
        Arrays.sort(idx, Comparator.comparingDouble(i -> -(double) prof[i] / cost[i]));

        c = new int[N];
        p = new int[N];
        for (int i = 0; i < N; i++) {
            c[i] = cost[idx[i]];
            p[i] = prof[idx[i]];
        }

        dfs(0, 0, 0);
        System.out.println(best);
    }
}

```

## Output:

<img width="364" height="228" alt="output1" src="https://github.com/user-attachments/assets/8b7ff236-a57b-4ccd-aeb6-0f025f674d00" />


## Result:
The program successfully solved 0/1 Knapsack problem using branch & bound and output is verified. 
