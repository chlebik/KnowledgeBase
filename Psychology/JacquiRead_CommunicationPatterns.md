# Communication Patterns - A guide for developers and architects

## Visual communication

### Chapter 1 - Communication essentials

* **know your audience** - who and when will be looking at the diagrams? How detailed should they be? How technical?
* **mixing levels of abstraction** - it is an **antipattern!** Whenever possible - separate different levels of 
  abstraction into separate visuals. **C4 diagrams** to the rescue!
* **representational consistency** - make sure that every next level of diagram clearly indicates which high-level 
  concept is being presented (e.g. with dashed box/background/label). 

### Chapter 2 - Clarify the clutter

* **color overload** - don't overuse colors. Provide legend, and try to group things per color.
* **boxes in boxes in boxes** - empty space is as important as the content. Try to differentiate background color. 
  Label everything. **Don't be smart. Be readable!**
* **relationship spiderweb** - make relationships/arrows as clear as possible, avoid tangling/crossing
* **balance text** - avoid long sentences, try to remove unnecessary parts 

### Chapter 3 - Accessibility

* **relying on color to communicate** - well, not everyone can see/differentiate between colors. Use 
  shapes/legends/symbols.
* **include a legend** - for everything. Colors/shapes/patterns/texture/abbreviations - but don't fall into the trap 
  of the overload. If possible - use toggle to show/hide the legend or use a link if it's bigger.
* **appropriate labels** 

### Chapter 4 - Narrative

* **the big picture comes first** - as it says - even if the audience is interested in the nitty-gritty details start with a big picture diagram/image.
* **match diagram flow to expectations** - make reading a flow of the diagram resemble natural language reading. So start 
  somewhere in the upper left/center and go down/right.
* **clear relationships** 

### Chapter 5 - Notation

(those below are **!!!antipatterns!!!**)

* **using icons to convey meaning** - icons should be used as an addition, not as the only source of truth/meaning.
* **using UML for UML's sake**
* **mixing behavior and structure** - as with SRP in SOLID, same here - don't mix the types. Diagram should show one conceptual thing.
* **going against expectations** - sometimes it can be used to catch audience's attention, but that's it. If they expect architecture
  design to be presented, don't show them ventriloquist show ;) Same applies to colors/shapes

### Chapter 6 - Composition

* **illegible diagrams** - it's often an **antipattern** to use default size/canvas in drawing tools. Adjust the one you use to 
  the format that the users will be reading/watching the visual from. If you can't edit the visual, slice it into pieces.
* **style communicates** - don't fall for the default style of the diagramming tools. Use the style that best fits to the domain/project,
  or the one that the target audience is used to.
* **misleading composition** - charts/diagrams can be tweaked to look better for specific cases (e.g. votes), or misleading
  by exaggerating the size/relations. Pay attention to it - both as a creator and as a viewer.
* **create a visual balance** - as title says. When possible - balance the diagram visually (ordering/rows).

## Multimodal communication

### Chapter 7 - Written communication

* **simple language** - no more comment needed. Use. Simple. Words.
* **acronym hell** - as with the legends for the diagrams, please don't assume people know the acronyms. Explain the 
  whole acronym first time you use it - both when speaking and writing.
* **structured writing** - use pyramid shape to explain. Start with the most top/overall statements and work your 
  way down with the arguments and details.
* **syntax of technical writing**
  * *strong verbs* like govern, amend, extract, realize, notify, convince, inspect, guide, scan, serve, transform, raise, generate, and ensure
  * *short sentences*
  * *precise paragraphs*
  * *consistent vocabulary*
  * *audience empathy* - figure out how much the audience knows, and what they want to get from your reading, and 
    help with that.


### Chapter 8 - Verbal and non-verbal communication

