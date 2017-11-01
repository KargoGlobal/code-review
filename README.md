# Performing Code Reviews at Kargo
Code reviews are an integral part of the development process at Kargo. They ensure our code is cleaner, easier to work in, and help teach you some new skills along the way. Anyone can review code, but improving how you perform code reviews is a skill that takes experience. Here are some tips for getting started, from basic concepts to more advanced ones.

## The Basics

### Style / Formatting
* Does the code style and formatting match the rest of the codebase? For JavaScript, Kargo recommends the [Airbnb Style Guide](https://github.com/airbnb/javascript/blob/master/README.md), so that's a good place to start in making suggestions.
* Ensure they're using the appropriate spaces or tabs for indentation (depending on the codebase).
* For something like ES6, for example, is the developer correctly using `const` and `let`? Are there any `var` references that should be used as `const` and `let`?
* JavaScript has many ways to declare a function - are they keeping things consistent with other areas of the codebase?
* Are there brackets opening and closing in the right spots? (there may not be a 'correct' style, but it should be consistent within a codebase)
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
* If you are working on a Javascript based project (Node or Angular) then use JSDoc syntax to describe classes, function parameters, and return values including descriptions and types.

### Does it Work?
* It is highly recommended to checkout the branch and test it on your local machine.
* If any unit tests fail or if you notice issues when testing the functionality, report them back to the developer with detailed steps to reproduce.
* Ensure that potential errors are handled gracefully. This is especially important for client side Javascript, where we can't feasibly test every possible device.

## Intermediate

### Do You Understand It?
* You should understand the code you're reviewing. If there is any aspect of the code you don't understand, it's likely that others will have trouble with it as well.
* If it's uncommented, you should ask the developer to write a comment explaining what it's doing.
* If it's commented, it may be time to talk to the developer about re-architecting it in a way that is more readable.
* Understand the codebase you are working on and/or reviewing first. If it's a high-performance / high-throughput application, then it's likely important to optimize for efficiency. If it's a lightweight tag for mobile, you'll likely want to optimize for brevity since every byte counts on mobile.
* In most situations (see previous bullet) prefer clarity over brevity. Unless you are truly optimizing for every byte, it's preferable that other developers understand the codebase and can debug and contribute over being fancy and concise with every single line of code. This means it's usually preferable to write a complex statement in multiple lines of code as opposed to chaining multiple function calls in a single statement:
```
// bad
const a = loadResults(process(x));

// good:
const a = process(x);
const b = loadResults(a);
```
* Watch out for overusage of 3rd party libraries such as LoDash. You can probably cover 90% of your use cases with the most common functions like `_.map` and `_.each`. If you had to scour their documentation to find some underused function, then consider that every other developer will also waste precious time doing so.
* Don't forget about built in language functions and regular old for loops. Sometimes developers will write 3 sequential Lodash function calls, when a single regular loop will do the job.

### Duplicate Code & Long Files
* Follow the 3 strike rule - if code is duplicated more than two times in a repository, it's best to recommend some refactoring so we're  reusing existing code rather than recycling.
* If a file is getting so long that you start losing track of what's going on in it, now's a good time to suggest some new patterns to break up the code into smaller pieces.
* Don't try to solve problems that don't yet exist. It's great to be forward thinking and plan for possible future requirements, but not at the cost of adding complexity, longer code review times, and higher potential for bugs. Solve the immediate problem first and then we'll worry about abstracting or scaling when we need to.

# Advanced

### Major Refactors
* Classes and functions should have singular purposes. If not, they may be difficult to test and can often be refactored into multiple classes or functions.
* If a method is difficult to unit test or it requires an excessive number of mocked functions/classes, it can likely be better written (and more easily tested) as multiple methods.

### Error Handling and Conditional Checks
* In most cases when you are adding a conditional check (e.g. if statement) you should consider alternative code paths as well. How should the application behave if the if statement is not entered? Did the developer add an appropriately handled else condition?
* Often times we expect things to work a certain way, but what should happen if it doesn't?
* Throw appropriate errors that describe what happened to anyone - even someone who didn't work in that codebase
* Don't wrap code in try/catch blocks unless you are actually expecting an error to be thrown in a normal code flow. Otherwise let the error bubble up through the normal exception handling flow.

### Performance and Optimizations
* Look for common memory and performance bottlenecks such as circular dependencies or excessive looping.
* When you see any loops, understand the performance cost using Big(O) Notation. A very common pattern to watch out for is an over-dependency on Lodash or similar libraries:
```
// bad - O(3n):
const mapped = _.map(data, 'myVar');
const filtered = _.filter(mapped, (d) => d > 0);
const results = _.map(filtered, (d) => {data: d});

// good - O(n):
const results = [];
for (const item in data) {
  if (item.myVar > 0) {
    results.push({data: item.myVar});
  }
}
```