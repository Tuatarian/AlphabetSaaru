When a [[Node]] is placed for the first time, it is spawned with no connections and nothing connected to it.

Each node will be a rectangle, the position will represent the center of that rectangle. 

Here is an example of what it may end up looking like:
![[XorBox.png]]

The current plan is to keep the rectangle size static across all Nodes, keeping the offsets for drawing the text ([[NodeType]]) and number (output) and their respective fontsizes completely constant. This is likely to make the implementation of this significantly easier, but it may make the game look too uniform, in which case a more dynamic approach will have to be taken

Another thing is regarding the visuals for connecting the various nodes together. I currently plan to use a tier 3 (cubic, w/ 4 points) bezier curve to draw the connections. To generate a set of 4 points {1, 2, 3, 4}, the current plan is to:

- Have the starting point and ending point (A and B), representing the position of the origin and endpoint nodes. Note their y pos
- Find the midpoint of the line between A and B, let that = mp
- Construct the curve from {A, (mp.x, A.y), (mp.x, B.y), B}

Basically, find the midpoint, then set points 2 and 3 as the x value of the midpoint and the y value of A and B respectively. This should create a reasonably nice looking connection for the vast majority of cases. 

Rendering this equation should also be fairly straightforward. Bezier curves always run from 0 <= x <= 1, with 0 and 1 being A and B respectively. As a result, to get the real X coordinate, all we need to do is multiply by absval A.x - B.x and then add A.x. To get the y coordinate, we simply need to add A.y. Knowing this, we can increment x from 0 to 1 in small steps, then after converting the recieved coords to screen space, we can render small lines between each step to approximate the real curve. 