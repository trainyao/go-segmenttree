# go-segmenttree
A extendable segment tree go implement.

## Why 'extendable'?

- `Node` struct can save any kind of data, thus you can use any kind of data to build your tree.
- A tree pass through `SegmentTreeUpdateFunc` type function you set when creating a tree, 
    to calculate or update non-leaf tree node data. In other lib this logic may be hard coded 
    (for example, non-leaf node data is the sum of left & right sub-tree data), but in this implement
    you can plug your own logic in the tree. 

## Usage

1. create a tree
    ```go
    package main
    
    import (
        "fmt"
        "github.com/trainyao/segmenttree"
    )
    
    func main() {
        nodes := []segmenttree.Node{}
        // fill node data
        updateFunc := func(leftChildData, rightChildData interface{}) (currentNodeData interface{}) {
            // implement your logic
            return leftChildData.(int) + rightChildData.(int)
        }
    
        tree := segmenttree.NewTree(nodes, updateFunc)
    }
    ```

2. use segment to search data (pending to implement, PR is welcomed~)

3. finding leaf node and parents

    ```go
    package main
    
    import (
    	"fmt"
    	"github.com/trainyao/segmenttree"
    )
    
    func main() {
        // ...
        var err error
        leaf, err := tree.Leaf(0)
        fmt.Print(leaf.Value.(int))
    
        parent := tree.FindParent(leaf)
    }
    ```
   
4. update tree data
    ```go
    package main
    
    import (
    	"fmt"
    	"github.com/trainyao/segmenttree"
    )
    
    func main() {
        // ...
        newData := 123
        leaf.Value = newData
        tree.Update(leaf)
    }
    ```
