Game will take place on a directed graph with each [[Node]] having in and out links to other Nodes. Explanation for rendering the graph can be found in [[Rendering the Digraph]]

## Technical Explanation

The game field is a **directed graph** (digraph) - each connection goes one way. (Node X outputting to Node Y != Node Y outputting to Node X). The only connections represented will be outputs, as for both the purposes of rendering and for calculation, we will be feeding *forward* the value we get out of each node, going backwards is unneeded

The connections will be represented using an **Adjacency List**, a `seq[seq[int]]`. Each node will have an ID, equal to the length of the list (first node is 0, second is 1, etc) .  `seq[i]` will be a seq of all the nodes that the i-th node outputs to. When a node is deleted, all nodes with ID > the ID of the deleted node will have their ID decreased by 1. For example, if there are nodes with ID 0..3, and node 1 is deleted, node 2 -> 1 and node -> 2

When a node is placed into the chart, it will begin with no connections. The order of the inputs will be decided by the order of the connections - the output of an older connection will be earlier in the `seq` of inputs than a connection established later. This will make a difference for operations like subtraction, for which the order of inputs matters. As a result, the player will be able to sever a connection by right clicking on it, meaning that they can rearrange the order of the operations if they so wish. 

We will need to store the Nodes themselves, not just their connections. The current plan is to integrate this `seq[int]` defining connections into the opNode datatype itself, meaning we can have one `seq[opNode]` instead of using tuples or having 2 seqs. Deleting a node may prove a bit more difficult, however - The current plan is to:

- define func for subtracting 1 if x >= y (calling sub1if)
- Store the index of the `opNode` being deleted
- delete that from the `seq`
- iterate through `i in index..<seq.len`:
	- iterate through `j in 0..<i.connections.len`:
		- if any in tuple == inx:
			- mark index for deletion
		- elif any > inx:
			- subtract 1 from it