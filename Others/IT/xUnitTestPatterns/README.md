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
* **implicit setup** - is a hook provided by the framework - e.g. ```setUp()``` or methods in general annotated with 
```@BeforeTest``` or such.


### Chapter 9 - Persistent Fixtures

**Persistent fresh fixtures** are the ones, that are passed along the test methods and at the same time 'remember' 
their state. Mostly this is about DB being used by specific classes, but simple stateful objects are enough to 
qualify for it. 

The usual problem is with teardown when something goes bad in test methods. As there are three setup types, the 
same applies to teardown methods. There's a table in the chapter showing a matrix of recommended approaches.

In general the whole chapter is saying explicitly - if possible, avoid having them ;)


### Chapter 10 - Result verification
Basics - know them already - discussing mostly **state verification** vs **behavior verification**.

### Chapter 11 - Using test doubles


Types of **indirect input/output**:
* input - collaborator in the SUT returns a specific value that is an INPUT for the SUT (e.g. predefined value or 
  exception)
* output - collaborator in the SUT **performs** some side effect, but not necessarily returns it (e.g. logging/email 
  send)

Two types of DOC behaviour verification:
* Procedural - <em>test spy</em> records all the interactions, and assertions are executed against in the verification 
  phase (e.g. <em>Capture</em> in the Mockito)
* Expected behaviour - we register <em>mock object</em> in the SUT. During test execution calls made to it, are 
  compared against predefined behaviours. When there's one that does not match with the existing ones test fails (e.g.
  <em>when…then</em> in Mockito)

Types of <em>test doubles</em>:
* **dummy object** - passed to the methods to meet the contract, but not actually used
* **test stub** - object that replaces component in order to control **indirect inputs**. A more specialised one is 
  **test spy** that records the interactions
* **mock object** - object used to control **indirect outputs** (lenient/strict)
* **fake object** - replaces functionality of the collaborator with an alternate implementation (e.g. in memory DB)

> Finally, we want to be careful that we don't fall into the "new hammer trap." Overuse of Test Doubles (and 
> especially Mock Objects or Test Stubs) can lead to Overspecified Software by encoding implementation-specific
information about the design in our tests. The design may be then much more difficult to change if many tests are
> affected by the change simply because they use a Test Double that has been affected by the design change.


### Chapter 12 - Organizing our tests

Types of tests organisation:
* testcase class per class
* testcase class per feature
* testcase class per fixture


### Chapter 13 - Testing with databases

> When there is any way to test without a database, test without the database!

Main issues with DB:
* persistent fixtures - data can stay in a DB long after the tests were run, resulting in problematic state and 
  tests interfering with each other on the data level
* shared fixtures - somehow related to the previous one, although not only. While sharing a common test fixture 
  between tests, we can create unintended coupling between tests that should not be there
* general fixtures - we end up with a big-ball-of-fixtures of all kinds, that a lot of different tests is using 
  while testing unrelated behaviours.

If it is possible to avoid DB directly, we can consider two options:
* use in-memory DB
* use *DB Fake* (e.g. code implementation of DB using maps). The biggest win here is that we can set up the state as a 
  fresh one with every test run.

