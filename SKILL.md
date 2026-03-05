name: logic-sculptor
version: 1.3.0
description: Crafts elegant algorithmic structures with mathematical precision
author: SMOUJBOT
type: design
dependencies:
  - python>=3.9
  - numpy>=1.24.0
  - graphviz>=0.20.0
  - rich>=13.0.0
  - pythonds3
  - pygraphviz
required_tools:
  - gcc
  - dot (graphviz)
  - pytest
environment_vars:
  - LOGIC_SCULPTOR_MODE=normal|strict|experimental
  - LOGIC_SCULPTOR_COMPLEXITY=O(n),O(n^2),O(logn),O(nlogn)
  - LOGIC_SCULPTOR_STYLE=imperative|functional|object-oriented
  - LOGIC_SCULPTOR_TEST_SEED=integer
tags:
  - sculpting
  - algorithms
  - elegance
  - structure
  - complexity
  - optimization
```

# Logic Sculptor

## Purpose

Logic Sculptor transforms abstract computational problems into mathematically precise, elegant algorithmic implementations. It goes beyond basic code generation to create algorithms with optimal time/space complexity guarantees, formal correctness reasoning, and aesthetic structural clarity.

Real use cases:
- Convert "find all prime numbers up to N using Sieve of Eratosthenes" into memory-efficient, cache-friendly implementation with complexity annotations
- Transform "optimize dynamic programming solution for longest common subsequence" into iterative bottom-up version with space optimization proof
- Design custom graph traversal algorithm with provable termination and complexity analysis
- Sculpt divide-and-conquer algorithm (like Karatsuba multiplication) with balanced recursion trees and base case justification
- Refactor imperative spaghetti code into pure functional transformations with immutability guarantees
- Generate mathematical proof sketches for algorithm correctness alongside implementation

## Scope

### Core Commands

#### `logic-sculptor design <problem>` - Generate algorithm from specification
```
Flags:
  --complexity <target>     Target Big-O complexity (e.g., "O(nlogn)")
  --style <pattern>         Algorithmic pattern: "dp", "divide-conquer", "greedy", "backtrack", "graph", "tree"
  --structure <type>        Data structure focus: "array", "linked-list", "heap", "bst", "trie"
  --prove                   Generate correctness lemma sketches
  --visualize               Output Graphviz .dot of algorithm flow
  --lang <language>         Target: "python", "rust", "typescript", "c", "go"
  --constraints <text>      Physical constraints (e.g., "in-place", "constant extra space")

Example: logic-sculptor design "maximum subarray sum" --style divide-conquer --prove --visualize --lang rust
```

#### `logic-sculptor optimize <algorithm_file>` - Refine existing algorithm
```
Flags:
  --target <metric>         Optimize for: "time", "space", "both", "cache"
  --iterations <n>          Number of refinement passes (1-10)
  --preserve <property>     Don't change: "interface", "api", "signature"
  --explain                 Generate optimization rationale document
  --ablation               Test each transformation separately

Example: logic-sculptor optimize ./algorithms/sort.py --target both --iterations 3 --explain
```

#### `logic-sculptor verify <algorithm_file> <test_cases>` - Formal correctness check
```
Flags:
  --property <name>         Property to verify: "termination", "partial-correctness", "total-correctness", "loop-invariant"
  --mode <depth>            Verification depth: "symbolic", "bounded", "exhaustive"
  --timeout <seconds>       Verification timeout (default 30)
  --smt-solver <engine>     Solver: "z3", "cvc5", "none"

Example: logic-sculptor verify ./binary_search.py test_cases.json --property total-correctness --mode symbolic
```

#### `logic-sculptor benchmark <algorithm> <inputs>` - Empirical performance analysis
```
Flags:
  --samples <n>             Number of runs per input (default 100)
  --warmup <n>              Warmup iterations (default 10)
  --memory                  Track memory usage (requires psutil)
  --profile <type>          Profiling: "cprofile", "line", "none"
  --reference <file>        Compare against reference implementation

Example: logic-sculptor benchmark quicksort --samples 1000 --memory --profile cprofile
```

#### `logic-sculptor explain <algorithm_file>` - Deep analysis with mathematical rigor
```
Flags:
  --complexity-analysis     Detailed Big-O derivation
  --proof-outline           Correctness argument structure
  --edge-cases              Systematic edge case enumeration
  --invariants              Loop/recursion invariants
  --history                 Similar algorithms from literature

