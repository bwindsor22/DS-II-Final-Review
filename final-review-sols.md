# Data Structures/Algos
## Maps
For an array of strings, return the common elements between all strings. When a letter appears more than once in all strings, return it more than once. For instance, for ["abca","daab", "iuoewaawioeb", "caazb"], you would return ["a", "a", "b"].

```
// Solution using lots of lambdas
import java.util.*;
import java.util.stream.Collectors;
import java.util.stream.IntStream;

public class Final {
    List<String> commonLetters(String[] inputs) {
        // convert each string to a count of characters
        List<Map<Character, Integer>> maps = Arrays.stream(inputs).map((inp) -> convertToMap(inp)).collect(Collectors.toList());

        // find the characters common across all maps
        Set<Character> chars = maps.stream().map((map) -> map.keySet()).reduce((keys1, keys2) -> {
            keys1.retainAll(keys2);
            return keys1;
        }).get();

        // put all of those as a set
        // a -> INFINITY
        // b -> INFINITY
        Map<Character, Integer> solution = new HashMap<>();
        chars.forEach((c) -> solution.put(c, Integer.MAX_VALUE));



        // set solution to have the minimum count of the character in each map
        // a -> 2
        // b -> 1
        maps.forEach((map) -> {
            map.entrySet().forEach((entry) -> {
                if (solution.containsKey(entry.getKey())) {
                    solution.put(entry.getKey(), Math.min(solution.get(entry.getKey()), entry.getValue()));
                }
            });
        });

        // convert solution to an array
        List<Character> charsRepeated = new ArrayList<>();
        solution.entrySet().forEach((entry) -> {
            IntStream.range(0, entry.getValue()).forEach((i) -> charsRepeated.add(entry.getKey()));
        });

        return charsRepeated.stream().map((s) -> s.toString()).collect(Collectors.toList());

    }
    Map<Character, Integer> convertToMap(String input) {
        Map<Character, Integer> map = new HashMap<>();
        for (Character c : input.toCharArray()){
            map.put(c, map.getOrDefault(c, 0) + 1);
        }
        return map;
    }

    public static void main(String[] args) {
        System.out.print(new Final().commonLetters(new String[]{"abca","daab", "iuoewaawioeb", "caazb"}));
    }
}

```
## Trees
Given a binary search tree, and a range, return a sum of all of the elemnts in the range. For instance, for the below tree, and the range [2, 4], you would return 2 + 2.5 + 3 + 4 = 11.5
```
       3
   2       6
1   2.5  4   9
```

```
Solution, using an inorder traversal:

    int sum = 0;
    int low = 0;
    int high = 0;
    public int sumOfBST(Node root, int low, int high) {
        this.low = low;
        this.high = high;
        traverse(root);
        return sum;
    }
    
    public void traverse(Node root) {
        if(root != null) {
            traverse(root.left);
            if(isInRange(root.val)) {
                sum += root.val;
            }
            traverse(root.right);
        }
        
    }
    
    public boolean isInRange(int val) {
        return low <= val && val <= high;
    }

```


## Graphs
* Draw a graph where a BFS and DFS produce the same traversal
```
Solution:
1 -> 2 -> 3 -> 4
```
* Given an adjacency list and two nodes, write code that determines whether both nodes are connected
```
node -> connections
0 -> 1, 2, 3
1 -> 0
2 -> 0, 2
3 -> 0
4 -> 2

Input: 0, 4
Output: True
```

```
Write a BFS or DFS from one node to another; see e.g. https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/
```

* In which of the following situations would Dijkstra's be most useful? Why?
    * Finding the fastest way to route a phone call between two telephones
    * Given two people, find a path of who-knows-who between them, e.g. Jane knows Sally knows Mary knows Linda 

```
Solution:
Disjstra's is most useful in the first scenario, because it looks at the weights in a weighted
 graph to determine the closest node. A phone call might be faster to route over a shorter wire,
  so we would want an algorithm that takes into account wire length.
```

## Dynamic Programming
* Suppose a robot starts on stair 0, and it can hop 1, 2, or 3 stairs. We wish to find the number of ways it can arrive at a stair. For instance, there are two ways to arrive at stair 2, either two hops of size 1, or one hop of size 2. 

