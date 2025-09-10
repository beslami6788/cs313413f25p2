README – Lab on Lists and Iterators
===================================

This document answers the TODO questions embedded in the source code files
TestList.java, TestIterator.java, and TestPerformance.java.

--------------------------------------------------
Questions from TestIterator.java
--------------------------------------------------

Q: Also try with a LinkedList – does it make any difference?
A: For small test cases, there is no difference in functionality between
ArrayList and LinkedList when using iterators. Both return elements in the
same order. However, LinkedList has slower random access (get by index),
while iteration performance is roughly comparable. For the unit tests,
both implementations work correctly.

Q: What happens if you use list.remove(Integer.valueOf(77)) instead of
i.remove() while iterating?
A: Calling list.remove(Integer.valueOf(77)) directly while iterating
modifies the underlying list without informing the iterator. This causes
a ConcurrentModificationException. In contrast, i.remove() is the correct
way to remove elements safely during iteration.

--------------------------------------------------
Questions from TestList.java
--------------------------------------------------

Q: Also try with a LinkedList – does it make any difference?
A: No difference in correctness; all list operations behave according to
the List interface. However, performance characteristics differ:
  - ArrayList is faster for indexed access (get/set).
  - LinkedList is faster for insertions/removals at the beginning.

Q: In testRemoveObject – what does list.remove(5) do?
A: list.remove(5) removes the element at index 5 (zero-based). In the test
case, that means removing the 6th element of the list.

Q: In testRemoveObject – what does list.remove(Integer.valueOf(5)) do?
A: list.remove(Integer.valueOf(5)) removes the first occurrence of the
object "5" from the list, regardless of index. This is the object-removal
overload, not the index-removal version.

--------------------------------------------------
Questions from TestPerformance.java
--------------------------------------------------

Q: What conclusions can you draw about the performance of LinkedList vs.
ArrayList when comparing their running times for AddRemove vs. Access?
A:
- AddRemove at the beginning:
  LinkedList performs significantly better because insertion/removal at the
  head is O(1), while ArrayList shifts all elements (O(n)).
- Access by index:
  ArrayList is much faster because it supports O(1) random access, while
  LinkedList requires O(n) traversal to reach an index.

Q: Which of the two lists performs better as the size increases?
A:
- For random access (get), ArrayList scales much better.
- For repeated add/remove operations at the front, LinkedList scales better.
- For general-purpose use where random access dominates, ArrayList is usually
the preferred choice.
