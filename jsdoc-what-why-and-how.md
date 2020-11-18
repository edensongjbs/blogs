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


## So, How Do We Use It?!

As I mentioned above, the [Official Docs](https://jsdoc.app/) are pretty straightforward and thorough, so I'll keep this section to some bare essentials and then highlight some of my own favorite features.

1) Install & Configure

JSDoc is easy to set up as a development dependency in Node.

Simply, type `npm i -D jsdoc` in your project's root directory

JSDoc will run with a default configuration, but if you'd like to change any of these default options, you'll want to create JSON configuration file in the root directory called "jsdoc.json".  Here is my configuration, which deviates in a few ways from the default that can be found [here](https://jsdoc.app/about-configuring-jsdoc.html).  The link also provides details on other alternate configuration options:

```
{
    "source": {
        "include": ["src"],
        "includePattern": ".js$",
        "excludePattern": "(node_modules/|docs)"
    },
    "plugins": [],
    "templates": {
        "cleverLinks": true,
        "monospaceLinks": true
    },
    "opts": {
        "recurse": true,
        "destination": "./docs/",
        "tutorials": "./tutorials",
        "readme": "./readme.md"
    }
}
```

We'll also want to configure our project's package.json with a custom node script to generate our docs:

```
"scripts": {
    "docs": "jsdoc -c jsdoc.json"
  }
```

2) Some Basic Block Tags

Writing your own JSDoc comments is easy!  In VSCode, you simply need to type '/\*\*' and the IDE will generate a full JSDoc comment block.  If you hit 'enter' from inside the block, new comment lines (preceded with the '*' character will) will be automatically generated as well.

I've written some code below to illustrate some available tags and how to use them.  Note that the block comments are JSDoc comments pertaining the demo domain where the line comments are my annotations of the JSDoc comments.  Apologies if that's confusing!!




3) Type-Checking

Below, I'm going to illustrate using some type-tags.  Similar to the last section, the my comments are annotating the actual JSDoc block comments.

As you can see, when I violate one of my typing "rules," VSCode will flag the error with a underline squiggle and provide a helpful error message pertaining the specific violation.

4) Generate the Docs



Those are probably the most essential features of JSDoc, but I've included a few of my favorite features below:


5) In-line blocks for additional resources



6) Support Markdown Syntax in Comments!



7) Extend the standard to React with Prop-Types and Better-Docs
