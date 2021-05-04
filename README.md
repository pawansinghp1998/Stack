Q.1(155).Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

Implement the MinStack class:

MinStack() initializes the stack object.
void push(val) pushes the element val onto the stack.
void pop() removes the element on the top of the stack.
int top() gets the top element of the stack.
int getMin() retrieves the minimum element in the stack.
 Input
["MinStack","push","push","push","getMin","pop","top","getMin"]
[[],[-2],[0],[-3],[],[],[],[]]

Output
[null,null,null,null,-3,null,0,-2]

Explanation
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin(); // return -3
minStack.pop();
minStack.top();    // return 0
minStack.getMin(); // return -2
 
 
 class MinStack {
    listnode top;
    int length;
    
       
        public class listnode
        {
             listnode next;
        int data;
        public listnode(int data)
         {
            this.data=data;
            this.next=null;
        }
    }

    /** initialize your data structure here. */
    public MinStack() {
        top=null;
       
       
    }
    
    public void push(int val) {
        
        listnode newnode=new listnode(val);
        
            newnode.next=top;
            top=newnode;
    }
    
    public void pop() {
       if(top!=null)
        top=top.next;
        
    }
    
    public int top() {
        if(top==null)
            return Integer.MIN_VALUE;
        else
        return top.data;
        
    }
    
    public int getMin() {
        int min=Integer.MAX_VALUE;
        listnode temp=top;
        while(temp!=null)
        {
            if(min>temp.data)
            {
                min=temp.data;
                temp=temp.next;
            }
            else
                temp=temp.next;
        }
        return min;
    }
}