Direct testing of **stored procedures** can be done in two ways (ok, I know that it's 2022 and basing any 
application logic on stored procedures is *passé*, but the book is quite old, so let's roll):
* we just call them directly using the framework/language that we write all other tests with
* we use dedicated xUnit solution for the DB (I didn't know that such possibility even exist!)


### Chapter 14 - Roadmap to effective test automation

This chapter describes a roadmap, of how to start with testing automation. To me, it's like 101 on testing in general,
but I won't go into details here. Instead, I'm just putting here a list of the recommended way of how to start:
* Exercise the happy path
* Verify direct outputs of the happy path
* Verify alternative paths
* Verify indirect output behaviour
* Optimize test execution and maintainability


## Part 2 - The test smells

### Chapter 15 - Code smells

* **Obscure test** - tests should serve as a documentation, and a separate execution logic. Any kind of problems 
  that prevent the test from meeting these two criteria are wrong. We should aim for the tests to be as clear and 
  readable as possible.
* **Conditional test logic** - test contains logic which does not need to be executed. It clutters the code, and 
  makes it harder to follow and maintain. Here a differentiation is needed - we are talking about execution logic 
  here, not the infrastructure code of the test itself (e.g. used for avoiding duplicates). 
* **Hard to test code** - it's simply the code, that suffers from bad architecture/design, and therefore testing it 
  is hard - usual culprits are **tight-coupling**, **asynchronous code** or **untestable test code** (meaning the 
  test code itself is hard to read and understand) 
* **Test code duplication** - mostly due to overuse of copy&paste or lack of time (or both). Simple refactorings 
  like *extract method/object* should help, the same as increasing awareness of the existence of helper code/classes.
* **Test logic in production** - code that is actually deployed to PRD, contains code that should be run only during 
  tests. In order to avoid that, it's best to extract that kind of hardcoded logic into a dependency 
  (strategy/collaborator), and use runtime config/polymorphism to execute proper piece of code. 


### Chapter 16 - Behavior smells

* **Assertion roulette** - occurs when test failure cannot be identified with a single assertion. Honestly I don't 
  know how it can happen with the current tooling, and provided examples of causes are not that convincing. 
* **Erratic tests** - the worst-case of chaos-driven testing. Sometimes the test works, and sometimes it does not. 
  The usual causes may be **interacting tests**, **interacting test suites**, **lonely test** (test run as a single 
  unit outside its suite fails, while working when run as a part of the suite), **resource leakage**, **resource 
  optimism** (code depending on external services, behaves in a nondeterministic way with different responses from 
  external source), **unrepeatable test** (green with the first run, red with all the subsequent ones), **test run 
  war** (more than one person executing tests concurrently) and **nondeterministic tests** 
* **Fragile tests** - tests are failing if the SUT that they test was changed, but it should not in any way 
  influence the test behavior. The other word used to describe it is **brittle tests**. 
* **Frequent debugging** - in order to locate the actual cause of test error we have to manually debug the code. The 
  usual problem is lack of proper localization (missing descriptive error messages for example) or overuse of mock 
  objects.  
* **Manual intervention** - every time a test is run it requires a person doing something (before running or during 
  the process). I expect that for unit tests it will be hard to find such thing, but for integration/component tests 
  I can imagine such scenarios without problems. In general the remedy here is to automate, automate, automate, or 
  mock/fake user-required behaviours.
* **Slow tests** - self-explanatory. 


### Chapter 17 - Project smells

* **Buggy tests** - unfortunately is found post-factum, where there's PRD problem, and it seems that our test code 
  was giving false positives, or vice versa - false negatives. Usually it's just a result of some other smells 
  (project/behavior alike).  
* **Developers not writing tests** - self-explanatory. If that's the situation, change the project or fire the 
  developers. 
* **High test maintenance cost** - as with the **buggy tests**, it's usually a combination of already mentioned 
  smells like **fragile/erratic tests**, **fragile fixtures** or **obscure/buggy tests** . The more changes to the 
  tests must be done with  every PRD code, the more this smell is felt. 
* **Production bugs** - despite having large amount of automated tests the number of bugs did not fall in comparison 
  to the time before writing tests. Usually that is a result of tests not being run as often as they should, or some 
  **lost tests** (disabled/not added to the suite). Although, in the current world of software development and CI/CD 
  I don't see if this should be that influential. More possible are just **missing tests** or lack of coverage for 
  the specific edge cases. 


## Part 3 - The patterns

### Chapter 18 - Test strategy patterns

#### Test automation strategy

* **recorded tests** - mostly used for *regression testing*. Unfortunately, they're tightly coupled with the UI 
  (which is usually used fo testing). Comparing to the times when the book was published, right now all these tools 
  are way more scriptable, and tests can be written also using code/text. Unfortunately there's still coupling part. 
* **scripted tests** - actually all the unit-tests we write are **scripted tests**, so no surprises there. What is 
  worth pointing out, is that these kinds of tests are also describing a situation, in which we create tests in some 
  higher level language or DSL, and then they're driving the development. An example would be *BDD* tests written by 
  business side before the development starts.
* **data-driven testing** - as simple as using *DataProviders* in *TestNG* or similar things in other 
  frameworks/libraries. The other term is *parameterized tests*. 
* **test-automation framework** - in general it mixes together tests runner, suites and tests, and names it as 
  *test-automation framework*. With the current state of tooling it's given OOB with every starter project/IDE so no 
  need to expand more on it here. Back then in 2007 when the book was published, it may be a thing to get everything 
  working. 



#### Test fixture strategy
* **minimal fixture** - exactly what it says. We should use as minimal fixture as possible when running tests.
* **standard fixture** - as the author says - it's more about the design than technology. We plan upfront for the 
  testing strategy and later, we reuse *standard fixture* among all the tests that can use it. *Standard fixture* is 
  always a *shared fixture* described below. What is more - there's a long section here asking - *who is actually 
  doing that?* - with an answer stating that when we're writing automated tests we should actually go rather towards 
  *minimal fixture*.
* **fresh fixture** - another no-brainer. We construct a *test fixture* for every test that is run. Creation is a 
  part of the setup phase (of the **test method**, not **class setup**). 
* **shared fixture** - using it is fine (especially for performance reasons), although it would be advisable to use 
  *immutable shared fixture*, to reduce the possibility of tests interfering with each other.


#### SUT interaction strategy
* **back door manipulation** - an example will be to verify the state of some 'under-the-hood' layer, instead the 
  SUT itself, e.g. DB. The problem here is that it's coupling low-level technical details to our tests, and what is 
  more - there must be an actual access using *back-door*. Although, it has its usages, when we want to confirm the 
  state of underlying layer, if there are other collaborators using it (e.g. besides our application operating 
  on the DB, we have some BI tooling that uses it). Also, it can speed up the tests, by testing the underlying state 
  directly, rather than generate some robust and heavy report using SUT. 
* **layer test** - name says all - we test only one layer to reach high coverage


### Chapter 19 - xUnit basic patterns

Actually I'm just listing here the contents, as there's nothing in this chapter that would require describing here.
I have the knowledge presented in the chapter already, so I'm just putting here the bullet points as a reminder.

#### Test definition

* **test method**
* **four-phase test** - setup/exercise/verify/teardown
* **assertion method**
* **assertion message**
* **testcase class**

#### Test execution
* **test runner**
* **testcase object**
* **test suite object**
* **test discovery**
* **test enumeration**
* **test selection**


### Chapter 20 - Fixture setup patterns

Actually I'm just listing here the contents, as there's nothing in this chapter that would require describing here.
I have the knowledge presented in the chapter already, so I'm just putting here the bullet points as a reminder. In 
general, all these bullets here are provided by test framework, and are listed in the book (my opinion) only for 
completeness.

#### Fresh fixture setup
* **in-line setup**
* **delegated setup**
* **creation method**
* **implicit setup**

#### Shared fixture construction
* **prebuilt fixture**
* **lazy setup**
* **suite fixture setup**
* **setup decorator**
* **chained tests**


### Chapter 21 - Result verification patterns

#### Verification strategy
* **state verification**
* **behavior verification**

#### Assertion method styles
* **custom assertion** - we create a custom assertion method, with **intent revealing name** in order to save space, 
  and avoid repetition 
* **delta assertion** - custom assertion method that compares pre-test state with the post-test state. Used mostly 
  in the situations where we don't have any control over fixture setup.
* **guard assertion** - added when we want to avoid **tests error**, and get **test failure** when the flow does not 
  meet the criteria we want it to meet. We use it too, to avoid conditional statement in the test.
* **unfinished test assertion** - we just *fail()* the test if it is still work in progress.


### Chapter 22 - Fixture teardown patterns

Actually I'm just listing here the contents, as there's nothing in this chapter that would require describing here.
I have the knowledge presented in the chapter already, so I'm just putting here the bullet points as a reminder.

#### Teardown strategy
* **garbage-collected teardown**
* **automated teardown**

#### Code organisation
* **in-line teardown**
* **implicit teardown**


### Chapter 23 - Test double patterns

This chapter is usually seen as the **cornerstone of test doubles' naming**. Unfortunately, due to different usages 
of them in testing tools, we have a real mess nowadays which is actually which. I recommend reading these notes closely.

**Test double** is a generic term, that represents an object, which substitutes (doubles) the object, that is 
necessary for our test, but for some reasons is unusable in our context. As an example we can provide DAO, that is 
hard to use in real version, as we usually don't want to run unit tests against the DB. However, a great caution is 
advised - here is a direct quote from the book.

> Of course, we have to be careful when using Test Doubles because we are testing the SUT in a different configuration
> from the one that will be used in production. For this reason, we really should have at least one test that verifies
> the SUT works without a Test Double. We need to be careful that we don't replace the parts of the SUT that we are
> trying to verify because that practice can result in tests that test the wrong software! Also, excessive use of Test
> Doubles can result in Fragile Tests as a result of Overspecified Software.

I think that every heavy-supporter of *London School* (via usage of mocking frameworks) should read that aloud a 
couple of times!


#### Test doubles' types
* **test stub** - is a collaborator, that provides a specific response for the SUT. Actually this is what we mostly 
  use in everyday programming life, although it's usually being called 'mock'. Its main job is to return a specific 
  value for given inputs. Mostly in order to test untested code,
  some corner cases or exceptions. There are two types of it - *Responder*, which returns valid data, to execute
  every bit of business logic, and a *Saboteur*, that returns errors/throws exceptions. Its main purpose is to mimic
  application failures.
* **test spy** - it is actually a **test stub**, but with *recording functionality*. Its behavior is the same as for 
  **stub**, the difference is in how (or if at all) we deal with this object in the verification phase - it is used 
  then to verify if our SUT used its spied-on collaborator in a valid/expected way (e.g. with parameters of specified 
  values). Although, what differentiates it from the **test mock**, is that it's the test method verification phase 
  knowledge/job, to check the constraints and to choose which ones we exercise.
* **test mock** - this is actually the most misunderstood ones here. Due to the fact that we use term **mock** all 
  over, usually as a synonym to **test doubles** in general. However, in the book **test mock**, is actually a 
  combination of a **stub** and a **spy**. In general, we create a **mock** to serve as a **test double**, but we 
  put specific expected behavior for it during creation. Later, in the verification phase, we just call its *verify* 
  method. I think that code example taken from the book will describe it best:

```java
ConfigurableMockAuditLog mockLog = new ConfigurableMockAuditLog();
mockLog.setExpectedLogMessage(helper.getTodaysDateWithoutTime(), Helper.TEST_USER_NAME, Helper.REMOVE_FLIGHT_ACTION_CODE,
                              expectedFlightDto.getFlightNumber());
mockLog.setExpectedNumberCalls(1);
  
//  mock  installation
FlightManagementFacade facade = new FlightManagementFacadeImpl(); 
facade.setAuditLog(mockLog);
  
//  exercise
facade.removeFlight(expectedFlightDto.getFlightNumber());
 
//  verify
assertFalse("flight  still  exists  after  being  removed", facade.flightExists(expectedFlightDto.getFlightNumber()));
mockLog.verify();  // THAT'S THE MAIN PART - EXPECTED INTERACTIONS/PARAMS/VALUES ARE CONTAINED WITHIN MOCK LOG OBJECT
```

* **fake object** - is not mock/double per se - it usually provides full-blown functionality of the collaborator, 
  although in the very simplistic way. An example of such object would be a map-based DB implementation, instead of 
  using DAO objects. It gained a lot of traction recently, especially for testing DDD/hexagonal applications. The 
  main reason for its usage is avoiding slow tests (hence the example with DB), but it also increases the quality of 
  the tests, as it avoids over-mocking.
* **dummy object** - objects passed only to satisfy compiler, or to comply with the interface. In the most 
  simplistic case it can be just NULL passed around. It is differentiated from other types mostly to indicate, that 
  the specific test method does not care about this param/object. 
 

#### Test double construction
* **configurable test double** - this is de-facto standard today, especially when we're using mock frameworks. In 
  the setup phase (no matter if setup-setup based or inlined) we can easily configure values we expect from the 
  **test double**. 
* **hard-coded test double** - the opposite of the above one. We just put hard-coded value in the **test double**.

The last type - not put in the above divisions - is **test-specific subclass**. It is a class that inherits from SUT,
in order to expose some data/state verification functionalities. In the Java world it's very common to use 
*package-private methods* for that, which are not part of the public API. In other languages we just use inheritance,
to comply with the SUT interface, but we additionally expose data, we don't want exposed in the PRD-ready code. 


### Chapter 24 - Test organisation patterns

Chapter begins with a simple notion of **named test suite** - which contains different tests, but linked in some way.
**Test suite** contains numerous **testcase objects**.

#### Test code reuse
* **test utility method** - as simple as it sounds - when we have some repetitive logic used in tests 
  (utility/assertions/setup code) we just introduce **utility method**. 
* **parameterized test** - self-explanatory 

#### Testcase class structure
* testcase class per class
* testcase class per feature
* testcase class per fixture

#### Utility method location
* testcase superclass
* test helper


### Chapter 25 - Database patterns

* database sandbox
* stored procedure test
* table truncation teardown
* transaction rollback teardown


### Chapter 25 - Design-for-testability patterns

* dependency injection
* dependency lookup
* humble object 
* test hook

# Chapter 26 - Value patterns

* literal value
* derived value
* generated value
* dummy object