<h1>ExpNo 4 : Implement A* search algorithm for a Graph</h1> 
<h3>Name:Raja Rithika M       </h3>
<h3>Register Number:2305001029           </h3>
<H3>Aim:</H3>
<p>To ImplementA * Search algorithm for a Graph using Python 3.</p>
<H3>Algorithm:</H3>


// A* Search Algorithm
1.  Initialize the open list
2.  Initialize the closed list
    put the starting node on the open 
    list (you can leave its f at zero)

3.  while the open list is not empty
    a) find the node with the least f on 
       the open list, call it "q"

    b) pop q off the open list
  
    c) generate q's 8 successors and set their 
       parents to q
   
    d) for each successor
        i) if successor is the goal, stop search
        
        ii) else, compute both g and h for successor
          successor.g = q.g + distance between 
                              successor and q
          successor.h = distance from goal to 
          successor (This can be done using many 
          ways, we will discuss three heuristics- 
          Manhattan, Diagonal and Euclidean 
          Heuristics)
          
          successor.f = successor.g + successor.h

        iii) if a node with the same position as 
            successor is in the OPEN list which has a 
           lower f than successor, skip this successor

        iV) if a node with the same position as 
            successor  is in the CLOSED list which has
            a lower f than successor, skip this successor
            otherwise, add  the node to the open list
     end (for loop)
  
    e) push q on the closed list
    end (while loop)

## PROGRAM
```python

import heapq

def a_star_search(graph, start, goal, heuristic):
    open_set = []
    heapq.heappush(open_set, (0 + heuristic[start], 0, start))  # (f_cost, g_cost, node)

    came_from = {}
    g_score = {node: float('inf') for node in graph}
    g_score[start] = 0

    while open_set:
        current_f_cost, current_g_cost, current_node = heapq.heappop(open_set)

        if current_node == goal:
            path = []
            while current_node in came_from:
                path.append(current_node)
                current_node = came_from[current_node]
            path.append(start)
            path.reverse()
            return path

        for neighbor, weight in graph[current_node].items():
            tentative_g_score = g_score[current_node] + weight

            if tentative_g_score < g_score[neighbor]:
                came_from[neighbor] = current_node
                g_score[neighbor] = tentative_g_score
                f_cost = tentative_g_score + heuristic[neighbor]
                heapq.heappush(open_set, (f_cost, tentative_g_score, neighbor))

    return None


graph = {}
num_nodes = int(input("Enter number of nodes in the graph: "))

print("\nEnter neighbors in the format: neighbor:weight (comma separated).")
print("Example: For node A → B with cost 1 and C with cost 4, enter: B:1,C:4")
print("If no neighbors, press Enter.\n")

for _ in range(num_nodes):
    node = input("Enter node name: ").strip()
    neighbors = input(f"Enter neighbors for {node}: ").strip()
    graph[node] = {}
    if neighbors:
        for edge in neighbors.split(","):
            n, w = edge.split(":")
            graph[node][n.strip()] = int(w.strip())

# Input heuristics
heuristic = {}
print("\nEnter heuristic values for each node:")
for node in graph:
    h = int(input(f"Heuristic value for {node}: "))
    heuristic[node] = h

# Start and goal
start_node = input("\nEnter the start node: ").strip()
goal_node = input("Enter the goal node: ").strip()

# Run A* Search
path = a_star_search(graph, start_node, goal_node, heuristic)

if path:
    print(f"\nPath found: {path}")
else:
    print("\nNo path found.")
import networkx as nx

G = nx.DiGraph()

for node, neighbors in graph.items():
    for neighbor, weight in neighbors.items():
        G.add_edge(node, neighbor, weight=weight)

import matplotlib.pyplot as plt
pos = nx.spring_layout(G)

nx.draw(G, pos, with_labels=True, node_size=700, node_color='skyblue', font_size=10, font_weight='bold')

edge_labels = nx.get_edge_attributes(G, 'weight')

nx.draw_networkx_edge_labels(G, pos, edge_labels=edge_labels, font_color='red')

plt.show()
```

SAMPLE GRAPH I
![277151990-b1377c3f-011a-4c0f-a843-516842ae056a](https://github.com/user-attachments/assets/bedfaca4-a69a-468a-957d-a3def3f28836)

SAMPLE INPUT
10 14 <br>
A B 6 <br>
A F 3 <br>
B D 2 <br>
B C 3 <br>
C D 1 <br>
C E 5 <br>
D E 8 <br>
E I 5 <br>
E J 5 <br>
F G 1 <br>
G I 3 <br>
I J 3 <br>
F H 7 <br>
I H 2 <br>
A 10 <br>
B 8 <br>
C 5 <br>
D 7 <br>
E 3 <br>
F 6 <br>
G 5 <br>
H 3 <br>
I 1 <br>
J 0 <br>
<hr>
Sample Output

![435098048-ac8a5725-93b0-44e9-bba7-8a32d7ee80ee](https://github.com/user-attachments/assets/23a66732-b6f5-4b74-8eae-e3e21b0f6814)




<hr>
<h2>Sample Graph II</h2>
<hr>

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/acbb09cb-ed39-48e5-a59b-2f8d61b978a3)


<hr>
<h2>Sample Input</h2>
<hr>
6 6 <br>
A B 2 <br>
B C 1 <br>
A E 3 <br>
B G 9 <br>
E D 6 <br>
D G 1 <br>
A 11 <br>
B 6 <br>
C 99 <br>
E 7 <br>
D 1 <br>
G 0 <br>
<hr>

SAMPLE OUTPUT

![435098114-175123a9-8519-4ec4-b3f6-1151b674380d](https://github.com/user-attachments/assets/91f98b2e-c195-45de-9dbf-19bc17dbfb8f)

GRAPH:

<img width="821" height="617" alt="Screenshot 2025-10-06 134348" src="https://github.com/user-attachments/assets/74b39bdd-063f-4ff9-87bc-0d3d112508eb" />


INPUT:

<img width="726" height="511" alt="Screenshot 2025-10-06 134452" src="https://github.com/user-attachments/assets/7fa23153-92e0-4b05-92e2-120ff9203138" />



OUTPUT:

<img width="359" height="38" alt="Screenshot 2025-10-06 134509" src="https://github.com/user-attachments/assets/07644645-5a04-45f1-9978-4c91031b25e9" />


## RESULT:
Thus the Implement A* search algorithm for a Graph is executed and verified successfully.
