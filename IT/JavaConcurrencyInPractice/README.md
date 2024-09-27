Below you will find quotes taken from *"Java concurrency in practice"*, a classic book about Java's multithreading and concurrency. Writing notes from this book would be like rewriting it - therefore, I am just putting here the specific remind-me-of quotes from the book.


------------------------------------------------------------------------------------------

## Chapter 2 - Thread safety

Stateless objects are always thread-safe.

A race condition occurs when the correctness of a computation depends on the relative timing or interleaving of multiple threads by the runtime;
in other words, when getting the right answer relies on lucky timing. The most common type of race condition is check-then-act, where a potentially stale observation is used to make a decision on what to do next.

Where practical, use existing thread-safe objects, like AtomicLong, to manage your class's state. It is simpler to reason about the possible states and state transitions for existing thread-safe objects than it is for arbitrary state variables, and this makes it easier to maintain and verify thread safety.

To preserve state consistency, update related state variables in a single atomic operation.

## Chapter 3 - Sharing objects

For each mutable state variable that may be accessed by more than one thread, all accesses to that variable must be performed with the same lock held. In this case, we say that the variable is guarded by that lock.

Every shared, mutable variable should be guarded by exactly one lock. Make it clear to maintainers which lock that is.

Avoid holding locks during lengthy computations or operations at risk of not completing quickly such as network or console I/O.

In the absence of synchronization, the compiler, processor, and runtime can do some downright weird things to the order in which operations appear to execute. Attempts to reason about the order in which memory actions “must” happen in insufflciently synchronized multithreaded programs will almost certainly be incorrect.

Locking is not just about mutual exclusion; it is also about memory visibility. To ensure that all threads see the most up-to-date values of shared mutable variables, the reading and writing threads must synchronize on a common lock.

Use volatile variables only when they simplify implementing and verifying your synchronization policy; avoid using volatile variables when veryfing correctness would require subtle reasoning about visibility. Good uses of volatile variables include ensuring the visibility of their own state, that of the object they refer to, or indicating that an important lifecycle event (such as initialization or shutdown) has occurred.

Locking can guarantee both visibility and atomicity; volatile variables can only guarantee visibility.

Immutable objects are always thread-safe.

Just as it is a good practice to make all fields private unless they need greater visibility, it is a good practice to make all fields final unless they need to be mutable.

## Chapter 4 - Composing objects

You cannot ensure thread safety without understanding an object's invariants and postconditions. Constraints on the valid values or state transitions for state variables can create atomicity and encapsulation requirements.

Encapsulating data within an object confines access to the data to the object's methods, making it easier to ensure that the data is always accessed with the appropriate lock held.

Confinement makes it easier to build thread-safe classes because a class that confines its state can be analyzed for thread safety without having to examine the whole program.

If a class is composed of multiple independent thread-safe state variables and has no operations that have any invalid state transitions, then it can delegate thread safety to the underlying state variables.

If a state variable is thread-safe, does not participate in any invariants that constrain its value, and has no prohibited state transitions for any of its operations, then it can safely be published.


## Chapter 5 - Building blocks

Where practical, delegation is one of the most effective strategies for creating thread-safe classes: just let existing thread-safe classes manage all the state.

Replacing synchronized collections with concurrent collections can offer dramatic scalability improvements with little risk.

## Chapter 6 - Task execution

Executor is based on the producer-consumer pattern, where activities that submit tasks are the producers (producing units of work to be done) and the threads that execute tasks are the consumers (consuming those units of work). Using an Executor is usually the easiest path to implementing a producer-consumer design in your application.

The real performance payoff of dividing a program's workload into tasks comes when there are a large number of independent, homogeneous tasks that can be processed concurrently.

## Chapter 7 - Cancellation and shutdown

There is nothing in the API or language specification that ties interruption to any specific cancellation semantics, but in practice, using interruption for anything but cancellation is fragile and difficult to sustain in larger applications.

Calling interrupt does not necessarily stop the target thread from doing what it is doing; it merely delivers the message that interruption has been requested.

Interruption is usually the most sensible way to implement cancellation.

Only code that implements a thread's interruption policy may swallow an interruption request. General-purpose task and library code should never swallow interruption requests.

