# Free project 1

(Warning to my reviewer: this is the longest of the 3 ideas, partially because of the potential niche domain)

## The user and a language

This section describes who the project would serve and why a language might be a
good way to meet their needs.

### What's the need?

_What need is met by your idea? Who are you helping? What is that person's
experience like now? What would their experience be like if you could help
them?_

There is a vast array of television shows and movies where no subtitles are provided or only exist in the show’s language. Fansubbing has historically been the avenue where these types of videos gain subtitles. Viewers participating in these fandom spaces often want to learn a foreign language. These learners can be fan translators who want to improve their skills in the language.

Dual-language (or multi-language) subtitles can help viewers optimize their learning by visually pairing the dialogue in the show’s language with the viewer’s native language. Fan translators can also exercise their skills in multiple languages. However, free subtitling tools have a relatively steep learning curve, are often time-consuming to use, and generally require a team of fansubbers that specialize in different aspects of subtitling - the “timers”, who create the template with proper timestamps; the “translators”, who write the line-by-line translation within the template; and the “editor/encoder”, who puts the subtitle together with the video. 

Implementing dual-language subtitles puts twice the amount of time for timers and translators for a single video. Since this labor is unpaid and voluntary, dual-language subtitling is not commonly seen in fansubbed videos.

A tool that alleviates tensions between free subtitling software and fansubbers and between creating different sets of subtitles can promote dual-language subtitles in fan-translated videos to help language-learning fans and create extra learning opportunities for the fan translators.


### Why a language?

_Why is a DSL appropriate for your user(s)? How does it address the need?_

An intuitive, declarative DSL can automate the creation of complete subtitles in other languages based on one complete, time-coded, stylized set. Such a tool would leverage existing labor to reduce the time it takes to create subsequent subtitles in other languages, thereby promoting dual-language subtitles in fandom communities. This not only helps language learners but also has the potential to serve a wider demographic of fan viewers. Additionally, this DSL would allow for translations on a pivot language, lowering the barriers of entry for fan translators into the fansubbing community.

In conclusion, a DSL would improve development productivity (a trait Fowler mentions as a reason to use DSL) by automating parts of a task (which Mernik et. al. cites as a common decision pattern for DSLs)


### Why you?

_What excites you about this idea? How did you come up with it?_

I used to be an ESL student and would learn English from cartoons. In recent years, I have participated in fansubbing spaces and have found subtitling to be difficult to learn. Services that allow fans to contribute subtitles easily are also disappearing - one notable example is YouTube removing its community captions interface in 2021. I feel that I have enough domain experience/expertise to understand the problem and create an intuitive solution.

### Domain

_Describe the project's domain in five words._

Subtitling and translation, text processing

### Interface (syntax)

_How might the user interact with the language? What does programming look
like? Why is this the right way to interact with the problem domain?_

A program in this DSL should start off by loading a complete subtitle file in common formats such as SRT or VTT. The DSL should provide features for extracting information about this file, such as the subtitle language, the total number of lines, the timecodes for each line, and the text within each subtitle line. The DSL should also provide support for common fansubbing practices. One example is translator notes - subtitle lines close to the top of the screen, usually for providing additional cultural contexts or explanations for fandom-specific jargon. This should follow an annotation structure that connects to a specific line. 

The features previously described should appear in every program in this DSL. The program should also have a module for creating or uploading texts in a different language. Similar to general text processing, users should declare the method to parse uploaded text. The module should have access to information parsed from the complete subtitle file and link the new text to the information. Finally, users should be able to declare the format to export a subtitle file from the new text, optionally indicating the location or name of that file. 

A useful feature would be some sort of printing of subtitle segments or a visual editor like ContextFree to allow users to preview their existing work before file export. A visualization before export is extremely helpful because of the sheer amount of subtitles for long-form videos. Additionally, such visualizations would allow them to proofread easily. I see this as analogous to “compiling” in LaTeX editors.

Overall, the interface I have described is relatively similar to image processing DSLs. This is the right way to interact with the problem domain because the subtitling problem is also a processing problem. Rather than images, the problem reduces to text processing (and generating) in specific formats.

### Operation (semantics)

_What might happen when a program runs? How does a program interact with the
user? What kinds of errors might occur, and how might they be communicated to
the user?_

When the program runs, it should read the file in such a way that the first operation is always loading a complete subtitle file. Before any sort of file creation, the program should validate the input file for any inconsistencies, such as empty subtitles, subtitles with incorrect timecodes, or subtitle lines that are too long. The features for validation are determined by the inherent characteristics of subtitles and general subtitling conventions. After, the program should check the new text on similar criteria. 

If the DSL has a visual editor like ContextFree, then the visualization should show the input subtitles with the newly created subtitles in parallel. Any errors or warnings can be indicated by color-coding or highlights on the visualization or written as a generic error message if the visualization fails.

Otherwise, a prompt should appear on the terminal that informs users of the results of the validation. If validation succeeded and the user has written code for exporting a subtitle file, the file should be generated and stored based on user inputs, or by some default name and stored in the same folder as the program.

