
## StackfullObjectPool
This repository contains a thread-safe header-only stackfull object pool under 'StackfullObjectPool/StackfullObjectPool.hpp'.<br>For some toy examples look at 'StackfullObjectPool/StackfullObjectPoolTests.cpp'.<br>NOTE #1: The pool is meant to store only [Trivially Copyable types](https://en.cppreference.com/w/cpp/named_req/TriviallyCopyable), and it is enforced by a concept. Hence it's appropriate to use it to store Plain Old Data types ([PODs](https://en.wikipedia.org/wiki/Passive_data_structure)) and the likes.<br>NOTE #2: A trivially copyable type must have a [Trivial Destructor](https://en.cppreference.com/w/cpp/language/destructor#Trivial_destructor), hence the destructor of the pool's objects is never called upon releasing them. Rather the bytes used to store the object are overwritten and reused.<br>NOTE #3: The pool-objects type need not define a default constructor.<br>NOTE #4: The pool's lifetime must exceed that of its objects, otherwise it'll lead to undefined behavior.
#### Some implementation details
The pool items' allocation and deallocation is managed using std::unique_ptr.<br>Under the hood, the pool is implemented using std::array of std::byte.<br>The next open slot in the pool is managed using a stack.