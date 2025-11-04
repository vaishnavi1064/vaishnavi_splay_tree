<h1 align="center">🌳 <b>Multi-Splay Tree Implementation in C</b></h1>

<h2>🎯 <b>Project Overview</b></h2>
<p>
This project is an advanced data structure implementation in C, specifically a <b>Multi-Splay Tree</b>. This structure is often used as a component in more complex dynamic data structures, such as <b>Link-Cut Trees (LCT)</b>, to efficiently manage and query forests of trees.
</p>
<p>
Unlike a standard splay tree, this implementation manages a "tree of trees." It uses splay operations not only to access nodes but also to change the "preferred path" of the tree, which is essential for dynamic graph algorithms. The core of this project is the <code>MultiSplayAlgo</code> function, which restructures the tree after an access.
</p>

<h2>🧩 <b>Key Data Structure Concepts</b></h2>
<p>
The <code>struct node</code> forms the basis of the tree and contains several key fields beyond standard left/right children:
</p>
<ul>
<li><code>key</code>: The integer value of the node.</li>
<li><code>depth</code>: The node's depth in the conceptual "represented tree."</li>
<li><code>mindepth</code>: The minimum depth of any node in the splay subtree rooted at this node.</li>
<li><code>isRoot</code>: A crucial boolean. In the context of Link-Cut Trees, this flag indicates if the edge to its parent is a "dashed edge" (<code>true</code>) or a "solid edge" (<code>false</code>). A solid edge means the node is on the same "preferred path" (splay tree) as its parent.</li>
<li><code>parent</code>, <code>leftChild</code>, <code>rightChild</code>: Standard tree pointers.</li>
</ul>

<h2>⚙️ <b>Core Functionality</b></h2>

<h3>1️⃣ Tree Construction (<code>BuildTree</code>)</h3>
<ul>
<li>Recursively builds a balanced binary search tree from a given range of integers.</li>
<li>Initializes <code>depth</code>, <code>mindepth</code>, and <code>isRoot</code> flags for all nodes.</li>
</ul>

<h3>2️⃣ Rotation (<code>Rotate</code>)</h3>
<ul>
<li>Performs a single rotation (zig or zag) on a node <code>ptr</code>.</li>
<li>Correctly updates parent-child pointers and the <code>isRoot</code> status.</li>
<li>This is the fundamental operation used by the <code>splay</code> function.</li>
</ul>

<h3>3️⃣ Splay Operation (<code>splay</code>)</h3>
<ul>
<li>Takes a node <code>ptr</code> and splays it up to a specified <code>top</code> node (or the root of its splay tree).</li>
<li>Handles zig-zig, zig-zag, zag-zag, and zag-zig cases by calling <code>Rotate</code> appropriately.</li>
</ul>

<h3>4️⃣ Path Management (<code>SwitchPath</code> & <code>refParent</code>)</h3>
<ul>
<li>This is the "multi-splay" or "dynamic tree" component.</li>
<li><code>SwitchPath</code> is called to change the preferred path. It finds the new child that should be on the preferred path (using <code>refParent</code>) and splays it, toggling the <code>isRoot</code> flag on the old preferred child to mark its edge as "dashed."</li>
</ul>

<h3>5️⃣ The Multi-Splay Algorithm (<code>MultiSplayAlgo</code>)</h3>
<ul>
<li>This is the main access function.</li>
<li>It takes a node <b>ptr</b> and brings it to the root of the entire represented tree (not just its local splay tree).</li>
<li>It works by walking up the tree:
<ol>
<li>If it traverses a "dashed" edge (<code>isRoot == true</code>), it first splays the parent (<code>temp2</code>) to the top of its splay tree.</li>
<li>It then calls <code>SwitchPath(temp2)</code> to "cut" the old preferred path and "link" <code>temp</code>'s path.</li>
</ol>
</li>
<li>Finally, it splays the original node <code>ptr</code> to the root.</li>
</ul>

<h3>6️⃣ Search (<code>Search</code>)</h3>
<ul>
<li>Performs a standard BST search for a <code>key</code>.</li>
<li>If the key is found, it calls <code>MultiSplayAlgo</code> on the found node.</li>
<li>If the key is not found, it calls <code>MultiSplayAlgo</code> on the last node visited (the nearest neighbor), as per splay tree convention.</li>
</ul>

<h2>🧰 <b>Technologies & Libraries Used</b></h2>
<ul>
<li><b>C</b> (Programming Language)</li>
<li><code>stdio.h</code> (For <code>printf</code>, <code>scanf</code>)</li>
<li><code>stdlib.h</code> (For <code>malloc</code>)</li>
<li><code>stdbool.h</code> (For the <code>bool</code> type)</li>
</ul>

<h2>🚀 <b>How to Compile & Run</b></h2>

<h3>1. Compilation</h3>
<p>Save the code as <code>multisplay.c</code> and compile it using a C compiler like GCC:</p>
<pre><code>gcc multisplay.c -o multisplay</code></pre>

<h3>2. Execution</h3>
<p>Run the compiled program from your terminal:</p>
<pre><code>./multisplay</code></pre>

<h3>3. Menu Options</h3>
<p>The program will prompt you to enter the number of nodes. After creation, you have three options:</p>
<ul>
<li><b>1 -> Display the Tree</b>: Prints the value, parent, and <code>isRoot</code> status for every node.</li>
<li><b>2 -> Search an Element</b>: Prompts for a key, searches for it, and then performs the <code>MultiSplayAlgo</code> to restructure the tree.</li>
<li><b>3 -> Exit the Code</b>: Terminates the program.</li>
</ul>

<h2>👩‍💻 <b>Author</b></h2>
<p>
(Based on your previous projects)





<b>Vaishnavi Chaughule</b>
</p>
