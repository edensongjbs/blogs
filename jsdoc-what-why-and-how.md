Outline

- What is it?

- Why use it?

- How?
npm install
set up boilerplate
type /**
start noting (ref API docs)
run export command


1) supports markdown comments
2) enforces static typing! (enable type enforcement)
3) note globals, functions, classes, modules, components
4) link to external resources/tutorials and readmes
5) Creates the docs for us!
6) automatic syntax hightlighting in VSCode/Atom etc.
7) Extend the standard to React with Prop-types and 


# JSDoc - What, Why, and How?

A key purpose of writing clean code is to clearly communicate with our collaborators and future selves what our program does, and how it works.  Two of the most effective tools we have for this purpose are comments and API documentation.  JSDoc helps us with both.

## What is it?!

JSDoc is both a markup language and a documentation generator. By following certain conventions while commenting our JavaScript code, we can then use the generator to automatically populate API docs that annotate our variables, functions, classes, modules and more. Furthermore, IDEs like VSCode support syntax-highlighting for our JSDoc comments and can even use our our annotations to type-check our code and throw errors if we violate the static typing "rules."

## Why Use It?!

Let's take these 3 basic features I listed above:

1) Commenting Convention - JSDoc provides a standardized syntax for writing legible and consistent comments.  The block tags ('@') guide us to provide important important information about the full project, the file we're looking at, and the assorted variables, functions, objects, etc. contained therein.  The tags are intuitive and easy to learn and the official [API Documentation](https://jsdoc.app/) describes the tags in detail.  While the tags help guide us to provide useful information, the IDE syntax highlighting helps make these comments easier to read than standard JS comments.

2) Automatically Generate API Docs - This is huge!  I've always struggled to write clear documentation for my projects and JSDoc really takes the guess-work out of it, enforces concision and clarity, and most importantly builds the Doc pages for us.  We can configure JSDoc with a node script to generate our documents with a single line of code: `npm run docs`.  (I'll discuss this further in the "How" section below)

3) Type-Checking - JSDoc provides easy to implement lightweight type-checking without the need to use TypeScript.  By configuring your IDE for type-checking, any errors with mismatched types (assigning a value with the wrong type to a variable, passing a parameter with the wrong type etc.) will be flagged immediately.  This is a helpful warning, allowing us to easily detect issues that may break our code.  However, the code will still run as usual if we ignore the warnings and throw errors (if any) at runtime.





