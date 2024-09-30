# Design-a-Stack-With-Increment-Operation


Design a stack that supports increment operations on its elements.

Implement the CustomStack class:

CustomStack(int maxSize) Initializes the object with maxSize which is the maximum number of elements in the stack.
void push(int x) Adds x to the top of the stack if the stack has not reached the maxSize.
int pop() Pops and returns the top of the stack or -1 if the stack is empty.
void inc(int k, int val) Increments the bottom k elements of the stack by val. If there are less than k elements in the stack, increment all the elements in the stack.
 

Example 1:

Input
["CustomStack","push","push","pop","push","push","push","increment","increment","pop","pop","pop","pop"]
[[3],[1],[2],[],[2],[3],[4],[5,100],[2,100],[],[],[],[]]
Output
[null,null,null,2,null,null,null,null,null,103,202,201,-1]
Explanation
CustomStack stk = new CustomStack(3); // Stack is Empty []
stk.push(1);                          // stack becomes [1]
stk.push(2);                          // stack becomes [1, 2]
stk.pop();                            // return 2 --> Return top of the stack 2, stack becomes [1]
stk.push(2);                          // stack becomes [1, 2]
stk.push(3);                          // stack becomes [1, 2, 3]
stk.push(4);                          // stack still [1, 2, 3], Do not add another elements as size is 4
stk.increment(5, 100);                // stack becomes [101, 102, 103]
stk.increment(2, 100);                // stack becomes [201, 202, 103]
stk.pop();                            // return 103 --> Return top of the stack 103, stack becomes [201, 202]
stk.pop();                            // return 202 --> Return top of the stack 202, stack becomes [201]
stk.pop();                            // return 201 --> Return top of the stack 201, stack becomes []
stk.pop();                            // return -1 --> Stack is empty return -1.
 

Constraints:

1 <= maxSize, x, k <= 1000

0 <= val <= 100

At most 1000 calls will be made to each method of increment, push and pop each separately.

# SOLUTION

Approach
Data Structures:
Use two lists: stack to store the elements and inc to track delayed increments.
Operations:
Push: Add x to stack if not full, and append 0 to inc.
Pop: Return the top of stack with any increment applied, propagate the increment down.
Increment: Add val to the k-th element in inc to handle bottom k increment efficiently.
Complexity
Time complexity:
O(1)

Space complexity:
O(N)

# JAVA CODE

class CustomStack {

    private int n;
    
    private Stack<Integer> stack;
    
    private List<Integer> inc;

    public CustomStack(int n) {
    
        this.n = n;
        
        this.stack = new Stack<>();
        
        this.inc = new ArrayList<>();
        
    }

    public void push(int x) {
    
        if (stack.size() < n) {
        
            stack.push(x);
            
            inc.add(0);
            
        }
        
    }

    public int pop() {
    
        if (stack.isEmpty()) return -1;
        
        if (inc.size() > 1) inc.set(inc.size() - 2, inc.get(inc.size() - 2) + inc.get(inc.size() - 1));
        
        return stack.pop() + inc.remove(inc.size() - 1);
    }

    public void increment(int k, int val) {
    
        if (!stack.isEmpty()) {
        
            int index = Math.min(k, inc.size()) - 1;
            
            inc.set(index, inc.get(index) + val);
            
        }
        
    }
    
}