Here is a list of warnings and errors I have thought about so far:
[Error] File compatibility: is input a subtitle/text file of some sort?
[Error] Compatibility with newly created text: is there some sort of mismatch between the newly created set of subtitles and the old ones?
Dimensions that this error can be detected: unequal number of subtitle lines, corrupted timecode data when transferring it to the new text, unintentional positioning of subtitles
[Error] Translation notes on non-existent lines
[Warning] Subtitle conventions: lines in new texts are too long
[Warning] Translation notes missing in the new text when they exist in the complete subtitle file


### Expressiveness

_What should be easy to do in this language? What should be possible, but
difficult? What should be impossible or very difficult?_

Recall that this language is intended to make it easy to create a new set of subtitles by bypassing the clunky nature of subtitle editors. This means the language should easily do all the “clunky” operations. This includes breaking a chunk of translated text into lines (if necessary), transferring time data to the new lines of text, and adding translator notes to subtitle lines.

As mentioned earlier, this problem is in the domain of text processing. Therefore, most text-processing functionality should be possible (but potentially slightly difficult) within this DSL. One example may be minor edits on the newly translated text. Since program validation involves checking subtitle positioning and lengths, this may mean that indexing into the strings may be a possible operation. Users might then be able to use indexing and splicing to edit specific words, but it would be easier to do this in a word processor and reload it into the program.

Anything that changes the information in the completed subtitle file should be impossible. The program relies on this file as the source of truth for creating new subtitle files. Operations like adjusting the time data or the text in that file must be impossible in the language so that the validation flow described in the previous section can accurately detect errors or warnings. The language should also make recursion of any sort very difficult due to the linear flow of reading and validating subtitles. It should also be impossible to export to any non-text-based file format.


### Related work

_Are there any other DSLs in this domain? If not, describe how you know there
aren't and conjecture why not. If so, describe them and provide links. How well
do they address the need? Are there any particularly admirable qualities of the
language? Are there parts of the language you think could be improved?_

There are many text-processing DSLs. One example is generating code from other code. The microservice DSL is one that allows API designers to generate OpenAPI specifications from MDSL. Annotations can be added in Java Spring Boot projects to generate API documentation, and client libraries can be generated from the documentation as well. 

However, I cannot find publicly available DSLs in the domain of subtitling. I believe this is because professional subtitling software has intuitive UI and features that make creating time-segmented templates easy. Additionally, the subtitling workflow is likely much more streamlined in professional scenarios. The general assumption is that there are many subtitle editors with varying capabilities, and people who do subtitling for a living have good enough tools that they wouldn’t need to learn how to script (however much a DSL would make scripting easier) to quickly create subtitles in different languages. Subtitling is also niche enough that maybe people who learn to subtitle do so because of enough vested interest.

MDSL: https://microservice-api-patterns.github.io/MDSL-Specification/generators/open-api.html
Annotations: https://docs.oracle.com/javase/tutorial/java/annotations/basics.html
OpenAPI Generator: https://github.com/OpenAPITools/openapi-generator


## The Project

This section examines whether the idea makes for a good CS 111 project.

### Suitability

_If someone were to work on this project, what percentage of their time would be
spent directly engaging in the **language** aspects of this project (e.g.,
making language design decisions), as opposed to "systems" aspects of the
project (e.g., implementing a complicated semantics that doesn't require a lot
of language design)?_

About 30-40% of the time would be spent engaging with the language aspects, while 60-70% will be working on the systems aspects of this project. 

Less time is spent on language aspects because there are conventions to how subtitles should look on a video. Nonetheless, some language decisions will need to be made regarding annotation, as these types of notes have slightly different conventions between different types of media (ex. American television vs Japanese anime).

The systems aspects of this project are more complicated. While inputs and outputs are easily definable, the inner workings of parsings may be difficult because of large numbers of potential edge cases.


### Scope

_How big an idea is this? How ambitious is this project?_

I think this is a relatively big idea, but modular enough that it can easily be scoped down. Particular avenues to make this project easier are establishing fixed formats of inputs/outputs and not creating the visual editor.

### Benefits and drawbacks

_Why might this be a good idea for a project? Why might this not be a good idea
project?_

This might be a good idea for a project since it essentially boils down to text processing. String parsing is something I have more experience with than parsing other types of media. The line-by-line nature of subtitling means that there are already some sets of rules and constraints, giving me a template to convert those into code logic. This project is also independent of any one specific programming language, meaning more freedom to choose one that has optimal functions to do the task at hand. 

Drawbacks to this project include the lack of an existing DSL in this domain. I would have to be careful about language design decisions because there is no reference for sanity checking. This also makes it harder to identify drawbacks within the implementation. Another potential downfall is that for this DSL to be useful, I should implement some sort of visualization like ContextFree for proofreading subtitles. However, creating that visualization might become the biggest risk of doing this project.

