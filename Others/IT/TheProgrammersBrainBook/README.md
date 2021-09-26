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