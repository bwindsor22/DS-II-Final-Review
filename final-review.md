# Data Structures/Algos
## Maps
For an array of strings, return the common elements between all strings. When a letter appears more than once in all strings, return it more than once. For instance, for ["abca","daab", "iuoewaawioeb", "caazb"], you would return ["a", "a", "b"].

## Trees
Given a binary search tree, and a range, return a sum of all of the elemnts in the range. For instance, for the below tree, and the range [2, 4], you would return 2 + 2.5 + 3 + 4 = 11.5
```
       3
   2       6
1   2.5  4   9
```

## Graphs
* Draw a graph where a BFS and DFS produce the same traversal
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
* In which of the following situations would Dijkstra's be most useful? Why?
    * Finding the fastest way to route a phone call between two telephones
    * Given two people, find a path of who-knows-who between them, e.g. Jane knows Sally knows Mary knows Linda 

## Dynamic Programming
* Suppose a robot starts on stair 0, and it can hop 1, 2, or 3 stairs. We wish to find the number of ways it can arrive at a stair. For instance, there are two ways to arrive at stair 2, either two hops of size 2, or one hop of size 2. 

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
# CS Tools
## Bash
* Describe what each of these functions do. What are the windows equivalents of each of them?
    * htop
    * tmux
* Describe how you would make a folder in linux titled "grades" with a file "mygrade.txt" with the word "A+" inside
    * You may use this site to test your work: `https://www.onlinegdb.com/online_bash_shell`


## Threads
* Explain what each of the following mean:
    * Deadlock
    * Livelock
    * Starvation

* Explain what each of these classes/methods do:
    * Executor.fixedThreadPool
    * Lock

## Regex
* The regex pattern `[a-z].+[0-9]` would match which of the following? Mark all that apply
    * asdf###390
    * asd9
    * a9

# AI in Computer Science
* Which of the following games would it be easiest to write an AI to solve, assuming the AI uses the Minimax algorithm? Explain your answer.
    * Poker
    * Checkers
* You wish to build a system that would detect whether the speaker in a chat room is a spammer or real person. How would the TF-IDF algorithm help in a situation like this? What does the IDF stand for?



