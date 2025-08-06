## Define a Linked List

```java
public class ListNode {
    // the value of the Node
    int val;
    
    // the next Node
    ListNode next;
    
    // Constructor(default)
    public ListNode(){
        
    }
    
    // Constructor(one parameter)
    public ListNode(int val){
        this.val = val
    }
    
    // Constructor(two para)
    public ListNode(int val, ListNode next){
        this.val = val;
        this.next = next;
    }
    
}
```

