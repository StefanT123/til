# Djikstra

```js
let givenNodes = {
  start: {a: 2, b: 3, c: 5},
  a: {d: 4, e: 5},
  b: {d: 6, f: 1},
  c: {f: 8},
  d: {e: 1, finish: 5, f: 2},
  f: {d: 2, finish: 1},
  e: {finish: 9, d: 1},
  finish: {}
};
let visitedNodes = [];
let nodes = [];
let pathArray = [];
// set distance of the start node to 0
nodes.push({name: 'start', distance: 0});

/**
 * Set distances to every other node that's not
 * start node to Infinity.
 */
function setDistance() {
    for (let i in givenNodes) {
        if (i !== 'start') {
            nodes.push({name: i, distance: Infinity});
        }
    }
}

/**
 * Find the shortest path between two distances.
 *
 * @param  {String} from
 * @param  {String} to
 * @param  {Array} pathArray
 * @return {Array}
 */
function findPath(from, to, pathArray) {
    let path = [];

    while (to !== from) {
        path.push(to);
        to = pathArray[to];
    }
    path.push(from);

    return path.reverse();
}

/**
 * Find the shortest distance to some node.
 *
 * @param  {String} toNode
 * @return {Object}
 */
function djikstra(toNode) {
    // check only nodes that haven't been visited yet
    let filterredWeights = nodes.filter(node => ! visitedNodes.includes(node.name));

    // if all nodes are visited, return the node that we are looking for
    // and the shortest path
    if (! filterredWeights.length) {
        return [
            nodes.find(node => node.name === toNode),
            findPath('start', toNode, pathArray)
        ];
    }

    // sort the nodes by distance, so we can get the node with the smallest distance
    filterredWeights.sort((a, b) => a.distance - b.distance);
    let smallestDistNode = filterredWeights[0];
    let currentNode = givenNodes[smallestDistNode.name];

    // loop through every neighbour node of the smallest distance node
    Object.entries(currentNode).forEach(neighbours => {
        let nodeName = neighbours[0];
        let nodeValue = neighbours[1];
        // add the distance of the node and the weight of the node
        let absoluteDistance = smallestDistNode.distance + nodeValue;

        let nodeIndex = nodes.findIndex(node => node.name === nodeName);

        // if the added distance is smaller than the node weight
        // set that distance as the node distance
        if (absoluteDistance < nodes[nodeIndex].distance) {
            nodes[nodeIndex].distance = absoluteDistance;
            pathArray[nodeName] = smallestDistNode.name;
        }
    });

    // push node to the visited array
    visitedNodes.push(smallestDistNode.name);

    return djikstra(toNode);
}

setDistance();
djikstra('finish');
```