The below code solves this, but does so in exponential time. Rewrite the code so it runs in linear time.
```
    int findSteps(int n){
        if (n <= 1){
            return 1;
        } else if (n == 2) {
            return 2; // 2, 1 + 1
        } else if (n == 3) {
            return 4; // 1 + 1 + 1, 1 + 2, 2 + 1, 3   
        } else {
            return findSteps(n-1) + findSteps(n - 2) + findSteps(n - 3);
        }
    }
    
```
Solution:
```
    int findSteps(Map<Integer, Integer> cache, int n){
        if (cache.containsKey(n)){
            return cache.get(n);
        }
        if (n <= 1){
            return 1;
        } else if (n == 2) {
            return 2; // 2, 1 + 1
        } else if (n == 3) {
            return 4; // 1 + 1 + 1, 1 + 2, 2 + 1, 3   
        } else {
            int solution = findSteps(cache, n-1) + findSteps(cache, n - 2) + findSteps(cache, n - 3);
            cache.put(n, solution);
            return solution;
        }
    }

```

# CS Tools
## Bash
* Describe what each of these functions do. What are the windows equivalents of each of them?
    * htop -- Explorere.exe, or the Windows view (the ability to show different programs at once and resize the view screens)
    * tmux -- Task Manager
* Describe how you would make a folder in linux titled "grades" with a file "mygrade.txt" with the word "A+" inside
    * You may use this site to test your work: `https://www.onlinegdb.com/online_bash_shell`

```
Solution:

mkdir grades
cd grades
nano mygrade.txt 
A+
```

## Threads
* Explain what each of the following mean:
    * Deadlock -- One thread is holding a resource, so the other thread cannot access it. "My brother has the car so I cannot drive to school."
    * Livelock -- Threads keep alternating resources but are blocking each other. "My brother saw me coming down the left side of the hallway so he moved right, but then I moved right, so we both moved left, and both right again..."
    * Starvation -- One process is consuming all the threads. "My mom made cookies but my brother ate all of them, now I have no cookies."

* Explain what each of these classes/methods do:
    * Executor.fixedThreadPool -- This determines the number of threads the Executor has to run something
    * Lock -- Using a lock will allow just one thread to access an object at a time


## Regex
* The regex pattern `[a-z].+[0-9]` would match which of the following? Mark all that apply. You may use the following to test: `https://regex101.com/`
    * asdf###390 -- match
    * asd9 -- match
    * a9 -- no match. The "+" operator means "match one or more"; the "." means "anything". So the pattern means "letters followed by one or more of anything followed by a number" which the sample does not match.

# AI in Computer Science
* Which of the following games would it be easiest to write an AI to solve, assuming the AI uses the Minimax algorithm? Explain your answer.
    * Poker
    * Checkers
```
Solution:
See minimax lecture:  https://docs.google.com/presentation/d/1PjWxkp9bf2QOZ24XKMN6eMXsYM9blh47CW2Wln8R-OQ/edit?usp=sharing 
Minimax represents each of the available options as a node on a tree, and computes the node with the highest value. To do this, 
we must be able to represent the game state as a node.

This is very easy to do in checkers; we just use the checkers board as a position on the tree.
In poker, it's much more complicated; it's harder to represent the different random cards and players tendencies to bluff
 as states on a tree.

```

* You wish to build a system that would detect whether the speaker in a chat room is a spammer or real person. How would the TF-IDF algorithm help in a situation like this? What does the IDF stand for?
```
Solution:
Recall the NLP lecture and simple sentiment analysis code:
https://docs.google.com/presentation/d/19SZE3dFBzFzbZPX7uarzL9-g6HGfxuO5PgDp7OV5PME/edit
https://gist.github.com/bwindsor22/7281bc056e9adf51c12dda5a4590c82a 

To train this algorithm, have a bunch of examples of a spammer talking and a real person talking, and
 feed them into the TF-IDF algorithm as positive (spammer) or negative (real person) examples. 
 The algorithm will learn the most common words for both the spammer and
 real person and be able to distinguish the two.

IDF stands for inverse-document frequency. This means that common words, like "the, and, hi", are treated
 as less important than uncommon words; "buy now, zebra"
```

