# Project Management Framework at MiCareo

https://en.wikipedia.org/wiki/Software_development_process

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
     * Code Ownership
     
* Documentation


## Project Management

The software projects are all framed in the global Waterfall model, and are currently being thought as a 'modified' waterfall model. It seems completely inefficient to try to change this, which is in itself a good decision.

However, the Waterfall model is used to define the outlines of the development :
It analyses the requirments and specification and define an architecture for the solution. After the implementation, verification and validation are done.
For the implementation of the solution, we don't need to keep the waterfall structure with the long cycles, and try to have something more flexible and dynamic.

Some methodologies at the implementation level will make it easier to ensure code quality - such as TDD (test driven development), Documentation Driven development, and Behavior Driven Development. and BDD.

#### Some Methodologies

##### Agile Methodologies

I don't know much about Agile methodologies.

* They are usually complete and strict framework, and doing it 'half' is meaningless
* It's hard to start without having a consultant/teacher to explain about it, and without specific software (usually expensive?)

Since we want to keep the Waterfall model for the big outlines, we can directly rule out Agile. But we can use some of the ideas to setup the implementation part of the waterfall model.

Most modern methodologies are derived or part of the Agile philosophy. While we don't want to completely adopt Agile ideas, we can use them to design an environment suited for us :

In particular, the 'tickets' based project management encourages code modularity, responsibilities and  collaboration.

The tasks to be performed make up a list of tickets - which is basically an advanced shared TO DO List.
Everyone is able to comment and give opinions on each task, but the task is assigned to one developper (or group) who is responsible for this part of the code.

How to handle these tickets is the big question.


##### Test Driven Development

TDD is at the core of Agile, and works very well with the idea of tickets. The main idea is that the test must be written first, and then the code is written to pass tests. Then a refactoring step - ensuring that the code is good, and not only 'passing the tests' is necessary.