Example: logic-sculptor explain dijkstra.py --complexity-analysis --proof-outline --invariants
```

#### `logic-sculptor scaffold <problem>` - Interactive guided design
```
Interactive mode: asks clarifying questions about constraints, assumptions, and requirements before generating.

Example: logic-sculptor scaffold "detect cycle in directed graph"
```

#### `logic-sculptor compare <algorithm1> <algorithm2>` - Structural and performance comparison
```
Flags:
  --complexity              Compare theoretical complexity
  --empirical               Benchmark both on same inputs
  --tradeoffs               Highlight pros/cons matrix
  --visual-diff             Visual representation of differences

Example: logic-sculptor compare bubble_sort.py merge_sort.py --complexity --empirical --tradeoffs
```

#### `logic-sculptor patterns list|show <pattern_name>` - Algorithmic pattern library
```
Example: logic-sculptor patterns show "sliding-window"
Example: logic-sculptor patterns list
```

## Detailed Work Process

### 1. Design Phase
```
   logic-sculptor design <specification> --complexity <target> --style <pattern>
   ↓
   [Sculptor parses specification, identifies core computational problem]
   [Checks pattern library for known solutions]
   [Generates draft algorithm meeting target complexity]
   [Annotates with time/space complexity at each step]
   [If --prove: sketches preconditions, postconditions, invariants]
   [If --visualize: creates algorithm flow Graphviz diagram]
   ↓
   Output: <problem>_solution.<ext> + <problem>_analysis.md + optional <problem>.dot
```

### 2. Optimization Phase
```
   logic-sculptor optimize <file> --target <metric> --iterations <n>
   ↓
   [Parses existing algorithm, constructs IR (intermediate representation)]
   [Applies transformation passes:
    - Inlining small functions
    - Loop unrolling (controlled)
    - Dead code elimination
    - Constant propagation
    - Data structure substitution (list→array, set→bitmap)
    - Memoization opportunities
    - Tail recursion elimination
    - Space-time tradeoffs]
   [Each pass validated with property tests]
   [Selects best variant by --target metric]
   [Generates optimization report]
   ↓
   Output: <file>_optimized.<ext> + optimization_log.md
```

### 3. Verification Phase
```
   logic-sculptor verify <file> <tests.json> --property <prop> --mode <depth>
   ↓
   [Loads algorithm and test specification]
   [Extracts function signature and contracts]
   [Builds verification condition formulas]
   [If mode=symbolic: invokes Z3/CVC5 to prove]
   [If mode=bounded: checks all inputs up to bound]
   [If mode=exhaustive: full state space exploration (limited size)]
   [Generates proof sketch or counterexample]
   ↓
   Output: verification_result.yaml + counterexamples/ (if failed)
```

### 4. Benchmarking Phase
```
   logic-sculptor benchmark <algo> --samples <n> --memory --profile <type>
   ↓
   [Generates input suite scaling from small to large]
   [Compiles/runs algorithm with instrumentation]
   [Collects: wall time, CPU time, memory RSS, cache misses (perf if available)]
   [Fits scaling curves to infer empirical complexity]
   [If --reference: computes speedup ratios]
   [Produces: benchmark_results.json, plots/ (if matplotlib)]
   ↓
   Output: <algo>_benchmark_report.md + results.csv + plots/
```

## Golden Rules

1. **Complexity Preservation**: Never generate algorithm exceeding declared `--complexity` target. If pattern cannot achieve target, abort with clear explanation.

2. **Proof Positive**: When `--prove` flag set, every loop must have explicit invariant, every recursive function must have base case and decreasing argument justification.

3. **No Hidden Constants**: Assumptions about input size, value ranges, or hardware must be explicit. Avoid "for practical purposes" justifications for theoretical claims.

4. **Determinism Guarantee**: Given same inputs, algorithm must produce identical outputs every run. Randomness only allowed with documented seed parameter.

5. **Minimalism**: Between two correct solutions, prefer fewer lines, simpler control flow, fewer special cases. Elegance = correctness + simplicity + optimal complexity.

6. **Explicit State**: Mutable state must be clearly marked. Prefer pure functions where feasible. Side effects documented in function docstring.

7. **Edge Case Hygiene**: Every boundary condition (empty input, single element, max/min values, duplicates) must be explicitly handled and tested.

8. **Resource Bounds**: Space complexity analysis includes stack depth for recursion, not just heap allocations.

9. **No Blackbox Magic**: External library calls must be justified (e.g., "heapq ensures O(log n) push/pop"). Reimplement if library obscures complexity.

10. **Reproducibility**: All random inputs generated with documented seeds. All benchmarks record git commit of tested code.

## Examples

### Example 1: Design with Proof
```
User input:
  logic-sculptor design "find kth largest element in unsorted array" \
    --complexity O(n) average \
    --style quickselect \
    --prove \
    --visualize \
    --lang python