* **encoding messages**
  * *using the acceptance prophecy* - approach others with the assumption that you like them, and they like you. It 
    cant be 'felt in the air', and therefore creating self-fulfilling prophecy.
  * *giving your full attention* - especially in today's world with short attention span and multithreading. Stop. 
    Look at. Listen.
  * *using body language and gestures* - always place them within the culture context. Avoid wide gestures, which 
    can be seen as hostile.
* **decoding messages**
  * *battling bias* - be aware of them. They will never subside, but it's better to limit their influence 
    (confirmation bias, hindsight bias, groupthink)
  * *being present* - variation of giving full attention from above. Be mindful of what's going on, don't assume or 
    guess. Limit your ego.
  * *awareness of cultural differences* - yeah, that can bite in the ass. 
* **influence and persuasion** - make sure to be prepared in terms of knowledge. No amount of communication 
  excellency will make up for the lack of preparation. However, polite and kind communication is also important. 

### Chapter 9 - The rhetoric triangle

At its core, **the rhetoric triangle** is a framework for understanding the three key elements of persuasive
communication: *ethos*, *logos*, and *pathos*. *Ethos* refers to the credibility and trustworthiness of the 
speaker, *pathos* to the emotional appeal used to engage the audience, and *logos* to the logical and rational argument
presented.

* **ethos**
  * *establish your credentials* - in the company's setup usually not needed. When presenting/writing for the 
    external audience it's required. But don't over-boost yourself!
  * *use trustworthy sources* - yeah, ChatGPT does not cut it.
  * *be transparent* - clearly say why you're doing what you're doing and why in this specific way. Conflicts of 
    interests should be clearly stated.
  * *demonstrate your knowledge* - show your skills in dedicated places. Don't hide it.
* **pathos**
  * *tell a story* - lots of resources about it out there. Humans don't like facts, but they love stories. Not only 
    success ones - failures can be very engaging too.
  * *speak from the heart* - meaning be sincere and authentic. People sense when you're not being honest in that area.
  * *use vivid language and strong imagery*
* **logos**
  * *use data and facts*
  * *make logical connections* 
  * *use reasoning and argumentation*


## Communicating knowledge

### Chapter 10 - Knowledge Management Principles

* **products over projects**
  * *project mindset* - **ANTIPATTERN** - create knowledge about the product, not about the projects. Projects are 
    transient, product stays with the company forever and ever (mostly).
  * *product mindset* - mindset created around the product changes all the other behaviors and people. Thinking 
    about the product in terms of "changesets" from the last finished projects is very reductive in nature.
* **abstractions over text** - wall of text is of no good. Present visually and abstract away
  * *lists* - start with most important, use consistent form of points, use numbers for order
  * *tables* - highly indicate headers, use only one type of value per column, no more than 2 sentences in a table
  * *visual abstractions* - e.g. stars rating/harvey's balls
  * *word clouds* 
  * *charts, graphs and diagrams*
  * *other abstractions*
* **perspective-driven documentation** - pattern to use putting specific emphasis on with who you're communicating.
  * *DRY* - it can be applied to documentation/knowledge too. You should not duplicate docs - reference all the time!
  * *fractal perspectives* - embed perspective in another, and if needed - another. They're not copies - they're 
    references that way therefore not violating DRY.
  * *implementing perspectives* - tags and metadata;flat structure;embedding;layers;templates
  

### Chapter 11 - Knowledge and people

* **get feedback early and often**
* **share the load** - especially if you're leader/architect/etc - delegate sharing knowledge as wide as you can!
  * *nonproprietary forms* - use simple formats/tools that do not require heavy setup or licenses
  * *accessibility* - both in terms of permissions to edit but also ease to find/start collaborating
  * *collaboration* - use tools that allow parallel editing
  * *roles and responsibilities* - it may be right to assign specific pieces of docs/knowledge to the concrete role 
    played by the team members. However, make sure not to create bottlenecks and always have a substitute person for 
    the role.
  * *additional techniques* - lunch&learn, templates for repetitive pieces of knowledge, save time in a sprint
