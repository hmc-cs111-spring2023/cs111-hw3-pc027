# Interview project

## The user and a language

This section describes who the project would serve and why a language might be a
good way to meet their needs.

### What's the need?

_What need is met by your idea? Who are you helping? What is that person's
experience like now? What would their experience be like if you could help
them?_

People often brainstorm ideas by writing down whatever comes to mind and organizing them later. This can be students trying to find ideas and sources for an essay, travelers planning a trip to some destination, or an all-purpose note sheet for random thoughts and to-dos. However, the result of brainstorming is often hard to parse because of information overload. Nonetheless, there is generally some existing organization within the brainstormed document and a desired organization of these ideas post-brainstorming. An example would be turning potential places to visit into a formal itinerary for the traveler's case.

At this moment, there are usually pre-existing file templates that people can copy and paste their ideas or apps that walk users through creating a document with some structure from scratch. However, neither of these solutions helps users sift through the information they already have - meaning they might potentially have forgotten or missed details that seem trivial but are actually important. 

If I could help them, I want to give users a tool to do a coarse re-ordering of their documents so that those hidden connections may become more visible. I believe this tool should not be a substitute for those templates or apps mentioned earlier. Instead, users should be able to use this tool quickly so that the later parts of the planning process (whether for an itinerary, essay, or some other format) can be smoother.


### Why a language?

_Why is a DSL appropriate for your user(s)? How does it address the need?_

A DSL for this scenario is appropriate because it can be an interface to quickly sift through the content without the fatigue from manual editing. A general API can also do the same, but since the aim is to automate a task in the writing process, a DSL can be more easily designed so that users do not have to context-switch to a “programming” style of thinking and helping people stay “in the zone” of writing.

This need is domain-specific - it focuses on a subset of word documents that have an implicit or designed order and modules that can be identified by keywords. The limited expressiveness is also guaranteed because this task is focused on reordering existing data, rather than editing the data itself. 


### Why you?

_What excites you about this idea? How did you come up with it?_

I interviewed my high school friend (who works in sales/marketing) about her experience with computers. She recently booked a flight for a trip and ran into a lot of issues with booking flights. Our conversation then verged into planning for travel, which is how this idea came about.

This idea is exciting because it involves balancing between “programming” for users that are likely not programmers with enough notation to prevent confusion (like the Perl vs AppleScript example from the last homework). It might also get my friend to be less fearful of breaking computer-related things and try writing scripts to help her tasks without feeling like she is “programming”.


### Domain

_Describe the project's domain in five words._

Brainstorm, planning, and text processing


### Interface (syntax)

_How might the user interact with the language? What does programming look
like? Why is this the right way to interact with the problem domain?_

Writing in the DSL should live in a GUI similar to ContextFree. The user should first identify the file for reordering in the program, just like how users would need to identify images for image processing DSLs.

The documents I am focusing on are those intended to have some order. Additionally, these structures are repeatable and can be identifiable by keywords. For example, an outline should have paragraphs, and within paragraphs, there should be arguments, each supported by a quote and an analysis. Text that should be in the same structure should also be identifiable by certain keywords. 

Based on these observations, the programmer should provide two sets of keywords - one for structure, and one for content modules within the structures. After defining these keywords, the user should also be able to define the ordering of information by ordering these keywords. An optional syntax decision could be allowing users to define synonyms of keywords.

Note that documents may contain data other than text. The language should assume certain characteristics about these other data types. For example, images will be classified into the same content module as the text in the lines before or after it. Tables and checklists that do not contain the defined keywords will have their separate section as an appendix. The reason for these assumptions decision is that the users of this language will involve people who have little to no experience with programming, and non-text data will require more annotations (and therefore more programming) to understand its content. Additionally, the intent of this DSL is coarse ordering to prevent information overload; figures are likely large enough that they do not contribute to the problem as much as blocks of text. 

Users should have the option (but do not need to) to give a name or location for the output.


### Operation (semantics)

_What might happen when a program runs? How does a program interact with the
user? What kinds of errors might occur, and how might they be communicated to
the user?_

Users should click a “run” button on the GUI to run the program.

