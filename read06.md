# Read-06

------------------

## What Is Node.js?
  
- project’s home page defination:
- __Node.js__:is a JavaScript runtime built on Chrome’s V8 JavaScript engine.
- Stack Overflow's defination:
- __Node.js__: is an event-based, non-blocking, asynchronous I/O runtime that uses Google’s V8 JavaScript engine and libuv library.

- __The V8 engine__: is the open-source JavaScript engine that runs in Google Chrome and other Chromium-based web browsers, including Brave, Opera, and Vivaldi.
  - It was designed with performance in mind and is responsible for compiling JavaScript directly to native machine code that your computer can execute.
- the creator of Node (Ryan Dahl) took the V8 engine and enhanced it.

      -with various features, such as a file system API, an HTTP library, and a number of operating system–related utility methods.

## Node Binaries vs Version Manager

     - There are various advantages to using a version manager. 
     - For example, it negates potential permission issues when using Node with npm and lets you set a Node version on a per-project basis.

## Node.js  Supporting

- Node has excellent support for ECMAScript 2015 (ES6) and beyond.
- this means that you can write your JavaScript using the latest and most modern syntax.
- It also means that you don’t generally have to worry about compatibility issues.

## Installing a Package Globally

- Node comes bundled with a package manager called npm.
- This command (npm -v): To check which version you have installed on your system.
- This command (npm install -g jshint): To install the jshint package globally on your system.
- This command (jshint index.js):To see a number of ES6-related errors.
  - to fix them up, add /*jshint esversion: 6*/ to the top of the js file, re-run the command and linting should pass.

## Installing a Package Locally

- Create a test folder and open a terminal in that directory.
- Then this command(npm init -y): To  create and auto-populate a package.json file in the same folder.
- Then this command(npm install lodash --save): to install the lodash package using npm and save it as a project dependency.
- Then Create a file named test.js and add the following:
  - const _ = require('lodash');
  - const arr = [0, 1, false, 2, '', 3];
  - console.log(_.compact(arr));
- run the script using node test.js.
  - To see [ 1, 2, 3 ] output to the terminal.

## articles covering build tooling on SitePoint

- [A Beginner’s Guide to npm, the Node Package Manager](https://www.sitepoint.com/beginners-guide-node-package-manager/)
- [A Beginner’s Guide to Webpack](https://www.sitepoint.com/webpack-beginner-guide/)
- [Up and Running with ESLint — the Pluggable JavaScript Linter](https://www.sitepoint.com/up-and-running-with-eslint-the-pluggable-javascript-linter/).
- [An Introduction to Gulp.js](https://www.sitepoint.com/introduction-gulp-js/)
- [Unit Test Your JavaScript Using Mocha and Chai](https://www.sitepoint.com/unit-test-javascript-mocha-chai/)
- [The Anatomy of a Modern JavaScript Application.](https://www.sitepoint.com/anatomy-of-a-modern-javascript-application/)
- if you want to start developing apps with any modern JavaScript framework (for example, React or Angular),
  - you’ll be expected to have a working knowledge of Node and npm (or maybe Yarn).
  - it’s because these frameworks are all available via npm and rely on Node to create a sensible development environment in which they can run.

## The Node.js Execution Model

![img](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2012/10/1516152673node_event_loop.png)

## Conclusion

- JavaScript is everywhere, and Node is a vast and expansive subject.
- Nonetheless, I hope that in this article I’ve offered you the beginner-friendly, high-level look at Node.js and its main paradigms that I promised at the beginning.
- I also hope that when you re-read the definitions we looked at previously, things will make a lot more sense.
