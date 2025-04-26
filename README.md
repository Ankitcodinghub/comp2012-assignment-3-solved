# comp2012-assignment-3-solved
**TO GET THIS SOLUTION VISIT:** [COMP2012 Assignment 3 Solved](https://www.ankitcodinghub.com/product/comp2012-solved-4/)


---

📩 **If you need this solution or have special requests:** **Email:** ankitcoding@gmail.com  
📱 **WhatsApp:** +1 419 877 7882  
📄 **Get a quote instantly using this form:** [Ask Homework Questions](https://www.ankitcodinghub.com/services/ask-homework-questions/)

*We deliver fast, professional, and affordable academic help.*

---

<h2>Description</h2>



<div class="kk-star-ratings kksr-auto kksr-align-center kksr-valign-top" data-payload="{&quot;align&quot;:&quot;center&quot;,&quot;id&quot;:&quot;124250&quot;,&quot;slug&quot;:&quot;default&quot;,&quot;valign&quot;:&quot;top&quot;,&quot;ignore&quot;:&quot;&quot;,&quot;reference&quot;:&quot;auto&quot;,&quot;class&quot;:&quot;&quot;,&quot;count&quot;:&quot;3&quot;,&quot;legendonly&quot;:&quot;&quot;,&quot;readonly&quot;:&quot;&quot;,&quot;score&quot;:&quot;5&quot;,&quot;starsonly&quot;:&quot;&quot;,&quot;best&quot;:&quot;5&quot;,&quot;gap&quot;:&quot;4&quot;,&quot;greet&quot;:&quot;Rate this product&quot;,&quot;legend&quot;:&quot;5\/5 - (3 votes)&quot;,&quot;size&quot;:&quot;24&quot;,&quot;title&quot;:&quot;COMP2012 Assignment 3 Solved&quot;,&quot;width&quot;:&quot;138&quot;,&quot;_legend&quot;:&quot;{score}\/{best} - ({count} {votes})&quot;,&quot;font_factor&quot;:&quot;1.25&quot;}">

<div class="kksr-stars">

<div class="kksr-stars-inactive">
            <div class="kksr-star" data-star="1" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="2" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="3" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="4" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="5" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>

<div class="kksr-stars-active" style="width: 138px;">
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>
</div>


<div class="kksr-legend" style="font-size: 19.2px;">
            5/5 - (3 votes)    </div>
    </div>
As an example to demonstrate the ownership problem and the application of the smart pointers we just implemented, the second half of this assignment will be an implementation of a simple representation of graphs and operations on them. Since a node can be the neighbor of, and hence have its reference held by multiple other nodes, smart pointers can be used to keep track of the number of held references of a node, and deallocate a node when no other nodes hold a reference to it.

Download

Skeleton code: pa3-skeleton.zip

End of Download

Review

We first review graphs, which is used as an example to demonstrate the ownership problem in this assignment.

A graph is a structure consisting of a set of nodes and a set of edges, which are pairs of nodes. In this assignment, we consider undirected graphs only, where an edge from a node n1 to another node n2 is also an edge from n2 to n1. Additionally, self-edges (an edge from a node to itself) and duplicate edges are forbidden.

If an edge from n1 to n2 exists, we say that n2 is a neighbor of n1. To represent a graph, we store the adjacency list of each node, which is simply a list of its neighbors. The degree of a node is the number of its neighbors.

A node nk is said to be reachable from a node n0 if a sequence of edges (n0, n1), (n1, n2), …, (nk-1, nk) exists. A connected subgraph of a node n is the set of reachable nodes from n.

As an example of graphs, think of the flights of an airline. The airports served by the airline are represented as nodes, and flights between two airports are represented as edges. The degree of a node (an airport) would then be the number of other airports connected by a direct flight. An airport is reachable from another airport if a sequence of flights connects them. And the connected subgraph of an airport is the set of airport reachable by an arbitrary number of flights. Natually, the airline would prefer not to waste storage space for airports they no longer serve, so this is a perfect application of our smart pointers, which would deallocate the data of an airport when all flights to it have been discontinued (i.e. all edges of the node have been removed).

End of Review

Description

This assignment can be divided into three parts, with each depending on the previous one. The first two parts each consists of a class template, and the last part consists of some function templates that operate on the class templates. You should ensure that memory leak does not occur in all of the functions you implement.

Part (A) SmartPtr&lt;T&gt;

The class template SmartPtr&lt;T&gt; declared in smartptr.h provides an abstraction for handling memory allocation and deallocation using reference counting. It contains the following data members:

T* ptr; unsigned int* count;

ptr is a pointer to type T. If the address stored in ptr is nullptr, we say that this SmartPtr is null. If ptr is not nullptr, it should point to a valid, allocated address. Note that a null SmartPtr only conceptually represents a null pointer, and the SmartPtr object itself is still defined. All member functions beside operator* can still be safely called on a null SmartPtr.

count is a pointer to type unsigned int, which is used to store the number of SmartPtr instances containing the address ptr. count should be nullptr if and only if ptr is nullptr.

Memory management of the object referred to by SmartPtrs are managed by the constructor, destructor, set and unset member functions. The only ways to initialize and assign ptr is by setting it to nullptr, an address allocated by copy-constructing an instance of type T, or the address contained in another instance of SmartPtr.

When a SmartPtr is created for or set to a new T object, count should be allocated to store the number 1, meaning, the address of the new T object is stored in only 1 SmarPtr. For example:

SmartPtr sp {42};

The number pointed to by count of sp is now 1 and ptr is allocated to store 42.

sp.set(0);

Again, the number pointed to by count of sp is set to 1 and ptr is allocated to store 0.

When a SmartPtr is copied by the copy constructor or assignment operator, the address stored in ptr is being copied, the number pointed to by count has to be incremented by 1. It means that the T object pointed by to ptr is being pointed to by one more SmartPtr instance.

Similarly, when a SmartPtr is destructed or set to refer to another object, the number pointed to by count has to be decremented. When the number becomes zero, it means that this instance of SmartPtr is the last to hold a reference to the object pointed to by ptr. Both ptr and count should be deallocated properly.

Member functions

SmartPtr&lt;T&gt;::SmartPtr

Compares the pointer member ptr of two instances of SmartPtr using the corresponding operators.

SmartPtr&lt;T&gt;::operator*

T&amp; operator*() const;

Returns by reference the object pointed to by ptr. Whether ptr points to nullptr is not checked.

SmartPtr&lt;T&gt;::operator-&gt;

T* operator-&gt;() const;

Returns the address stored in ptr.

Non-member functions operator&lt;&lt;

template &lt;typename T&gt; std::ostream&amp; operator&lt;&lt;(std::ostream&amp; os, const SmartPtr&lt;T&gt;&amp; sp);

If sp is not null, outputs to os the string “SmartPtr(“, followed by the object pointed to by sp.ptr, then by a “,”, then by the number of SmartPtr instances containing the address sp.ptr, finally by “)”. The object pointed to by sp.ptr should be output by invoking operator&lt;&lt;. Otherwise, outputs to os the string “SmartPtr()”.

For example, if sp.ptr points to a string “Hello World”, with two instances of SmartPtr holding the same address, os &lt;&lt; sp should output “SmartPtr(Hello World,2)” to os.

The return value should follow the convention as the standard library, where chaining multiple invocations of operator&lt;&lt; outputs to the same stream. For example, os &lt;&lt; sp &lt;&lt; ” ” would output a newline character following “SmartPtr(Hello World,2)” to os.

Implement this function template in smartptr-output.tpp. No other required implementations should be present in smartptr-output.tpp. For grading, besides the cases explicitly testing operator&lt;&lt;, your implementation in smartptr-output.tpp will be swapped for a standard implementation.

Part (B) Node&lt;T&gt;

The class template Node&lt;T&gt; represents a node or vertex in a graph. It contains the following data members:

T val;

SmartPtr&lt;Node&lt;T&gt;&gt;* out; unsigned int capacity; unsigned int size_p;

Member functions

Node&lt;T&gt;::Node

Node(const T&amp; val);

template &lt;typename T&gt; void remove_graph(SmartPtr&lt;Node&lt;T&gt;&gt; root);

Removes every node from the connected subgraph of root by removing all edges between each pair of nodes, which would deallocate their memory if no other SmartPtrs hold a reference to them. Does nothing if root is null.

find

template &lt;typename T&gt;

SmartPtr&lt;Node&lt;T&gt;&gt; find(SmartPtr&lt;Node&lt;T&gt;&gt; root, T val);

Finds a node whose val field is equal to val. Returns a null SmartPtr if none of the nodes have a val field is equal to val, or if root is null.

reachable

template &lt;typename T&gt; bool reachable(SmartPtr&lt;Node&lt;T&gt;&gt; root, SmartPtr&lt;Node&lt;T&gt;&gt; dest);

Returns true if dest is reachable from root, i.e. dest is in the connected subgraph of root, and false otherwise. Returns false if either root or dest is null.

End of Description

Tasks

Your task is to implement the missing member functions of the two classes and function templates in smartptr.tpp, smartptr-output.tpp, graph.tpp and graph-output.tpp.

End of Tasks

Sample Output and Grading

There are 27 given test cases of which the code can be found in the given main function.

These 27 test cases are first run without any memory leak checking (they are numbered #1 #27 on ZINC). Then, the same 27 test cases will be run again, in the same order, with memory leak checking (those will be numbered #101 – #127 on ZINC). For example, test case #108 on ZINC is actually the given test case #8 (in the given main function) run with memory leak checking.

About memory leak and other potential errors

End of Sample Output and Grading

Submit a single zip file pa3.zip containing the following files only: smartptr.tpp, smartptroutput.tpp, graph.tpp and graph-output.tpp. Submit the file to ZINC. ZINC usage instructions can be found here.

Notes:

In the grading report, pay attention to various errors reported. For example, under the “make” section, if you see a red cross, click on the STDERR tab to see the compilation errors. You must fix those before you can see any program output for the test cases below.

Make sure you submit the correct file yourself. You can download your own file back from ZINC to verify. Again, we only grade what you uploaded last to ZINC.

Compilation Requirement

It is required that your submissions can be compiled and run successfully in our online autograder ZINC. If we cannot even compile your work, it won’t be graded. Therefore, for parts that you cannot finish, just put in dummy implementation so that your whole program can be compiled for ZINC to grade the other parts that you have done. Empty implementations can be like:

In this particular PA, it is probably related to misuse of dynamic memory. Good luck with bug hunting!

Specification clarification

Q: Should I increment the count when I copy construct or copy assign a SmartPtr?

End of Frequently Asked Questions