Generated files:
  kth_largest_solution.py:
    import random
    
    def quickselect(arr, k):
        """Returns kth largest element (1-indexed).
        Average: O(n), Worst: O(n²)
        Space: O(1) in-place"""
        def select(left, right, k_smallest):
            if left == right:
                return arr[left]
            pivot_idx = random.randint(left, right)
            pivot_idx = partition(left, right, pivot_idx)
            if k_smallest == pivot_idx:
                return arr[k_smallest]
            elif k_smallest < pivot_idx:
                return select(left, pivot_idx - 1, k_smallest)
            else:
                return select(pivot_idx + 1, right, k_smallest)
        
        return select(0, len(arr)-1, len(arr)-k)
    
    def partition(left, right, pivot_idx):
        pivot = arr[pivot_idx]
        arr[pivot_idx], arr[right] = arr[right], arr[pivot_idx]
        store = left
        for i in range(left, right):
            if arr[i] < pivot:
                arr[store], arr[i] = arr[i], arr[store]
                store += 1
        arr[right], arr[store] = arr[store], arr[right]
        return store

  kth_largest_analysis.md:
    ## Correctness Sketch
    
    **Precondition**: 1 ≤ k ≤ len(arr)
    **Postcondition**: returned element is kth largest in original array (modulo permutation)
    
    Loop invariant for partition (Lomuto scheme):
      - All elements arr[left:store] < pivot
      - All elements arr[store:i] ≥ pivot
      - All elements arr[i:right] unexamined
      - Pivot at arr[right]
    
    Quickselect recurrence:
      - T(n) = T(n/2) + O(n) average (good pivot)
      - T(n) = T(n-1) + O(n) worst (bad pivot)
      - Expected pivot rank uniformly distributed → average T(n) = O(n)
    
    **Proof of termination**: Each recursive call reduces array size by at least 1 (partition moves pivot to final position)

  kth_largest_flow.dot:
    digraph quickselect {
        node [shape=box];
        Start -> Partition;
        Partition -> "k == pivot_idx" [label="true"];
        Partition -> "k < pivot_idx" [label="false"];
        "k == pivot_idx" -> Return;
        "k < pivot_idx" -> "Recurse left";
        "k > pivot_idx" -> "Recurse right";
        "Recurse left" -> Partition;
        "Recurse right" -> Partition;
    }
```

### Example 2: Optimization with Rationale
```
User input:
  logic-sculptor optimize ./algorithms/fibonacci_recursive.py \
    --target time \
    --iterations 2 \
    --explain

Input (fibonacci_recursive.py):
  def fib(n):
      if n <= 1: return n
      return fib(n-1) + fib(n-2)

Iteration 1:
  Applied: Memoization
  Output: fib_memo.py
  Changes:
    - Added @lru_cache(maxsize=None)
    - Complexity: O(n) time, O(n) space
  
Iteration 2:
  Applied: Iterative DP (tabulation) with space optimization
  Output: fib_optimized.py
  Changes:
    - Eliminated recursion stack (prevents RecursionError)
    - Space: O(1) by tracking only two previous values
    - Time: O(n), Space: O(1)
  
optimization_log.md:
  ## Transformation Log
  
  Pass 1 (Memoization):
    - Benefit: Exponential→linear time
    - Cost: O(n) memory for cache
    - Tradeoff: Acceptable for n ≤ 10^6
  
  Pass 2 (Iterative DP):
    - Benefit: O(1) space, no recursion limits
    - Cost: Slightly less declarative
    - Rationale: Fibonacci naturally iterative
  
  Final verdict: fib_optimized.py achieves optimal O(n,1) time-space.
```

### Example 3: Verification with Counterexample
```
User input:
  logic-sculptor verify ./binary_search.py tests_bounds.json \
    --property total-correctness \
    --mode symbolic

tests_bounds.json:
  {"inputs": [[1,2,3,4,5], [1]], "targets": [4, 1]}

binary_search.py:
  def binary_search(arr, target):
      lo, hi = 0, len(arr)
      while lo < hi:
          mid = (lo + hi) // 2
          if arr[mid] < target: lo = mid + 1
          elif arr[mid] > target: hi = mid
          else: return mid
      return -1