* **just in time architecture** - yup, delay all the decisions as long as possible.


### Chapter 12 - Effective practices

* **ADR** - there's whole subchapter here, and it's worth reading as a whole. Start [on the wiki](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions)
* **architecture characteristics** - usually related to *non-functional requirements*. List [here](https://en.wikipedia.org/wiki/List_of_system_quality_attributes) 
* **all documentation is code** - if possible, try to version it, make it accessible and part of the project. 
  Autogenerate whatever can be autogenerated.


## Communicating remotely

### Chapter 13 - Remote time

* **synchronize time** - if you're in the multi-timezone setup, be aware of that and schedule communication based on 
  that with clear boundaries set
  * *time zone*
  * *empathy and compromise* - extra time (outside of regular working hours) should be compensated or taken in turns
  * *split shifts* - when possible distribute shifts for the benefit of people's commitments&lifestyles
* **respect working patterns** - people may not work in the same manner as you. Accept it.
  * *communicate availability* - always, whether in email signature or on chat status
  * *defend part-time hours* - be aware of people not working full time. Make sure that they don't feel left out.
  * *plan for holidays* 
  * *account for geography and culture* - work time differs between Spain in July, and Finland in December.
  * *recognize real working capacity* - people don't only code. They have meetings, docs to write, etc.
* **improve energy and productivity** - rested people, are efficient and performing people.
  * *control notifications* - limit the amount and the time to respond if possible. Schedule time windows to deal 
    with notifications, and snooze/filter as much as possible.
  * *automate tasks* - when possible (mostly email) create rules/filters to do triage of the messages. Bots for 
    Slack/Discord are the same - to remind people about things.
  * *work with other's rhythms* - productivity during the day varies. When requesting communication/response from 
    people take that under consideration.
  * *schedule for energy* - that is a follow-up from the previous one. Pick low-energy times during a day for the 
    meetings, and do the actual work when you're in a peak shape. That also applies to meetings themselves - 
    anything longer than 60 minutes should have a break, to let people recover a little.
  

### Chapter 14 - Remote principles

* **meetings to sync**
  * *synchronous vs async* - synchronous should take place only if it brings value. Period.
  * *enhance meetings* - agenda/keep the time/only required people/always have a meeting summary
* **async to think**
  * *async advantages* - well, they're obvious ;)
  * *async obstacles* - don't include too many people/more fatigue when using tools like virtual dashboards/limited 
    body language
  * *direction matters* - depending on the type of the matter sometimes async/sync is better. 
  * *async methods* - email/IM/prerecorded audio&video/forum and Q&A platforms/management tools/wikis
  * *enhance async* - automate whatever you can and set clear rules of async communication
* **remote-first working** 
  * *remote-first vs remote-friendly* - **first** means that this is the main focus area. **Friendly** it means that 
    it is allowed but not optimized for.
  * *remote-first benefits* - huge list of them - read the book
  * *evolving to remote-first* - same as above


### Chapter 15 - Remote channels

* **symmetrical email** - there should be specific rules for using email - in terms of their subjects, response time,
  etc.
  * *email reasons*
  * *email expectations*
  * *email clarity*
  * *email tips* - long list of them - read the book
* **online presentations** - usually they're harder than in-person ones
  * *audience engagement* - use chat for Q&A, observe for reactions/emojis, make more slides to give more stimuli to 
    the audience
  * *presentation content* - agenda slide does not need to be detailed. Use picture/quote/story. Also use 
    points-to-take or action points slide at the end to increase retention for the audience.
  * *screen shares* - useful when want to engage the audience or show work in progress or experimentation. 
* **remote tools and governance** - there's a lot of them described here. I'm just listing the subchapters - for 
  specifics you need to read the actual book
  * *selection techniques*
  * *remote tools*
  * *data proliferation*
  * *security*
  * *tool efficiency*
  * *tool governance*

