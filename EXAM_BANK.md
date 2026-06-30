# Exam Bank

This file is the authoring workspace for stronger quizzes and future final exams.

The live app stays self-contained in `index.html`.

Use this file to:

- draft harder questions without touching runtime code
- organize questions by lesson and difficulty
- review wording with students or teachers
- promote polished questions into `index.html` later

## Difficulty Model

Use three cumulative levels:

- `Core`: must-know facts, definitions, invariants, basic complexity recall
- `Standard`: comparisons, exam traps, selecting the right structure or algorithm
- `Challenge`: scenario reasoning, edge cases, implementation tradeoffs, deeper analysis

Recommended study presets:

- `Core only`: fast review before an exam
- `Core + Standard`: default study mode
- `All levels`: mastery mode

## Authoring Rules

- Prefer scenario-based questions over pure definition checks when possible
- Explain every answer, including why tempting wrong answers are wrong
- Use technical naming consistently
- In Hebrew, keep the Hebrew term and include the English CS name where helpful
- Include implementation-aware questions, not only complexity recall
- Make harder questions deeper, not just trickier

## Question Template

```text
Lesson:
Difficulty:
Type: MC / TF
Prompt:
Choices:
- A
- B
- C
- D
Correct:
Explanation:
Notes:
```

## Lesson Buckets

### Sorting

#### Core

- What property means equal keys keep their original relative order?
- Which comparison sort has worst-case `O(n log n)` and uses extra memory?

#### Standard

- Why is quicksort often faster in practice even though its worst case is `O(n^2)`?
- When would counting sort beat merge sort?

#### Challenge

- You need stable sorting for records by one field after a previous sort by another field. Which algorithms fit and why?
- Your keys are small integers in a narrow range, but memory is limited. Which sorting family is attractive, and what tradeoff appears?

### Search and Membership

#### Core

- When is binary search valid?
- What kind of questions is Union-Find designed to answer?

#### Standard

- Why is binary search not automatically `O(log n)` on a linked list?
- What is the role of path compression?

#### Challenge

- You receive repeated connectivity queries and occasional union operations. Why is Union-Find a better fit than repeated graph traversal?
- Compare linear search, binary search, and hashing for different input constraints.

### Linear Structures

#### Core

- Which structure is LIFO?
- Which structure is FIFO?

#### Standard

- Why is an array better than a linked list for random access?
- Why is a priority queue not just a normal queue?

#### Challenge

- You need fast indexing plus frequent inserts near the front. Which structure hurts and why?
- For BFS, why is a queue the natural fit while a stack changes the traversal behavior?

### Trees

#### Core

- What BST invariant must hold?
- Why do AVL rotations exist?

#### Standard

- Why can a plain BST degrade to `O(n)`?
- Why is a heap not a BST?

#### Challenge

- You need ordered traversal and predictable worst-case lookup. Which tree family fits best and why?
- Why can a splay tree be attractive even though one operation may be expensive?

### Hashing

#### Core

- What is a collision?
- What does expected `O(1)` mean?

#### Standard

- Compare chaining and open addressing.
- Why can linear probing create clustering?

#### Challenge

- You need fast lookup but also sorted iteration. Why is a hash table not enough by itself?
- Why must the second step in double hashing not be zero?

### Heaps and Priority Queues

#### Core

- What does a min-heap guarantee at the root?
- What are the usual costs of `peek`, `insert`, and `extract-min`?

#### Standard

- Why is a heap only partially sorted?
- Why is `build heap` linear?

#### Challenge

- You repeatedly insert events and always need the next event with minimum time. Why is a heap the right mental model?
- Why are binomial heaps mainly interesting when merge is a first-class operation?

## Refined Drafts

These are stronger candidate questions that can be promoted into `index.html` after review.

### Linear Structures

#### Standard

```text
Lesson: Linear Structures
Difficulty: Standard
Type: MC
Prompt: You need frequent random access by index to the middle of a collection. Which structure is the strongest default fit?
Choices:
- Array
- Singly linked list
- Queue
- Stack
Correct: Array
Explanation: Arrays support direct address arithmetic, so indexed access is O(1). A linked list must walk node by node, which makes middle access O(n).
Notes: Better than a pure definition question because it tests structure choice.
```

```text
Lesson: Linear Structures
Difficulty: Standard
Type: MC
Prompt: A priority queue is different from a normal queue because it removes items by:
Choices:
- Arrival order only
- Index position
- Priority
- Most recent insertion
Correct: Priority
Explanation: A normal queue is FIFO, but a priority queue removes the item with highest or lowest priority, regardless of arrival order.
Notes: Good replacement for very easy FIFO/LIFO-only checks.
```

#### Challenge

```text
Lesson: Linear Structures
Difficulty: Challenge
Type: MC
Prompt: A system needs O(1) indexing for reads, but also frequent inserts near the front. Which warning matters most?
Choices:
- Arrays make front inserts expensive because elements shift
- Linked lists give O(1) indexing by position
- Queues keep the whole collection sorted
- Stacks support efficient range queries
Correct: Arrays make front inserts expensive because elements shift
Explanation: Arrays are great for indexed reads, but inserting near the front usually shifts many elements, often costing O(n).
Notes: Good implementation-tradeoff question.
```

