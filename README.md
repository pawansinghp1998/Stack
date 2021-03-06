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


Q.2.(225).Implement a last in first out (LIFO) stack using only two queues. The implemented stack should support all the functions of a normal queue (push, top, pop, and empty).

Implement the MyStack class:

void push(int x) Pushes element x to the top of the stack.
int pop() Removes the element on the top of the stack and returns it.
int top() Returns the element on the top of the stack.
boolean empty() Returns true if the stack is empty, false otherwise.
Notes:

You must use only standard operations of a queue, which means only push to back, peek/pop from front, size, and is empty operations are valid.
Depending on your language, the queue may not be supported natively. You may simulate a queue using a list or deque (double-ended queue), as long as you use only a queue's standard operations.
 
 Example 1:
Input
["MyStack", "push", "push", "top", "pop", "empty"]
[[], [1], [2], [], [], []]
Output
[null, null, null, 2, 2, false]

Explanation
MyStack myStack = new MyStack();
myStack.push(1);
myStack.push(2);
myStack.top(); // return 2
myStack.pop(); // return 2
myStack.empty(); // return False

class MyStack {
Queue <Integer> q1=new LinkedList<Integer>();                                      //Here we are creating two queue
    Queue <Integer> q2=new LinkedList<Integer>();int c=0;
    /** Initialize your data structure here. */
    public MyStack() {
       this.c=0;
    }
    
    /** Push element x onto stack. */
    public void push(int x) {                                         //Adding element queue and with the help of variable c counting number of element in queue
        q1.add(x);
        c++;
    }
    
    /** Removes the element on top of the stack and returns that element. */
    public int pop() {
        int c1=c;int a1=0;
        while(c1>1)
        {
            int d=q1.poll();
            q2.add(d);                                           //We will remove all element except last element with help of while lopp
            c1--;
        }
        c=c-1;                                                  //As one element is poped out we will decreses the size of queue by one
        a1=q1.poll();                                           //Here we will extract last elemt also
        q1=q2;                                                  //we will restore all element in q1 except the pop out elemnt
        return a1;                                              // Here we will return poped out element
        
    }
    
    /** Get the top element. */
    public int top() {
        int c2=c;int a1=0;
        while(c2>1)
        {
            int d=q1.poll();
            q2.add(d);
            c2--;
        }
       a1=q1.poll();                                    
        q2.add(a1);                                           //Here in this case we will add last element also as it is peek operation
        q1=q2;
        return a1;                                           //we will return back top element
        
    }
    
    /** Returns whether the stack is empty. */
    public boolean empty() {
        if(c==0)                                            //If the number of element in queue is zero , queue is empty
        return true;
        else
            return false;
    }
}


Method 2:

class MyStack{
	Queue<Integer> s1 = new LinkedList<>();
	Queue<Integer> s2 = new LinkedList<>();

	public void push(int x) {
		s1.add(x);
		int i = 0;
		while(i < s1.size() - 1){                         //we will reverse storation order as loop will iterate one time less than number of element in queue
			s2.add(s1.remove());                             //So finally queue is stored as stack
			s1.add(s2.remove());
			i++;
		}
	}
	public int pop() {
		return s1.remove();
	}

	/** Get the top element. */
	public int top() {
		return s1.peek();
	}

	/** Returns whether the stack is empty. */
	public boolean empty() {
		return s1.isEmpty();
	}
}

Q.3.(232).Implement a first in first out (FIFO) queue using only two stacks. The implemented queue should support all the functions of a normal queue (push, peek, pop, and empty).
Implement the MyQueue class:
void push(int x) Pushes element x to the back of the queue.
int pop() Removes the element from the front of the queue and returns it.
int peek() Returns the element at the front of the queue.
boolean empty() Returns true if the queue is empty, false otherwise.

Input
["MyQueue", "push", "push", "peek", "pop", "empty"]
[[], [1], [2], [], [], []]
Output
[null, null, null, 1, 1, false]
Explanation
MyQueue myQueue = new MyQueue();
myQueue.push(1); // queue is: [1]
myQueue.push(2); // queue is: [1, 2] (leftmost is front of the queue)
myQueue.peek(); // return 1
myQueue.pop(); // return 1, queue is [2]
myQueue.empty(); // return false

class MyQueue {
    Stack<Integer> s1=new Stack<>();
    Stack<Integer> s2=new Stack<>();
int c;
    /** Initialize your data structure here. */
    public MyQueue() {
        this.c=0;
    }
    
    /** Push element x to the back of queue. */
    public void push(int x) {
        s1.add(x);
        c++;
        
       
    }
    
    /** Removes the element from in front of queue and returns that element. */
    public int pop() {
        int c1=c;
        while(c1>1)
        {
            s2.add(s1.pop());                             //In s2 element will be stored in reverse order ,but last element will not be stored 
            c1--;
        }
        c--;
        int k=s1.pop();                                 //returning first element if we foloow queue data structure
        int c2=0;
        while(c2<c)
        {
            s1.add(s2.pop());                            //Restoring all element of s2 in in same order as that of s1 previously but missing one element that is popped out
            c2++;
        }
        return k;
        
        
    }
    
    /** Get the front element. */
    public int peek() {
         int c1=c;
        while(c1>1)
        {
            s2.add(s1.pop());
            c1--;
        }
        int k=s1.peek();                                          //returning first eleent entered in stack that is first element to be popped out if we follow queue data                                                                            structure
        int c2=1;
        while(c2<c)
        {
            s1.add(s2.pop());
            c2++;
        }
        return k;
        
    }
    
    /** Returns whether the queue is empty. */
    public boolean empty() {
        if(c==0)
            return true;
        else
            return false;
    }
}

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue obj = new MyQueue();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.peek();
 * boolean param_4 = obj.empty();
 */

Method 2:
import java.util.*;
class MyQueue {
    Stack<Integer> S1;
    Stack<Integer> S2;

    /** Initialize your data structure here. */
    public MyQueue() {
        S1 = new Stack();
        S2 = new Stack();
    }
    
    /** Push element x to the back of queue. */
    public void push(int x) {
        S1.push(x);
    }
    
    /** Removes the element from in front of queue and returns that element. */
    public int pop() {
        if(S2.empty()){
            while(!S1.empty()){
                S2.push(S1.pop());
            }
        }
        return S2.pop();
    }
    
    /** Get the front element. */
    public int peek() {
        if(S2.empty()){
            while(!S1.empty()){
                S2.push(S1.pop());
            }
        }
        return S2.peek();
    }
    
    /** Returns whether the queue is empty. */
    public boolean empty() {
        return S1.isEmpty() && S2.isEmpty();
    }
}


