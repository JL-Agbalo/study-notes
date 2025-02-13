## Algorithm Characteristics

- **Input**: Data fed into the algorithm.
- **Output**: Result produced by the algorithm.
- **Unambiguity**: Each step is clearly defined.
- **Finiteness**: Algorithm has a finite number of steps.
- **Effectiveness**: Each step contributes to the solution.
- **Generality**: Can solve various problems.

## Algorithm Flow

1. **Input**: Gather necessary data.
2. **Process**: Perform calculations or operations.
3. **Output**: Produce the final result.
4. **Decision Making**: Make choices based on conditions.
5. **Iteration**: Repeat steps until a condition is met.
6. **Termination**: Algorithm stops.

## Algorithm Complexity

### Time Complexity

Measures the time an algorithm takes to complete based on input size (e.g., O(1), O(n), O(n^2)).

### Space Complexity

Measures the memory an algorithm uses based on input size.

## Data Structures

### Linear Data Structures

Examples: Array, List, Queue, and Stack.

### Non-Linear Data Structures

Examples: Tree, Graph.

### Stack Data Structure

A stack is a simple data structure that works like a stack of plates. You add plates to the top and remove them from the top. The last plate added is the first one to be taken off.

- **LIFO (Last In First Out)**: The last item added is the first one removed.
- **Push**: Add an item to the top.
- **Pop**: Remove the top item.
- **Peek**: Look at the top item without removing it.
- **IsEmpty**: Check if the stack is empty.
- **isFull**: Check if stack is full.
- **size**: Returns the size of the stack.

Example in pseudocode:

```
stack.push(1)
stack.push(2)
stack.push(3)
print(stack.pop())  // Outputs: 3
print(stack.peek()) // Outputs: 2
```

### Queue Data Structure

A queue is a data structure that follows the First In First Out (FIFO) principle. The first item added is the first one removed.

- **FIFO (First In First Out)**: The first item added is the first one removed.
- **Enqueue**: Add an item to the end.
- **Dequeue**: Remove the item from the front.
- **Peek**: Look at the front item without removing it.
- **IsEmpty**: Check if the queue is empty.
- **IsFull**: Check if the queue is full.
- **Size**: Returns the size of the queue.

### Empty Queue

A queue with no elements. Dequeue operations result in an error or special value.

### Full Queue

A queue at maximum capacity. Enqueue operations result in an error or special value.

A limitation of the queue is that empty spaces are not reused until the queue is completely empty.

### Circular Queue

A circular queue is a data structure where data is queued in a circular manner. It also follows the principles of FIFO (First In First Out) and LILO (Last In Last Out).

This removes the limitation of the standard queue data structure where empty spaces are not reused until the queue is completely empty.

- **Enqueue**: Add an item to the end.
- **Dequeue**: Remove the item from the front.
- **Peek**: Look at the front item without removing it.
- **IsEmpty**: Check if the queue is empty.
- **IsFull**: Check if the queue is full.
- **Size**: Returns the size of the queue.

Example in pseudocode:

```
circularQueue.enqueue(1)
circularQueue.enqueue(2)
circularQueue.enqueue(3)
print(circularQueue.dequeue())  // Outputs: 1
print(circularQueue.peek())     // Outputs: 2
```
