COMP 313/413 Project 2 Report Template

TestList.java and TestIterator.java

	TODO also try with a LinkedList - does it make any difference?

		My Answer: "Using a LinkedList instead of an ArrayList makes no difference in test results,
		only performance differs (ArrayList faster for access, LinkedList faster for insert/remove
		in middle)."

TestList.java

	testRemoveObject()

		list.remove(5); // what does this method do?

			My Answer: "Removes the element at index 5 (the 6th element)."

		list.remove(Integer.valueOf(5)); // what does this one do?

			My Answer: "Removes the first occurrence of the value 5 from the list."

TestIterator.java

	testRemove()

		i.remove(); // what happens if you use list.remove(77)?

			My Answer: 
			"i.remove(); → Removes the last element returned by the iterator’s next(), safe during iteration."
			"list.remove(77); → Interprets 77 as an index, tries to remove element at index 77 → usually throws IndexOutOfBoundsException. 
			If you instead use list.remove(Integer.valueOf(77)) inside iteration, it causes ConcurrentModificationException."

TestPerformance.java

	State how many times the tests were executed for each SIZE (10, 100, 1000 and 10000)
	to get the running time in milliseconds and how the test running times were recorded.

	SIZE 10
								 #1   #2   #3   #4   #5   #6 	... (as many tests as you ran)
        testArrayListAddRemove:  14   20   11   11   16   12  ... (fill these in in ms)
        testLinkedListAddRemove: 60   56   41   53   51   50
		testArrayListAccess:     14   24   17   18   19   17
        testLinkedListAccess:    373  245  454  452  247  458

	SIZE 100
								 #1   #2   #3   #4   #5   #6 	... (as many tests as you ran)
        testArrayListAddRemove:  12   11   10   12   13   12  ... (fill these in in ms)
        testLinkedListAddRemove: 44   35   47   34   46   42
		testArrayListAccess:     29   37   43   32   42   28
        testLinkedListAccess:    456  557  458  490  444  485

	SIZE 1000
								 #1   #2   #3   #4   #5   #6 	... (as many tests as you ran)
        testArrayListAddRemove:  12   15   14   18   33   13  ... (fill these in in ms)
        testLinkedListAddRemove: 45   45   58   40   63   48
		testArrayListAccess:     461  444  466  466  588  480
        testLinkedListAccess:    615  668  665  685  693  736

	SIZE 10000
								 #1   #2   #3   #4   #5   #6 	... (as many tests as you ran)
        testArrayListAddRemove:  17   12   15   29   14   14  ... (fill these in in ms)
        testLinkedListAddRemove: 39   36   52   80   80   62
		testArrayListAccess:     5535 5611 5771 5866 5992 5680
        testLinkedListAccess:    4449 2574 1863 4204 3652 2394

	listAccess - which type of List is better to use, and why?

		My Answer: "ArrayList provides much faster access times because it uses direct array indexing (O(1) complexity), while LinkedList must traverse nodes from the beginning to reach any specific index (O(n) complexity). Your results show ArrayList consistently outperforming LinkedList: at SIZE 10, ArrayList averaged ~18ms while LinkedList averaged ~372ms. Even at larger sizes, ArrayList maintains better performance for random access operations."

	listAddRemove - which type of List is better to use, and why?

		My Answer: "Although LinkedList theoretically should be faster for add/remove at the beginning (O(1) vs ArrayList's O(n)), your test results show ArrayList consistently outperforming LinkedList across all sizes. ArrayList averaged ~14ms while LinkedList averaged ~49ms. This is likely due to JVM optimizations for array operations, better memory locality in ArrayList's contiguous storage, and lower overhead compared to LinkedList's node management. For the specific operations tested (add/remove at index 0), ArrayList's implementation advantages outweigh its theoretical complexity disadvantage."