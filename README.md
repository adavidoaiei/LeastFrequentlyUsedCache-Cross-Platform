# LFU Cache Implementation

## Overview 

A cross platform (Windows/Linux/etc) Least Frequently Used (LFU) Cache implementation in .NET that evicts items based on their usage frequency. Each cached item maintains a usage counter that increments upon access. When the cache reaches its capacity limit, it removes the item with the lowest usage count to free up space.

**Note:** This project has been updated to run on Linux using NUnit for testing and Visual Studio Code as the development environment.

## Installation 

Install via NuGet Package Manager:

```
Install-Package LFUCache -Version 1.0.2
```

## Usage Example

```csharp
ICache<string, string> cache = new LfuCache<string, string>(1000);
cache.Add("name", "Helene");
cache.Add("surname", "Stuart");
var name = cache.Get("name");
```

## Technical Implementation

The `LfuCache` class implements the `ICache` interface:

![Class Diagram](https://raw.githubusercontent.com/adavidoaiei/LeastFrequentlyUsedCache-Build-Linux/master/images/diagram_xkbden.png)

### Data Structure

The implementation uses a hybrid data structure combining:
- A `SortedList` where the key is the usage count
- A `LinkedList` as the value, containing all elements with the same usage count

This structure is organized as a binary tree of linked lists, enabling O(log n) time complexity for both Add and Get operations.

![Binary Tree and Linked List Structure](https://raw.githubusercontent.com/adavidoaiei/LeastFrequentlyUsedCache-Build-Linux/master/images/binary_tree_linked_list_r9zgzj.jpg)

## Performance

### Benchmark Results

The cache demonstrates impressive performance:
- 1,000,000 add/get operations
- Cache size: 90,000 items
- Dataset size: 100,000 elements
- Execution time: 466ms

![LFU Cache Performance](https://raw.githubusercontent.com/adavidoaiei/LeastFrequentlyUsedCache-Build-Linux/master/images/lfu_syqnac.png)

Compared to .NET Framework's MemoryCache, this implementation:
- Executes faster
- Uses less memory
- Maintains consistent performance

![Memory Cache Performance Comparison](https://raw.githubusercontent.com/adavidoaiei/LeastFrequentlyUsedCache-Build-Linux/master/images/mc_ikzrsm.png)

The benchmarks:
- Use randomly generated Add/Get operation sequences in `BitArray`
- Process elements from a fixed-size list
- Are conducted using [BenchmarkDotNet](https://benchmarkdotnet.org/)

![Benchmark Results](https://raw.githubusercontent.com/adavidoaiei/LeastFrequentlyUsedCache-Build-Linux/master/images/benchmarks_gqqzru.png)

## Testing

Unit tests are written using the NUnit framework with comprehensive code coverage tracked through Azure Pipeline.

![Code Coverage Report](https://raw.githubusercontent.com/adavidoaiei/LeastFrequentlyUsedCache-Build-Linux/master/images/code_coverage_lzv2si.png)




