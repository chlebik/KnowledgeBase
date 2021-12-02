# xUnit Design Patterns by Gerard Meszaros

## Part 1 - The narratives

### Chapter 1 - A brief tour
### Chapter 2 - Test smells

### Chapter 3 - Goals of test automation

Goals of test automation (tests should...):

* **improve quality** 
  * tests as specification
  * bug repellent
  * bug localization
* **help understand the SUT**
  * tests as documentation
* **reduce the risk (not introduce it)**
  * tests as safety net
  * do no harm
* **easy to run**
  * fully automated tests
  * self-checking tests
  * repeatable tests
* **easy to write and maintain**
  * simple tests
  * expressive tests
  * separation of concerns
* **require minimal maintenance as system grows**
  * robust tests   
 

### Chapter 4 - Philosophy of test automation

* tests after or test first
* test-by-test or test all-at-once
* outside-in or inside-out
* behaviour verification or state verification
* fixture design by test or big fixture upfront


### Chapter 5 - Principles of test automation

* Test-driven design
* design for testability
* use the front door first
* communicate intent
* don't modify the SUT
* keep tests independent
* isolate the SUT
* minimize test overlap
* minimize untestable code
* keep test logic out of production code
* verify one condition per test (hint: whole object/process state, not just pieces)
* test concerns separately
* ensure commensurate effort and responsibility (effort to write test <= effort to write production code)


### Chapter 6 - Test automation strategy
Basics - know them already

### Chapter 7 - xUnit Basis
Basics - know them already


### Chapter 8 - Transient Fixtures

**Fresh fixture** - every SUT test sets up the state (fixtures) from scratch, however based on the strategy what 
 to do with them AFTER the test, we can separate **transient fresh fixture** and **persistent fresh fixtures**. 
This chapter concentrates on the former.

How fixtures can be setup:
* **inline setup** - everything is put inside the test method (possibly a lot of bloatware/repeated code is created)
* **delegated setup** - we extract repeatable logic to separate utility methods with descriptive names.
> When it is not important for something to be seen in the test method, it is important that it not be seen in the test method!
* **implicit setup** - is a hook provided by the framework - eg. ```setUp()``` or methods in general annotated with 
```@BeforeTest``` or such.


### Chapter 9 - Persistent Fixtures



## Part 2 - The test smells
## Part 3 - The patterns
## Part 4 - The narratives