The high-level order of actions when a program run is as follows:
- Check that the given file exists
- Create a coarse-grain view of the types of data that exist within file
- Obtain keywords that the user provides
- Detect the location of keyword occurrence and section text by distance from the keyword, whitespace/indentations, and implicit rules/assumptions
- Note any keywords that could not be found in document; validation on the user-indicated constraints
- Create a new document, and iteratively paste information based on the user-identified ordering of keywords
- At the end of the document, indicate any errors

The GUI should indicate when the new file has been created, or failure to create the file. The file should be in .doc or .docx format.

Again, since users are likely not programmers, I want to reduce the number of errors available. If errors do arise, then the user should know the crux of the problem immediately. I envision the error message to be similar to HTTP messages - a simple message that summarizes the problem, and a code that they can reference some documentation for additional information. The main “fatal” error that might occur is that the given file cannot be found, or that the new file cannot be created. 

Other issues that would create a “suboptimal” output should all be warnings. Examples of this include keywords that cannot be found, non-text data that the program detects, and recursion in the given keyword order. The program should have default behaviors when these characteristics are detected during the validation process. There should also be a constraint on how long a program can run in the case that the DSL missed some edge cases. Warnings should be visible as a list in the GUI, as text within the generated document, or as a comment.


### Expressiveness

_What should be easy to do in this language? What should be possible, but
difficult? What should be impossible or very difficult?_

It should be easy to coarsely order any text-only document in this language. It should also be easy to create modules of keywords and rules that can be re-used when defining the order of the document. 

One possible, but difficult function of this language is to create highly hierarchical orderings in this language. The syntax is intended to be simple as it assumes high-level reordering, but the need necessitates some way of creating nested structures. However, having many nested layers would probably make for messy code in this DSL. This kind of difficulty would likely arise for any code intended to fine-tune choices.

It should be impossible to do recursion, conditionals, or duplication of data in this language. It should also be impossible to generate non-document file types like videos. Additionally, this language should only work with the English language - other languages have different styles of an organization that should alter the many assumptions that this language makes to create the final output.


### Related work

_Are there any other DSLs in this domain? If not, describe how you know there
aren't and conjecture why not. If so, describe them and provide links. How well
do they address the need? Are there any particularly admirable qualities of the
language? Are there parts of the language you think could be improved?_

There are DSLs related to this domain. Itinerary creation is used as an example in this Java internal DSL tutorial. This paper shows a DSL-like excerpt of travel itinerary configuration in XCOSEML, which is an extension of the COSEML language (which seems quite DSL-like as well, but I have not spent enough time reading through the documentation to be confident about this claim). These DSLs are proof-of-concepts that a DSL can be created to address the need.

My guess for why there is no DSL specific for this need is because the annoyance is mild enough that people take it for granted as part of the process of organizing documents. Additionally, the more people put up with this annoyance, likely it is that they become better at sorting through vast amounts of information. 

COSEML info: https://user.ceng.metu.edu.tr/~coseml/coseml.pdf


## The Project

This section examines whether the idea makes for a good CS 111 project.

### Suitability

_If someone were to work on this project, what percentage of their time would be
spent directly engaging in the **language** aspects of this project (e.g.,
making language design decisions), as opposed to "systems" aspects of the
project (e.g., implementing a complicated semantics that doesn't require a lot
of language design)?_

About 50-60% of the time would be spent engaging with the language aspects, while 40-50% will be working on the systems aspects of this project. There are equally as many concerns about how much natural language should be incorporated into the DSL as how many customizations should users be able to define and assumptions that the program should make.

### Scope

_How big an idea is this? How ambitious is this project?_

I think the DSL for this idea is a well-scoped idea for the class, and the inputs and outputs are relatively easy to parse and generate. Since this need is, at its root, a text-processing problem, many parts of the project can be reduced down to strings to simplify the implementation.

### Benefits and drawbacks

_Why might this be a good idea for a project? Why might this not be a good idea
project?_

The benefits of this project include familiarity with the domain. The problem is also well-defined, and constraints can also be easily transferred into code. The project also has the flexibility of not adding too much optimization between constraints as the goal is to have loosely-ordered documents. The drawbacks of this project include dealing with multiple data types in the “backend” of the DSL without revealing it to the user. This limited information may cause some unintended issues and edge cases that are difficult to understand at the moment.
