# Breadth first search

Pseudocode:
1. Start by visiting vertex 3, the source, setting its distance to 0.
2. Then visit vertices 2 and 6, setting their distance to 1 and their predecessor to vertex 3.
3. Start visiting from vertices at distance 1 from the source, beginning with vertex 2. From vertex 2, visit vertices 4 and 5, setting their distance to 2 and their predecessor to vertex 2. Don't visit vertex 3, because it has already been visited.
4. From vertex 6, don't visit vertex 5, because it was just visited from vertex 2, and don't visit vertex 3, either.
5. Now start visiting from vertices at distance 2 from the source. Start by visiting from vertex 4. Vertex 2 has already been visited. Visit vertex 1, setting its distance to 3 and its predecessor to vertex 4.
6. From vertex 5, don't visit any of its neighbors, because they have all been visited.
7. Now start visiting from vertices at distance 3 from the source. The only such vertex is vertex 1. Its neighbors, vertices 4 and 5, have already been visited. But vertex 0 has not. Visit vertex 0, setting its distance to 4 and its predecessor to vertex 1.
8. Now start visiting from vertices at distance 4 from the source. That's just vertex 0, and its neighbor, vertex 1, has already been visited. We're done!

```js
var Queue = function() {
    this.items = [];
};
Queue.prototype.enqueue = function(obj) {
    this.items.push(obj);
};
Queue.prototype.dequeue = function() {
    return this.items.shift();
};
Queue.prototype.isEmpty = function() {
    return this.items.length === 0;
};

/*
 * Performs a breadth-first search on a graph
 *
 * @param {array} graph - Graph, represented as adjacency lists.
 * @param {number} source - The index of the source vertex.
 * @returns {array} Array of objects describing each vertex, like
 *     [{distance: _, predecessor: _ }]
 */
var doBFS = function(graph, source) {
    var bfsInfo = [];

    for (var i = 0; i < graph.length; i++) {
        bfsInfo[i] = {
            distance: null,
            predecessor: null
        };
    }

    bfsInfo[source].distance = 0;

    var queue = new Queue();
    queue.enqueue(source);

    // Traverse the graph
    // As long as the queue is not empty:
    while (! queue.isEmpty()) {
        //  Repeatedly dequeue a vertex u from the queue.
        var u = queue.dequeue();

        //  For each neighbor v of u that has not been visited:
        for (var v = 0; v < graph[u].length; v++) {
            var neighbour = graph[u][v];

            if (bfsInfo[neighbour].distance === null) {
                // Set distance to 1 greater than u's distance
                bfsInfo[neighbour].distance = bfsInfo[u].distance + 1;

                // Set predecessor to u
                bfsInfo[neighbour].predecessor = u;

                // Enqueue v
                queue.enqueue(neighbour);
            }
        }
    }

    return bfsInfo;
};


var adjList = [
    [1],
    [0, 4, 5],
    [3, 4, 5],
    [2, 6],
    [1, 2],
    [1, 2, 6],
    [3, 5],
    []
    ];
var bfsInfo = doBFS(adjList, 3);
```