Verification result:
  verification_result.yaml:
    status: FAILED
    property: total-correctness
    counterexample:
      input: [1,3,5,7], target: 2
      expected: -1 (not found)
      actual: IndexError (mid out of bounds)
    issue: "hi = len(arr)" causes mid to equal len(arr) when lo=len(arr)-1, hi=len(arr)
    fix: "hi = len(arr) - 1" or guard mid access

Generated patch suggestion:
  def binary_search(arr, target):
      lo, hi = 0, len(arr) - 1  # ← fixed boundary
      while lo <= hi:           # ← changed condition
          mid = (lo + hi) // 2
          ...
```

### Example 4: Benchmark with Complexity Detection
```
User input:
  logic-sculptor benchmark quicksort_v1.py \
    --samples 50 \
    --memory \
    --profile cprofile \
    --reference quicksort_optimized.py

Generated input sizes: [100, 500, 1000, 5000, 10000, 50000]
Benchmark results:
  quicksort_v1.py:
    Time scaling: T(n) ≈ 0.0000012 × n^1.95  → Empirical O(n²) on already-sorted data (bad pivot)
    Memory: O(log n) stack in average, O(n) worst
    
  quicksort_optimized.py (median-of-three pivot):
    Time scaling: T(n) ≈ 0.0000008 × n^1.01 → Empirical O(n log n)
    Memory: O(log n) stack guaranteed
  
  Speedup at n=50000: 3.2× faster, 1.5× less memory
  
benchmark_plots/time_scaling.png:
  [Scatter plot with fitted curves showing quadratic vs n log n slope]
```

### Example 5: Pattern Library Exploration
```
User input:
  logic-sculptor patterns show "sliding-window"

Output:
  ## Pattern: Sliding Window
  
  **Use when**: Finding contiguous subarray satisfying constraint (sum, product, uniqueness, max/min length)
  
  **Core structure**:
    left = 0
    for right in range(len(arr)):
        update window state with arr[right]
        while window violates condition:
            remove arr[left] from state
            left += 1
        if window satisfies goal:
            record solution [left:right+1]
  
  **Complexity guarantees**: O(n) time (each element enters window once, exits once)
  
  **Canonical problems**:
    - Longest substring without repeating characters
    - Minimum size subarray sum ≥ target
    - Maximum sum of size k subarray
  
  **Template code (Python)**:
    def sliding_window(arr, **state_updater):
        left = 0
        best = None
        for right, val in enumerate(arr):
            state_updater.add(val)
            while state_updater.violates():
                state_updater.remove(arr[left])
                left += 1
            if state_updater.goal_met():
                best = max(best, right-left+1, key=len) ...
        return best
  
  **Pitfalls**: Forgetting to shrink window after expanding, incorrect state updates at boundaries.
```

## Rollback Commands

### Revert Design to Previous Iteration
```
# If working in interactive scaffold mode
logic-sculptor scaffold cancel

# If files already generated, restore from git
git checkout HEAD -- kth_largest_solution.py

# Or use built-in backup (if --backup flag was used)
logic-sculptor restore kth_largest --from-backup 2024-03-15T10:30:00
```

### Undo Optimization Passes
```
# De-optimize to original (requires keeping originals)
logic-sculptor optimize kth_largest.py --reverse --to-iteration 0

# Compare versions side-by-side
logic-sculptor diff kth_largest_original.py kth_largest_optimized.py

# Keep both and branch in git
git branch kth_largest_original
```

### Revert Verification Changes (if any)
```
# Some verifications may add assertions/invariants to code
logic-sculptor verify fib.py tests.json --apply-fixes --dry-run  # preview
logic-sculptor verify fib.py tests.json --apply-fixes           # apply
logic-sculptor verify fib.py tests.json --revert-fixes         # undo

# Manual restoration
cp ./backups/fib.py.before_verification fib.py
```

### Cleanup Temporary Files
```
# Remove all generated artifacts for a project
logic-sculptor cleanup kth_largest --keep-solution --remove-analysis
logic-sculptor cleanup all --dry-run
logic-sculptor cleanup all --expire 7d  # remove files older than 7 days

# Standard cleanup
rm -f *_analysis.md *.dot benchmark_* verification_*.yaml optimization_log.md
```

### Reset Configuration
```
# If environment variables caused issues
unset LOGIC_SCULPTOR_MODE LOGIC_SCULPTOR_COMPLEXITY
logic-sculptor config reset --to-defaults
```