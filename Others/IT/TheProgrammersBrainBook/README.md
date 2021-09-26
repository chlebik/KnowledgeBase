# The Programmer's Brain by Felienne Hermans

## Part 1 - On reading code better

### Chapter 1 - Decoding your confusion when coding

Types of confusions when reading the code:
* **lack of knowledge** - issue in *LTM (Long Term Memory)*
* **lack of information** - issue in *STM (Short Term Memory)*
* **lack of processing power** - Issue in *working memory*

Information -> Filter -> STM (RAM memory)-> Working memory (CPU) -> LTM (SSD disc)


### Chapter 2 - Speed reading for code

LTM supports the limits of STM/working memory. The more we have stored in LTM, the more patterns we're able to 
recognize, and therefore help our STM/working memory do their work.


### Chapter 3 - How to learn programming syntax quickly

Use flashcards with spaced repetitions.


### Chapter 4 - How to read complex code

Cognitive load:
* **Intrinsic load** - how complex is the problem
* **Extraneous load** - what are the outside distractions
* **Germane load** - created by having to store things in LTM

* Techniques to reduce it:
  * refactoring
  * replace unfamiliar code constructs
  

Techniques to help with working memory overload:
* create dependency graph
* use state table


## Part 2 - On thinking about the code

### Chapter 5 - Reaching a deeper understanding of the code

The only part of the chapter that I find interesting or new is a study, that shows, that actually the linguistic 
skills, are a factor when learning programming (not necessarily math). The rest of the chapter is full of 
overthought typologies, which have no real value to me.

### Chapter 6 - Getting better at solving programming problems

In general the outcome of the chapter is that we're using mental models when dealing with software. Humans can store 
different models of one thing simultaneously. Therefore, it's possible, to mix them and loose the overall 
understanding of a thing.

### Chapter 7 - Misconceptions: bugs in thinking

Knowledge transfer between existing models in memory and new ones, can have two outcomes:
* **positive transfer** - when existing model helps to understand/create new one (for loop)
* **negative transfer** - when existing model actually prevents us from understanding new things (checked exceptions 
  in Java vs exceptions in C#)

Preventing misconceptions when learning new language:
* keep an open mind
* study common misconceptions
* ask for advice of experienced programmers


## Part 3 - On writing better code

### Chapter 8 - How to get better at naming things

General conclusion is that naming is hard ;)

### Chapter 9 - Avoiding bad code and cognitive load: Two frameworks

**Code smells** are causing high cognitive load. Depending on the type of code smell it can cause:
* overloading the capacity of working memory
* no possibility for effective chunking or chunking gone wrong (code clones)

**Linguistic antipatterns** is a second framework - when casual language concepts in the code are not representing 
what they say they do (eg. <em>isValid</em> does not hold a boolean but int). They cause increased cognitive load on 
the developers.


### Chapter 10 - Getting better at solving complex problems

To get better at solving use one of two strategies:
* internalization - make parts of common problems stored in LTM. The more you remember (from doing!) the easier it 
  is to fetch this knowledge/skill.
* worked examples - how other people solved specific problems

The last type of cognitive load is **germane load**. It occurs when the *intrinsic* and *extraneous* loads are so high, 
that there's no way we can move anything from working memory or STM to LTM. In that way we cannot actually **learn** (in 
terms of remembering). That's why giving recipes for solutions when tackling problems are causing **germane load** 
to decrease, and enable us to actually remember something.


## Part 4 - On collaborating on code

### Chapter 11 - The art of writing code

Interruptions are a problem, and as studies suggest - there's LOTS of time wasted trying again to get into the zone 
(which requires 'warm up'). There are three techniques that help with coming back after interruption:
* **store your mental model** - when model you currently have in mind is stored externally (paper/code/etc), it's 
  possible to skip 'warm up' phase
* **help prospective memory** - write down what you were thinking that you had to do next
* **label subgoals** - write down every small step that is needed to tackle the specific problem


### Chapter 12 - Designing and improving larger systems

**Cognitive dimensions of code bases** are design principles for codebase. They're used to evaluate the usability of 
existing one, or be a heuristic for create new. Here are the dimensions used:
* *error proneness* - strong types are better than dynamic types
* *consistency*
* *diffuseness* - how much the programming languages concepts take (in terms of space)
* *hidden dependencies*
* *provisionality* - how easy it is to think while using the tool
* *viscosity* - how hard is to make changes into the system
* *progressive evaluation* - how easy it is to execute partial code
* *role expressiveness* - how easy is to see the role of a specific part of the code
* *closeness of mapping* - how close the language/code is to the domain which problems it solves
* *hard mental operations*
* *secondary notation* - possibility to add extra meaning to code (eg. comments or named params)
* *abstraction* - describes if the users of the system can create abstractions as powerful as built-in the language
* *visibility* - how easy is to see other parts of the system


### Chapter 13 - How to onboard new developers?

> One of the reasons more-senior people often struggle with effectively teaching and
explaining is the “curse of expertise.” Once you have mastered a certain skill sufficiently,
you will inevitably forget how hard it was to learn that skill or knowledge. You will, therefore, overestimate how many new things a newcomer can process at the same time.

[Neo-Piaget stages for development](https://en.wikipedia.org/wiki/Piaget%27s_theory_of_cognitive_development#Four_stages_of_development)
<br/>
[Dreyfuss model of skill acquisition](https://en.wikipedia.org/wiki/Dreyfus_model_of_skill_acquisition)


Advise how to make onboarding better:
* limit/decrease cognitive load (describe the proper vocabulary to the newcomer)
* limit tasks to one programming activity (transcription/exploration/comprehension/searching/incrementation)
* support the memory of the onboardee
* read code together