Here is a picture showing the workflow in TDD
![TDD Lifecycle](https://upload.wikimedia.org/wikipedia/commons/thumb/0/0b/TDD_Global_Lifecycle.png/800px-TDD_Global_Lifecycle.png)

More specifically, here is a list of steps for TDD :




TDD is far from perfect, and here are the most important errors :

* TDD is focused on unit-testing, and may makes us forget to make sure the actual product is working
* Desiging the code based on tests is not a better design idea than designing test on design - they should be independant.
* TDD encourages *continuous testing* wich requires fast test. Pushed to the extreme, test will be run every few minutes, so each test must be extremely fast. While most useful tests should indeed be fast, it is counter productive to rule out a test because it takes more than a second.

* Excess is usually the issue : we are testing for improving code quality, not just for testing and having a good coverage!


TDD can (and has been) be modified to avoid these pitfalls. Three popular methodologies have been built on top of TDD, and all have the same common things : TDD is awesome, but shouldn't be used directly at top level.

##### Outside in

Show how to modify unit-testing TDD to create a more 'complete' framework. 

Outside In is one of the modification of TDD.

Rather than simply designing a unit test for each small tasks the idea is more 'recursive' :

* We have the **functionalities** for the program. These functionalities are usually taken from specifications, but they could also eventually come from the design, and be defined 'by module', or both.
* We write tests for each of these functionalities. They are *functional* or *system* tests. These functionalities are normally described as simple natural language sentences.
* Then we chose to implement one of these tests that doesn't work. 
* We use TDD to implement this functionality (test - design - implementation - refactorisation) It is ok if these tests actually 'know' the design
* We chose a new functionality

It somewhat help at deciding 'what to test' 

This is apparently particularly suited for Web developemnt


#### Behavior Driven Development

Behavior Driven Development is another refinment of TDD, very popular with Agile methods. 
https://pythonhosted.org/behave/philosophy.html

Outside-In can actually be considered as a kind of BDD. In practice, pure BDD is mainly useful for communicating about tests between developpers and non-technical persons such as QA and managers. It aims at taking into account the view of multiple stakeholders for the testing phase (methodologies for translating 'natural language' to actual tests).

It goes well with a more complete TDD and Agile methodologies, but may not be perfectly suited for our case, as it start being useful at a higher level, already taken into account in the global company's methodology.

An interesting things can be taken from that would be the practice of using *Mocks* to do testing independantly between different modules, ie. even if other parts are not written yet.

#### Documentation Driven Development

As the name implies, it is a twist on TDD, where *documentation* comes first, and not tests. Tests are designed based on this documentation. 

The main outline is actally simply a TDD, but before designing the tests, the first step is now : Write or update the documentation.
Before touching any single part of the code, the documentation should be edited (and reviewed) to reflect the intended change.

Indeed, for user perspective, a functionality not documented is the same as a missing functionality.

Some of the advangtages are : 

* Writing the documentation first will give a good space for customer to talk with dev about the detail of the functionalities (not relevant)
* It ensures that the documentation and the code are always consistant

Reviewing the documentation before actually starting the real work of  testing and implementing seems like a good way to save lots of time. 


While it is globally a good idea, documentation of functionalities is not a priority need for our products, and I believe each developper should be able to document his code however he wants it. (same for testing, the TDD part could simply be 'recommanded' but if we want to test differently it's ok, as long as we have a good list of tests all passing) . This could however be included with an Outside-In method on a higher level.

Documentation Development seems especially good for API develpoment.

http://collectiveidea.com/blog/archives/2014/04/21/on-documentation-driven-development/
https://gist.github.com/zsup/9434452



#### What about us ?


I want to use the tickets from Agile methods for managing the implementation.

In clear, the global Waterfall will define a concrete architecture of the solution. From there, we can identify a list of tasks need to be performed.
These task will mostly be 'implement a functionality'. 

* It is important that the tasks are 'atomic' : they only implement one functionality, and they require very little code. The precise architecture we have thanks to the waterfall model should allow that.
* The tasks don't need to be 'flat' : some may be more important than others, and some might even be 'optional'.  When we have deadlines, each task will need to be assignated to a deadline, be definitely not necessarily the same one.
* Beside, there is going to be a hierarchy of tasks : some will only be available to perform after others are finished.


One of the software developper will then chose a task - or be assigned a task by the project manager that has the responsibility that the priorities are respected.
He will them implement it, following the other guidelines of the company.

**After** a task, he can push his implementation, and some code quality control (testing, review, etc...) may be done.

Detail what I chose among this, and why.

Make sure the choice is convenient 


(Advantages : make sure that what we have is tested, make sure that we don't randomly do more than what we planned, make sure that at some point, we always have a deliverable product.
Image Analysis is maybe one part that do not beneficiate so much from the Ticket tdd, but i think it shouldn't be harmed by it either.

#### TDD

I want to adapt TDD to use it inside our current model. Outside In ideas can be used to guide us on how to do that.
http://osherove.com/blog/2005/2/21/employing-tdd-and-unit-testing-with-waterfall-methodologies.html
http://blog.orfjackal.net/2009/10/tdd-is-not-test-first-tdd-is-specify.html


Using a mix of DDD/Outside-In for the outer level, and TDD forr inner level seems like a good idea.
Need to make sure 'edge-case' are tested and considered as tasks, but still different than main functionalities. 

When using this kind of methodologies, many people will code on the same parts. Need to be careful and set rules about :
* How to modify someone else's code. Do it brutally. talk about it with him. Talk about it with everyone (since the code was not necessarly written by one single person) . ?
* Who is responsible for the code (the guy just did the push) ( + everyone )


I need to do a workflow / flowchart / etc to make sure about how to handle things, and how I see the stuff work. It will be better than the complex explanation. 

Need to add test for each module after or during implementation step ? Whith my current process we are only testing 'functionalities' of each of the module, but not each moule. It may be enough if the code is indeed , but if inside modules have errors on cases that are not tested by current functionalities --> will bring errors when adding things. Should be dealt when adding things ?

#### Priorities & Time Management

We should have a planning. But beside that, I think everyone should be able to handle their work and be productive however they want. Could have a time tracker for the whole group to know how much time we are spending on each task, but it seems like too much micro-managing.

Even the order of the tasks, each person in the group should be able to figure out what does it need to do, without having a 'project manager' that assign tasks. 

The best way to get the best out of people is to let them do however they are more comfartable with
--> even for test first ? Should simply have a continuous tetign (Mavis) environment, and then let it work ?

#### Tools

Which tools could we consider to help us, for the project management part (ie. Tickets, Time management, ...)

Gantt
Ticket Systems : Trello, GitHub Issues (+ 'sugar coating'), etc...

Integrated and coninuous testing  -- need to synchronize the 'tasks' with the test failure ! 

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

Addressed by the project management in some parts. Indeed most modern software development processes put testing at the top of the development process. It helps deciding when and what to test. 

There are still many questions about how should things be tested.

Tests should be independant. It is necessary to ensure that it is possible to easily track what is the issue, what is the work left, etc...

Tools are very useful and language dependant

All languages have great (and similar) unit testing framework :
* Java has JUnit
* Python has unittest, nose and pytest
* 

They all allow continuous testing.

These tests are performed locally. A great way to make sure that the 'important tests' are really passing, a good solution would be to use Continuous Integration tools that would start the tests automatically, everytime new code is pushed on GitHub for example.
* [Travis CI](https://travis-ci.org/) is a great tool to do this, but is quite expensive (130USD/mo for start-ups)
* Many other extists, we could do a quick survey

#### How to write tests

No matter what the unit is, a unit test should  

DO's: 
* Make sure every non-trivial method is tested EG: get_account_status() → test_get_account_status() 
* For every branch of logic within each method, create EG: withdraw_cash() → test_withdraw_test_normal() test_withdraw_test_overdraft() test_withdraw_test_disallowed() 

DONT's: 
* No need to test trivial getters/setters 
* Don't stack all the logical pathways into a single long test for the method being tested. Instead, split them up as above



+ Tools and techniques is very important. How to test the different projects that we have ?

Unit testing frameworks

####Mocking 

Mocking is an important technique that allows to test modules by completely ignoring whether other modules are properly implemented or not.
Basically, you create a *mock* which is an object pretending to be part of the code you don't want to care about. You can set it up to return whatever you want, and can ensure that it has been called with good parameters (if function) or that the good methods have been used.
It seems not so trivial to start using mocks efficiently, but it is necesasry to ensure that tests are really independant, and is very useful for testing complex applications, such as Database driven application (could emulate a database?) or the Image Analysis (could make sure the pipeline is working, and could make sure the good transformation are applied on the picture.



#### Testing Database and WebApplications


#### Testing the Image analysis




#### Beside Unit Test

Unit Test are only one part of testing. Many modern software process also put emphasis on system tests.

Shouldn't forget user tests : when you actually use the product, does it behave as expected ?

This is normally not easy to do - and will be required to do quite formally for some FDA applications maybe? - but we have the chance that the whole bio group is directly using all the products that we want to give to customers. They are therefore our beta-testers (but should still give them well tested code to use or they will lose their time, so the company will lose time asd well!!)

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


DDD requires the documentation about functionalities to be written first. This may be a little bit too 'strict' in our case


## Other Remarks

### Ressources 

List of interesting links and blabla

Note : 

* A good way to handle code reviews : we don't directly commit to the main stuf. We work locally, and then when the task is implemented, we issue a pull request. This pull request willbe reviewed. It seems to be the way some of the tool sare working

https://guides.github.com/introduction/flow/


# Tools (need to sort them)

## CI

https://github.com/integrations/scrutinizer-ci
https://github.com/integrations/sonarqube
https://github.com/integrations/cnverg
https://github.com/integrations/lgtm
https://github.com/integrations/pullapprove
https://github.com/integrations/hound
https://github.com/integrations/coveralls
https://github.com/integrations/solano-ci
https://github.com/integrations/snap-ci
'https://github.com/integrations/circle-ci
https://github.com/integrations/reviewninja
https://github.com/integrations/codecov
https://github.com/integrations/codacy
https://github.com/integrations/buildkite

https://github.com/integrations/zube
https://github.com/integrations/apiary
## PM
https://github.com/integrations/trello
https://github.com/integrations/waffle
https://github.com/integrations/huboard
https://github.com/integrations/codetree
