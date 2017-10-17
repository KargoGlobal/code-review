# Performing Code Reviews at Kargo
Code reviews are an integral part of the development process at Kargo. They ensure our code is cleaner, easier to work in, and help teach you some new skills along the way. Anyone can review code, but improving how you perform code reviews is a skill that takes experience. Here are some tips for getting started, from basic concepts to more advanced ones.

## The Basics

### Style / Formatting
* Does the code style and formatting match the rest of the codebase? For JavaScript, Kargo recommends the [Airbnb Style Guide](https://github.com/airbnb/javascript/blob/master/README.md), so that's a good place to start in making suggestions.
* Ensure they're using the appropriate spaces or tabs for indentation (depending on the codebase). 
* For something like ES6, for example, is the developer correctly using `const` and `let`? Are there any `var` references that should be used as `const` and `let`?
* JavaScript has many ways to declare a function - are they keeping things consistent with other areas of the codebase?
* Are there brackets opening and closing in the right spots? 
* Varible and function names should be using the `appropriateCase` for `that_particular_codebase`. 

### Nomenclature
* Look out if all added variables are used
* If code being refactored, make sure that all functions are still in use
* Look out for variable names that don't mean anything to you. A good variable name should be clear as to what it represents.
* Look out for magic numbers - values in code should be referenced by meaningful name
* VariblesAndFunctionNamesShouldNeverBeSoLongThatTheyBecomeSentences: Keep things concise when possible and offer suggestions if things get a bit long winded.

### Comments
* The top of each file or class should have a definition explaining the purpose of that file or class.
* Each function should have a single-line comment unless it's utterly clear what the function does.
* Complicated areas of code or long sections of code should contain comments describing what they're doing.
* If there is some complicated math or a long-winded conditional, suggest a comment to help break it down.

### Does it Work?
* It is highly recommended to checkout the branch and test it on your local machine.
* If any unit tests fail or if you notice issues when testing the functionality, report them back to the developer with detailed steps to reproduce.


## Intermediate

### Do You Understand It?
* You should understand the code you're reviewing. If there is any aspect of the code you don't understand, it's likely that others will have trouble with it as well. 
* If it's uncommented, you should ask the developer to write a comment explaining what it's doing.
* If it's commented, it may be time to talk to the developer about re-architecting it in a way that is more readable.

### Duplicate Code & Long Files
* Follow the 3 strike rule - if code is duplicated more than two times in a repository, it's best to recommend some refactoring so we're  reusing existing code rather than recycling.
* If a file is getting so long that you start losing track of what's going on in it, now's a good time to suggest some new patterns to break up the code into smaller pieces.

# Advanced

### Major Refactors
* Lorem ipsum
