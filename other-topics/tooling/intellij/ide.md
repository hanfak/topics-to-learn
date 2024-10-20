# IDE - Intellij

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [IDE - Intellij](#ide-intellij)
	- [Shortcuts](#shortcuts)
		- [Live templates](#live-templates)
		- [Links](#links)
	- [Setup/preferences](#setuppreferences)
	- [Plugins](#plugins)
	- [Scratch Files](#scratch-files)
	- [Links](#links)
	- [Other IDEs](#other-ides)

<!-- /TOC -->

I exclusively use Intellij as an IDE for developing code with either java, javascript, bash, sql and scala. It has many plugins that help with development and lots of shortcuts to help develop and refactor code effectively.

## Benefits

- Spot compiler issues, bad code style, unneeded code etc
- Offers hints
- custom templating, ie sout or psvm
- Can generate code for you so you don’t have to type it. Getters and setters, equals and hashCode, and toString
	- Becareful, to when generating complex code like hashcode etc, have tests in place
- Has refactoring tools that can automatically move your code in a particular direction while keeping the compiler happy
- Can run your tests and help you debug problems.
- Can even help you with tools or systems external to your application code—for example, version control, database access, or code review

## Shortcuts

There are loads of shortcuts (See link below for a list) but that will be a waste of time writing them instead here are few areas that should be learned to be an efficient developer.

A great way to practise, is to not use the mouse when developing

Another way to practise is to turn off tabs.

`ctrl + shift + a` gives a search for all actions best command to know and use often (NOTE: for mac: `cmd + shift + a`)

- Moving around project files and within file
- Refactoring
- copy,cut, paste, highlighting, find, replace
  - globally, files or in individual Files
- Moving between windows
- Running tests and Builds
- Debugging
- Version control
- Book marking files
- multi line selection

NOTE: There will be some specific shortcuts and ways of using IntelliJ in different sections of this repo.

- https://blog.jetbrains.com/idea/2020/05/debugger-basics-in-intellij-idea/

### Live templates

Help reduce amount of typing for common code pieces

- test -> junit test template
- sout and soutv -> System.println.out and same but add the variable above
- psvm -> public static void main
- ???

### Links

- Code golf

I also have editor tabs turned off. This leads me to use shortcuts for navigating between files and classes

## Setup/preferences

## Plugins

Cool plugins which help with productivity

- rainbow brackets
- syntax highlighter
- markdown support
- string manipulation
- ???
- language specific - docker/yaml/javascript/scala


## Scratch Files
- version control - github, gitlabs

Great for copying json or xml and then doing some formatting. Plus they dont go away

## Links

- http://hadihariri.com/2014/01/06/intellij-idea-minimal-survival-guide/
- https://zeroturnaround.com/rebellabs/getting-started-with-intellij-idea-as-an-eclipse-user/
- https://youtu.be/pX2jyeWs1qw IntelliJ Super Productivity in 45 Minutes
- https://www.youtube.com/watch?v=cK19rE2V9UY Victor Rentea - The Secrets of the Fastest Java Developers on Earth



## Other IDEs

- Eclipse
- Netbeans
- vscode

I would avoid using text editors such as atom/sublime as these will slow down work as compliation does not happen straight away and lots of other stuff is missing. But they are good for simple scripting ie ruby/python.