### Hashing

#### Standard

```text
Lesson: Hashing
Difficulty: Standard
Type: MC
Prompt: Why can linear probing slow down over time even when many table slots are still empty?
Choices:
- It creates clusters of occupied slots
- It destroys sorted order in a BST
- It increases recursion depth
- It forces binary search
Correct: It creates clusters of occupied slots
Explanation: Linear probing can produce primary clustering, where long runs of occupied positions make future probes longer.
Notes: Stronger than just asking for the name of a collision method.
```

```text
Lesson: Hashing
Difficulty: Standard
Type: TF
Prompt: Expected O(1) lookup in a hash table means every single lookup is guaranteed to take constant time.
Choices:
- True
- False
Correct: False
Explanation: Expected O(1) means the average behavior under the hashing assumptions is constant, not that every individual operation is guaranteed constant.
Notes: Good exam-trap wording.
```

#### Challenge

```text
Lesson: Hashing
Difficulty: Challenge
Type: MC
Prompt: You need fast lookup, but you also need to print keys in sorted order at the end of each hour. Which answer is best?
Choices:
- Use only a hash table
- Use a balanced search tree
- Use only a stack
- Use Union-Find
Correct: Use a balanced search tree
Explanation: A hash table is strong for expected O(1) lookup, but it does not maintain sorted order. A balanced tree supports lookup plus ordered traversal.
Notes: Good cross-topic comparison question.
```

```text
Lesson: Hashing
Difficulty: Challenge
Type: MC
Prompt: In double hashing, why must the second hash value not be 0?
Choices:
- Because the probe would stop moving
- Because the table becomes sorted
- Because collisions disappear
- Because resizing becomes impossible
Correct: Because the probe would stop moving
Explanation: If the second step is 0, every retry lands on the same position, so probing cannot explore the table.
Notes: Implementation-aware and still short enough for the app.
```

### Heaps and Priority Queues

#### Standard

```text
Lesson: Heaps and Priority Queues
Difficulty: Standard
Type: TF
Prompt: A heap is useful when you repeatedly need the next highest-priority item, even if the rest of the structure is not fully sorted.
Choices:
- True
- False
Correct: True
Explanation: A heap guarantees the top-priority item at the root, which is exactly what repeated priority removal needs.
Notes: Better than simply asking whether a heap is sorted.
```

```text
Lesson: Heaps and Priority Queues
Difficulty: Standard
Type: MC
Prompt: Why is searching for an arbitrary value inside a heap usually not fast?
Choices:
- Heap order is only partial
- The root is always random
- Heaps do not use comparisons
- Heaps forbid duplicate values
Correct: Heap order is only partial
Explanation: A heap guarantees only parent-child priority order. It does not keep all values globally sorted like a BST or sorted array.
Notes: Good conceptual distinction question.
```

#### Challenge

```text
Lesson: Heaps and Priority Queues
Difficulty: Challenge
Type: MC
Prompt: A simulator keeps inserting future events and always needs the smallest timestamp next. Which structure best matches that workflow?
Choices:
- Min-heap
- Stack
- Hash table
- Union-Find
Correct: Min-heap
Explanation: A min-heap gives O(1) access to the smallest timestamp and O(log n) updates as new events are inserted.
Notes: Strong real-world scenario question.
```

```text
Lesson: Heaps and Priority Queues
Difficulty: Challenge
Type: MC
Prompt: Why is build-heap O(n) instead of O(n log n) in the standard bottom-up algorithm?
Choices:
- Most nodes are near the leaves and move only a little
- Heapify never uses comparisons
- The root is inserted only once
- Arrays automatically sort children
Correct: Most nodes are near the leaves and move only a little
Explanation: Bottom-up heap construction does not pay full height for every node. Most nodes sit low in the tree, so the total work sums to O(n).
Notes: Good higher-difficulty reasoning question.
```

## Recommended First Promotions

If we upgrade the live app gradually, these are the best first replacements:

- Replace one easy priority-queue recall question with the event-simulator min-heap scenario
- Replace one easy hashing recall question with the clustering or expected-O(1) trap question
- Replace one easy array/list recall question with the indexing-vs-front-insert tradeoff question

## Combined Exam Ideas

### Standard

- You need fast lookup by key and do not care about order. What should you try first?
- You need undo support. Which structure matches the behavior?
- You need repeated minimum extraction. Which structure fits?

### Challenge

- Choose between hash table, AVL tree, and heap for a task that needs fast lookup, sorted traversal, and predictable worst-case behavior.
- Explain why binary search, hashing, and BSTs solve different versions of "search."
- Compare Union-Find and BFS/DFS for connectivity questions under repeated queries.

## Promotion Checklist

Before moving a question into `index.html`, check:

- Is the wording short enough for the app UI?
- Is the explanation strong enough to teach, not just grade?
- Does the question fit the intended difficulty level?
- Does it avoid accidental ambiguity?
- Does it add coverage instead of repeating an existing item?
