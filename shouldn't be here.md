# Project Management Framework at MiCareo

Why do we need something like that ?

Our current project development scheme is very free : there is little to no control about what should be done, and how should it be done.
This was ok up to some point, but it is now necessary for us to have a stricter framework to frame development :
* Write professional quality code for the actual commercial product
* Ensure code quality and responsibilities. It is also useful for FDA application for the parts that will need it.
* Better sense of priorities, which leads to better productivity
* Better integration of future addition to the teams and easier eventual outsourcing of parts of the projects.

## Situation

MiCareo is a Medical device company. The product - and only part of the software - is regulated by FDA.

The project development follow a much longer cycle than software in many other industries. Plane, Spatial and Banking software probably have similar specificities.

Software is only a part of the project, and not a core part : it must follow the global guidelines of the company, and is therefore framed in a Waterfall-based project management scheme.


There is actually two quite different software related activities that is handled by the same team :

* research (doesn't need to follow these guidelines, since it is not directly going to be in the product)
* internal software (doesn't need the same level of attention as commercial product, but would not be a bad idea to follow roughly the same guidelines)
* commercial software, that will be sold with the device to the clients. 


The projects we are working on are very varied :

* Automatic Data Collection : Database client written in C++, integrated with LabView
* Data Analysis tool - mixing internal and commercial purpose. Database driven application, with currently undefined interface(s), in Python
* Reviewer : Web Application (locally hosted) (Java Spring MVC)
* Image Analysis : Java library to analyse, with integration with the database. Both for internal research and Commercial purpose



This documents will identitfy all the issues that need to be handled, collect information about how is it done in other companies, and finally try to give a begining of answer about how do I think it should be done.
It will mainly discuss general guidelines to be folowed globaly when working of sotware at MiCareo, and ensure they can be used and adapted to the specificities of each subproject, and how.


### Topic of concern

Multiple, very different aspect of programming and managing projects must be handled :

* (sub)Project Management
     * Productivity (meet deadlines)
     * Efficiency (work is focused on important matters)
     * ...
* Code Quality
     * Code Readability & maintainability
         * Naming Conventions
         * In code documentation
     * Testing (*Note : This is not the 'official verification' as requested by FDA, since it is done by developers themselves
     * Efficiency of the code
     * Code Review
     
* Documentation


## Project Management

The software projects are all framed in the global Waterfall model, and are currently being thought as a 'modified' waterfall model. It seems completely inefficient to try to change this, which is in itself a good decision.

However, the Waterfall model is used to define the outlines of the development :
It analyses the requirments and specification and define an architecture for the solution. After the implementation, verification and validation are done.
For the implementation of the solution, we don't need to keep the waterfall structure with the long cycles, and try to have something more flexible and dynamic.

Some methodologies at the implementation level will make it easier to ensure code quality - such as TDD (test driven development), Documentation Driven development, and Behavior Driven Development. and BDD.

### Agile inspiration

Most modern methodologies are derived or part of the Agile philosophy. While we don't want to completely adopt Agile ideas, we can use them to design an environment suited for us :

In particular, the 'tickets' based project management encourages code modularity, responsibilities and  collaboration.

The task to be performed make up a list of tickets - which is basically an advanced shared TO DO List.
Everyone is able to comment and give opinions on each task, but the task is assigned to one developper (or group) who is responsible for this part of the code.

How to handle these tickets is the big question.

#### For us ?

I don't know the official Agile methodologies. They all aim to tackle all the issues of project management, so it is already ruled out.

But I want to use the tickets for managing the implementation.

In clear, the global Waterfall will define a concrete architecture of the solution. From there, we can identify a list of tasks need to be performed.
These task will mostly be 'implement a functionality'. 

* It is important that the tasks are 'atomic' : they only implement one functionality, and they require very little code. The precise architecture we have thanks to the waterfall model should allow that.
* The tasks don't need to be 'flat' : some may be more important than others, and some might even be 'optional'.  When we have deadlines, each task will need to be assignated to a deadline, be definitely not necessarily the same one.
* Beside, there is going to be a hierarchy of tasks : some will only be available to perform after others are finished.


One of the software developper will then chose a task - or be assigned a task by the project manager that has the responsibility that the priorities are respected.
He will them implement it, following the other guidelines of the company.

**After** a task, he can push his implementation, and some code quality control (testing, review, etc...) may be done.

#### Some Methodologies

##### TDD

At the core of Agile, and works very well with the idea of tickets

Explain how it works, where it can be modified


Detail the limits and how can it be improved upon

##### Inside Out

Show how to modify unit-testing TDD to create a more 'complete' framework. 


#### BDD, DDD 

Explain a bit these two other methods, 

#### What about us ?

Detail what I chose among this, and why.

Maybe this need to be put with the `For us?` part, but in here.

Make sure the choice is convenient 


(Advantages : make sure that what we have is tested, make sure that we don't randomly do more than what we planned, make sure that at some point, we always have a deliverable product.
Image Analysis is maybe one part that do not beneficiate so much from the Ticket tdd, but i think it shouldn't be harmed by it either.


#### Tools

Which tools could we consider to help us, for the project management part (ie. Tickets, Time management, ...)

Gantt
Ticket Systems : Trello, GitHub Issues (+ 'sugar coating'), etc...
Other ?

most of them will be in the code quality part, because they deal with the code quality. (mention that they are there)


## Code Quality

### Code convention

Two ways of going with this, and I don't know which one is better

* Follow usual conventions for each language (Google's C++, Python PEP8, whatever exists in Java)
* Decide a general

A mixed convention, with company level outlines and language specific details might be a good solution too.

Many convention would agree on some points :

* Make the name of variables clear
  * Do not use 'invented' abbreviations for variables
* Comment only the non obvious parts of the code (and should avoid writing code need comments to understand it)


What matters is clarity!

### In Code Documentation

As said in the conventions, in code comments are not required, and should not be essential.

However it is realy important to use comment to describe the utility of each file, class and function.
These comments should be written following specific conventions that would allow to use it for generating doumentation (javadoc, sphinx, doxygen)

They are extremely useful because :

* They provide a separate structured documentation
* They provide an inline description of the units of the code
* They should show how to use each units to perform the functionality provided by the unit. (and can even be used for simple automatic testing, using DocTest in Python for exmaple.

It doesn't mean that it should be the only documentation the programmer need to provide.

### Testing

Addressed by the project management in some parts. What needs to be added ? Why and how?

+ Tools and techniques is very important. How to test the different projects that we have ?

Unit testing frameworks

Mocking 


Quickly give overview of strategies to test each projects we have
  * Web based applications are a bit special
  * Image Analysis is a bit special, but not too much. Explain how could we transpose the unit testing to image analysis


### Reviews

It is important to do code review in a company. 

Note : I am not talking about the 'official' code review verification activity imposed by FDA, I don't know the constraint about it.

Developper of a same team can have many advantages from code review :

* Everyone has a good understanding of the company's codebase
* Reviewer learn from reading other people's code
* Code itself will be improved from the comments reviewer made to the implementer

However it takes some time, and it is not really trivial to do it right.
Need to find to good tool, and the good rythm.

### ?


## Documentation

Other than code documentation, other documentation are required.

I am not talking about 'architecture & design justification' and other design documents, since they should be done at a higher level than what I am considering here.

The code implemented may need some detail on how it works, and why was it implemented like that. Since the biggest of the design is already , this parts will not be big and essential, but should have a way to keep record of it.


## Other Remarks

### Ressources 

List of interesting links and blabla

