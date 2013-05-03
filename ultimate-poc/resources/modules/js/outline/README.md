**WORK IN PROGRESS**: for now a basic outline implementation is made in the global js modules, displaying every node of the AST without any custom logic.

This is a try to bring an outline implementation for every node type of an AST. Here we rely on the Mozilla Parser APi specification.

With a depth-first tree traversing, this should work. See what functions actually need:

* links to children for sure
* links to parent too?

# Model

For us, an outline is represented by a simple tree, and targets a GUI.

The model for that is extremly simple: a node has a label (a string) and an ordered list of children nodes, optional, and possibly empty.

# Outline

## Internal

How to build an outline tree?

### Traversal

The AST traversal MUST be depth first.

Indeed, an outline view summarizes the program (i.e. the AST), not by showing every syntactic part of the program, but a more compact and semantic view.

Therefore, some nodes will be squashed to simplify it, resulting in one node with a meaningful label.

Moreover, in this case the knowledge of parents nodes is not required, whereas the knowledge of children nodes is mandatory!

### Transformation

An AST node is an object with a set of properties.

Some of these properties are recurrent and describes the node itself, while all the others depends on the node type: some of them are the children node while others are some properties.

### Pending


But this requires the children node to be processed first, so that a parent node can check if it can compute a proper label or keep children as is.

Rule: if a node has multiple children, just keep them, otherwise think about using the unique child label to build the current node label if relevant, otherwise keep the child as is.