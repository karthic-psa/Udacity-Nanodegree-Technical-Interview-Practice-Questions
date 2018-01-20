# Python Technical Interview Practice #
## Description ##
For this project, you will be given five technical interviewing questions on a variety of topics discussed in the technical interviewing course. You should write up a clean and efficient answer in Python, as well as a text explanation of the efficiency of your code and your design choices.

## Answer the following questions: ##

##  Question 1 ##

Given two strings ```s``` and ```t```, determine whether some anagram of ```t``` is a substring of ```s```. For example: if ```s = "udacity"``` and ```t = "ad"```, then the function returns ```True```. Your function definition should look like: ```question1(s, t)``` and return a boolean ```True``` or ```False```.

###  Explanation for Q-1 (Python code in ```solutions.py``` file) ###

We can check whether two strings are anagram by checking the count of all characters in both string. If all counts are the same, then the two strings are anagram. We can first compile a dictionary of counts for t and check with every possible consecutive substring sets in s. If any set is anagram of t, then we return True, else False. Comparing counts of all characters will can be done in constant time since there are only limited amount of characters to check. Looping through all possible consecutive substrings will take worst case O(len(s)). Therefore the time complexity of this algorithm is O(len(s)). Excluding the space used to load t and s, we only additionally stored the counts of t and counts of s. Since the number of character are bounded, the algorithm will only take space complexity of O(1).

##  Question 2 ##

Given a string ```a```, find the longest palindromic substring contained in ```a```. Your function definition should look like ```question2(a)```, and return a string.

###  Explanation for Q-2 (Python code in ```solutions.py``` file) ###

One observation to make is that checking the palindrome will take worst case O(n) time and can be started from the center. Since there are only O(n) location any palindromic substring can be rooted, we can easily check all possible combinations and will only take order O(n^2) time. Excluding the space used to load a, we only need to store left and right index of the longest palindromic substring. Therefore, the space complexity of this algorithm is O(1).

##  Question 3 ##

Given an undirected graph G, find the minimum spanning tree within G. A minimum spanning tree connects all vertices in a graph with the smallest possible total weight of edges. Your function should take in and return an adjacency list structured like this:

```
{'A': [('B', 2)],
 'B': [('A', 2), ('C', 5)], 
 'C': [('B', 5)]}
 ```
 
###  Explanation for Q-3 (Python code in ```solutions.py``` file) ###
 
I used Kruskal's algorithm to solve this problem. The basic idea is to sort the edges by its weight and starts include the edge without causing a cycle in the graph. One way to make sure there are no cycle in the graph is by keep track of each vertice in a list of sets. If the new edge will connect two vertices within the same set, we will not include it. Else, we include the set and take union of the sets. This algorithm has may parts. First, generate list of edges will take O(E) time and O(E) space. Second, sort the edges by weight will take O(Elog(E)) time and O(E) space. Third, loop through each edges, find the indices, and merge sets will take worst case O(E*V) time and O(V) space. Lastly, we have to convert the edges back to the required output graph structure that will take O(E) time and O(V) space. Overall my algorithm will take O(E*V) time and O(E) space. However, the overall time complexity can be further reduced to O(E*log(V)) time with "disjoint-set data structure".

##  Question 4 ##

Find the least common ancestor between two nodes on a binary search tree. The least common ancestor is the farthest node from the root that is an ancestor of both nodes. For example, the root is a common ancestor of all nodes on the tree, but if both nodes are descendents of the root's left child, then that left child might be the lowest common ancestor. You can assume that both nodes are in the tree, and the tree itself adheres to all BST properties. The function definition should look like ```question4(T, r, n1, n2)```, where ```T``` is the tree represented as a matrix, where the index of the list is equal to the integer stored in that node and a ```1``` represents a child node, ```r``` is a non-negative integer representing the root, and ```n1``` and ```n2``` are non-negative integers representing the two nodes in no particular order. For example, one test case might be

```
question4([[0, 1, 0, 0, 0],
           [0, 0, 0, 0, 0],
           [0, 0, 0, 0, 0],
           [1, 0, 0, 0, 1],
           [0, 0, 0, 0, 0]],
          3,
          1,
          4)
```
 and the answer would be ```3```.
 
###  Explanation for Q-4 (Python code in ```solutions.py``` file) ###
  
I really don't get how that matrix is representing a BST, so I made my own tree node class. I also assumed r is a valid BST node as the problem stated. We will traverse through the tree from top-down and with the BST properties, the least common ancestor between two nodes is just the first node we meet with the value between n1 and n2. We will go left if the current node is greater than both n1 and n2, right if the current node is less than both n1 and n2, else the node is the least common ancestor. Since the worst case we will traverse is the depth of a binary tree, the time complexity will be O(log(n)) (if balanced, else it will be O(n)) where n is the number of elements in the tree. The space complexity is O(1) because we only keep track of the current node at the traversal stage. Special note to deal with the edge case when n1 and/or n2 are not in the tree. We can simply traverse the BST to check if the value exist in the tree. This part will take same time and space complexity as the main algorithm, so it won't increase the overall complexities.

##  Question 5 ##
  
Find the element in a singly linked list that's ```m``` elements from the end. For example, if a linked list has 5 elements, the 3rd element from the end is the 3rd element. The function definition should look like ```question5(ll, m)```, where ```ll``` is the first node of a linked list and ```m``` is the "mth number from the end". You should copy/paste the ```Node``` class below to use as a representation of a node in the linked list. Return the value of the node at that position.

```
class Node(object):
  def __init__(self, data):
    self.data = data
    self.next = None
``` 

###  Explanation for Q-5 (Python code in ```solutions.py``` file) ###

The best way to solve this problem is to just traverse through the linked list twice. The first time we traverse through the linked list to get its length. Then we can determine how many elements to traverse on the second pass to get the mth element from the back. The time will still be O(n) for traverse through ll twice. Since we only store the length, the space complexity will be O(1). One special case to note is to deal with circular linked list. If that case is not treated, then the get_length() function might stuck in a infinite loop when feed a circular linked list. We can use two nodes each traverse at different rate to deal with the case. If both of them ever meet, then we know the linked list is circular and we can terminate the loop. This part will not take additional time in traversal and will only need to store one additional node durning the traversal. Therefore the overall time and space complexity will not be affected.


 
