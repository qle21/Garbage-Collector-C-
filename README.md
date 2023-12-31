# Garbage Collection ReadMe

This project focuses on implementing a Garbage Collector (GC) utilizing a Mark and Sweep algorithm. The algorithm is divided into two main phases: the Mark Phase and the Sweep Phase.

## Mark Phase

### 1. Overview
- **Objective:** Identify and mark objects that are still in use.
- **Methodology:** Deep search starting from a root set of references held in local variables on the Stack or global variables.
- **Root References:** The search begins with a set of root references, and any object with references to these roots is marked as "alive."
- **Handling Circular References:** Circular references are not problematic if they are not directly accessible from the root.

### 2. Execution
- **Marking Objects:** The Garbage Collector marks objects by setting their "mark bit" to true.
- **Object Accessibility:** Objects that hold references to other objects are marked as alive.
- **Application Threads:** During the Mark Phase, application threads need to be stopped to prevent changes to object states.

## Sweep Phase

### 1. Overview
- **Objective:** Remove unmarked objects from memory to free up HEAP space.
- **Unmarked Objects:** All unmarked objects from the Mark Phase are removed from memory.
- **Fragmentation Issue:** Fragmentation can occur, potentially causing memory allocation failures.
  
### 2. Addressing Fragmentation
- **is_pointer Function:** Introduced to determine if a potential pointer points to an in-use block in the heap.
- **Binary Search:** The `isPtr(ptr p)` function performs a binary search of allocated blocks to identify valid pointers.
  
### 3. Execution
- **Heap Space Management:** Sweeping phase ensures efficient use of HEAP space by collecting garbage.
- **Memory Allocation:** Fragments created during sweeping might impact memory allocation; the is_pointer function addresses this issue.

## Implementation Details

- **Marking Function:** The marker function is called for each root node during the Mark Phase.
- **Recursive Traversal:** The `walk_region_and_mark` function recursively marks accessible child nodes.
- **Unreachable Blocks:** At the end of the Mark Phase, unmarked allocated blocks are identified as unreachable and treated as garbage during the Sweep Phase.

## Usage and Considerations

- **Memory Management:** Garbage Collection is crucial for effective memory management.
- **Root Nodes:** Proper identification of root nodes is essential for a comprehensive Mark Phase.
- **Stopping Application Threads:** Ensure application threads are halted during the Mark Phase to maintain consistency.
- **Fragmentation Concerns:** Address potential fragmentation issues by utilizing the `is_pointer` function.
- **Circular References:** Circular references are managed effectively during the Mark Phase.

**Note:** The Garbage Collector is designed to enhance memory efficiency by identifying and collecting unreachable objects, optimizing the use of memory resources.

Happy Garbage Collecting!