When **Future.get** throws **InterruptedException** or **TimeoutException** and you know that the result is no longer needed by the program, cancel the task with **Future.cancel**.

Daemon threads are not a good substitute for properly managing the lifecycle of services within an application.

## Chapter 8 - Applying thread pools

Whenever you submit to an Executor tasks that are not independent, be aware of the possibility of thread starvation deadlock, and document any pool sizing or configuration constraints in the code or configuration file where the Executor is configured.

Sequential loop iterations are suitable for parallelization when each iteration is independent of the others and the work done in each iteration of the loop body is significant enough to offset the cost of managing a new task.

## Chapter 9 - GUI applications

**I have read the chapter out of curiosity but as I have never worked with AWT/Swing, and the current desktop work for Java is based on JavaFX - I am not putting any quotes here**

## Chapter 10 - Avoiding liveness hazards

A program will be free of lock-ordering deadlocks if all threads acquire the locks they need in a fixed global order.

Invoking an alien method with a lock held is asking for liveness trouble. The alien method might acquire other locks (risking deadlock) or block for an unexpectedly long time, stalling other threads that need the lock you hold.

Strive to use open calls throughout your program. Programs that rely on open calls are far easier to analyze for deadlock-freedom than those that allow calls to alien methods with locks held.

Avoid the temptation to use thread priorities, since they increase platform dependence and can cause liveness problems. Most concurrent applications can use the default priority for all threads.

## Chapter 11 - Performance and scalability

Scalability describes the ability to improve throughput or capacity when additional computing resources (such as additional CPUs, memory, storage, or I/O bandwidth) are added.

Avoid premature optimization. First make it right, then make it fast—if it is not already fast enough.

Measure, don't guess.

All concurrent applications have some sources of serialization; if you think yours does not, look again.

Don't worry excessively about the cost of uncontended synchronization. The basic mechanism is already quite fast, and JVMs can perform additional optimizations that further reduce or eliminate the cost. Instead, focus optimization efforts on areas where lock contention actually occurs.

The principal threat to scalability in concurrent applications is the exclusive resource lock.

Allocating objects is usually cheaper than synchronizing.

## Chapter 12 - Testing concurrent programs

The challenge to constructing effective safety tests for concurrent classes is identifying easily checked properties that will, with high probability, fail if something goes wrong, while at the same time not letting the failure-auditing code limit concurrency artificially. It is best if checking the test property does not require any synchronization.

Tests should be run on multiprocessor systems to increase the diversity of potential interleavings. However, having more than a few CPUs does not necessarily make tests more effective. To maximize the chance of detecting timing-sensitive data races, there should be more active threads than CPUs, so that at any given time some threads are running and some are switched out, thus reducing the predicatability of interactions between threads.

Writing effective performance tests requires tricking the optimizer into not optimizing away your benchmark as dead code. This requires every computed result to be used somehow by your program—in a way that does not require synchronization or substantial computation.

## Chapter 13 - Explicit locks

## Chapter 14 - Building Custom Synhronizers

Document the condition predicate(s) associated with a condition queue and the operations that wait on them.

Every call to wait is implicitly associated with a specific condition predicate. When calling wait regarding a particular condition predicate, the caller must already hold the lock associated with the condition queue, and that lock must also guard the state variables from which the condition predicate is composed.

Whenever you wait on a condition, make sure that someone will perform a notification whenever the condition predicate becomes true.

**Hazard warning:** The equivalents of wait, notify, and notifyAll for Condition objects are await, signal, and signalAll. However, Condition extends Object, which means that it also has wait and notify methods. Be sure to use the proper versions—await and signal—instead!

## Chapter 15 - Atomic variables and nonblocking synchronization

## Chapter 16 - The Java memory model

With the exception of immutable objects, it is not safe to use an object that has been initialized by another thread unless the publication happens-before the consuming thread uses it.

Initialization safety guarantees that for properly constructed objects, all threads will see the correct values of final fields that were set by the constructor, regardless of how the object is published. Further, any variables that can be reached through a final field of a properly constructed object (such as the elements of a final array or the contents of a HashMap referenced by a final field) are also guaranteed to be visible to other threads.
