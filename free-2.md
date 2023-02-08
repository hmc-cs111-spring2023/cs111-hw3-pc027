# Free project 2

## The user and a language

This section describes who the project would serve and why a language might be a
good way to meet their needs.

### What's the need?

_What need is met by your idea? Who are you helping? What is that person's
experience like now? What would their experience be like if you could help
them?_

There are lots of instances where presentation slides are used as graphic design tools. This may be because Photoshop is expensive and hard to learn, and slides give enough drawing and diagram options for particular use cases. 

However, some of these designs are intended for reuse and often have patterns in them. Like ContextFree, perhaps there is a way to declaratively make these slides/images without having to manually edit the information every time. The next section will give some more examples of use cases.

### Why a language?

_Why is a DSL appropriate for your user(s)? How does it address the need?_

A DSL will reduce the time it takes to create templated presentations, especially for the specific case of color-coded lyric videos. While the current technologies used may be more intuitive because of the visual nature of the videos, proficiency in DSL will allow creators to make these videos and upload them faster. This can lead to more views and subscribers compared to the competition. 

While a regular API may be equally suitable for the job described previously, the control required to generalize this process for other similar cases is easier by implementing a DSL. One example of this is the convention of scheduled posters that VTubers post weekly. The DSL would fit into a data pipeline where schedules on an online calendar may be converted into a list of events as text, and the text and background can then be consolidated by programming in the DSL. 


### Why you?

_What excites you about this idea? How did you come up with it?_

I came up with this idea because I encounter these types of media often due to my interests. One VTuber I watch also complained about the time it takes to create schedule posters, and wish there was some way to simply convert calendar events into posters magically. This also relates to my first idea about multi-lingual subtitling in fansubbing communities. Sometimes the material is audio only, and translators create their own layouts in a presentation-like format and make a video with subtitles from scratch. 

### Domain

_Describe the project's domain in five words._

Image and text processing, presentations

### Interface (syntax)

_How might the user interact with the language? What does programming look
like? Why is this the right way to interact with the problem domain?_

The syntax of this language will lean object-oriented rather than functional because the ultimate goal is to create a composite between images and texts. Therefore, the syntax will need two distinct data structures to represent and group methods. Additionally, operations on images will be more limited than on text by the nature of presentation slides. 

Most programs in this language will start by loading in a set of images and a set of text, as is the norm for image and text processing libraries.

There will likely be iterative loops and conditionals involved in most programs of this language. Loops are a necessary function to generate multiple images for use cases where many slides are needed and can be helpful to create even positioning between different text sections. Conditionals will be useful to determine the styling of objects on these slides. One way to simplify these stylizations is to introduce some method of creating spaces on top of the base image/canvas as placeholder positions for other objects.

The fluency of the language will likely come from method-chaining rather than function composition because it is easier to see the order in which effects are applied. 

Since the output of programs of this DSL is composites of some sort, there will likely be a designated block of code that puts together those images and texts. Users should also be tasked with defining the location and format of final outputs.


### Operation (semantics)

_What might happen when a program runs? How does a program interact with the
user? What kinds of errors might occur, and how might they be communicated to
the user?_

Since this DSL involves two distinct data types, I will assume that it will be built on a statically typed language to help users catch mistakes early. Programming in this DSL will likely occur within the host language’s IDE (instead of a terminal or a separate GUI) to leverage existing tools for code formatting and type checking. 

The high-level order of actions when a program run is as follows:
- Start at the code block associated with composition (similar to Java’s main function)
- Check that the given files exist and are of the correct file types
- Some kind of conversion turns those files into data types that the DSL can more easily operate on
- Apply the programmed transformations onto the DSL’s representation of a blank canvas
- Turn that blank canvas into desired output

Error checking is necessary throughout this process because of various potential visual issues every time a new object is placed onto the canvas. Some examples of errors that may occur are overlapping elements and common object-oriented errors like null pointers and out-of-bound indexes. Since this DSL will rely on the IDE, errors will be shown in the terminal. A logging interface within this DSL will also print more human-readable errors in the terminal.


### Expressiveness

_What should be easy to do in this language? What should be possible, but
difficult? What should be impossible or very difficult?_

Things that should be easy to do in this language are compositing images with text and creating multiple images. Possible, but difficult things to do in this language is any sort of text manipulation. The DSL should assume that the set of texts the user uploads at first is mostly final but allow for minor changes like spelling or punctuation errors. One function that should definitely be impossible is writing recursive loops. However, because this idea relies on the host language, I am not exactly sure how I can manually stop recursive loops. Perhaps this is adding some sort of detection in the compiler or a runtime restriction?

### Related work

_Are there any other DSLs in this domain? If not, describe how you know there
aren't and conjecture why not. If so, describe them and provide links. How well
do they address the need? Are there any particularly admirable qualities of the
language? Are there parts of the language you think could be improved?_

ContextFree is an example of an image-generating DSL. Even though it seems likely, I was not able to find a DSL specifically for image composition. Maybe I wasn’t using the right keywords, but one possible reason may be that people who generally create the things this DSL makes are familiar with design tools like Adobe Photoshop and/or are unfamiliar with coding in general.

## The Project

This section examines whether the idea makes for a good CS 111 project.

### Suitability

_If someone were to work on this project, what percentage of their time would be
spent directly engaging in the **language** aspects of this project (e.g.,
making language design decisions), as opposed to "systems" aspects of the
project (e.g., implementing a complicated semantics that doesn't require a lot
of language design)?_

The time would be split 35/65 between language design and implementation. There are slightly more choices in the systems of the DSL - thinking about intermediary data types that might be necessary to generate these images. In turn, these decisions might affect language fluency itself.

### Scope

_How big an idea is this? How ambitious is this project?_

I think the scope of this project may be a little big because of its reach in both image and text processing domains. Some time will need to be spent to determine the actual boundaries that this DSL span, but the domains that are involved are common with lots of examples for reference.


### Benefits and drawbacks

_Why might this be a good idea for a project? Why might this not be a good idea
project?_

This might be a good idea for a project because I am not familiar with image processing, and I will definitely have to become intimate with the details here. That might also be a reason that this project is not as feasible. Other drawbacks include balancing the complexity of this project with how easy the DSL should read and support for multiple types of data.
