# Notes-on-Browser-Compatibility-and-Transpilation

Question: How do Javascript developers address the gap between the newer Javascript syntax conventions, and the Javascript syntax that browsers can recognize?

This is an especially hard problem because there exists many different browsers, operating systems, and hardware form-factors. Each of these can potentially read and interpret Javascript differently. This is a problem, because writing Javascript that works in one browser, may not work in another. Here are some of the most browsers you may already be using, or recognize.

![image](http://royalpingdom.wpengine.com/wp-content/uploads/2011/06/browser-logos.jpeg)

How are those browsers broken up by popularity?

![image](https://upload.wikimedia.org/wikipedia/commons/c/c5/StatCounter-browser-ww-monthly-200901-201707.png)

## ECMA International, Brendan Eich, and Browser Compatibility

How do software developers manage to build anything that even works in this type of ever-changing environment?

Enter ECMA International.

* ECMA is an industry association founded in 1961, dedicated to the standardization of information and communication systems.
  * **ECMAScript** is a standardized version of scripting language developed by Brendan Eich, called Javascript.

Ok, but who is Brendan Eich?

* Brendan Eich was working at Netscape as a web developer in the early 1990's and built the initial version of Javascript. Unfortunatly, Netscape as a company, did not survive. As Netscape began to go under, Brendan Eich wanted to keep the language alive, and implemented a standard that would guide the path of Javascript.

Javascript became ECMAScript, and blew up, and now it's in every browser, and it's crazy, and it's a part of everything and it's everywhere, and so we need to do a good job of making sure all the Javascript developers' heads don't explode with different versions and updates and we're all on the same page and everything, and right now that page is called **ES6**, but it's real name is ECMAScript, but that's confusing so just call it **ES6**, and so the whole thing is: 'hey, can we make sure all the browsers understand **ES6** and everything? like, can we all agree to just get along?'

Ok, so, that's **browser compatibility**. Make sense?

A really good tool for checking browser compatibility is caniuse.com. You can searchup any feature or function, and it will show you the browser compatibility matrix. It looks like this:

![image](https://www.webpagefx.com/blog/images/assets/cdn.sixrevisions.com/0494-07-can-i-use-css-category.png)

## Transpilation and Babel

What happens when you check canIuse.com, and realize the feature you need to build is (frustratingly) not supported by all modern browsers?

Babel to the rescue!

* Babel is a javascript library that you can use to convert new unsupported Javascript (ES6), into a older version (ES5), that _will most likely_ be support by all modern browsers.

  * **Transpilation** or **Transcompilation** is the process of converting one programming language into another.

## Using Babel via NPM in your project:

To automatically use Babel to transpile code in your project, we need to setup our project to use the Node Package Manager (NPM). NPM needs to be installed _before_ Babel.

### Installing NPM

* developers use NPM to access and manage _node packages_.
  * node packages are directories that contain Javascript code written by other developers, that can help to reduce duplication of work and avoid bugs.

So, the first step is to install NPM. Do this with following command, in the root directory.

```
npm init
```

This command creates a **package.json** file in the root directory.

* a package.json file contains information about the current Javascript project. Some of this information includes:
  * Meta-Data - project title, description, authors, and more.
  * A list of packages required for the project. (If another developer wants to run your project, NPM looks inside the **package.json** file and downloads the packages that are listed. )
  * Key-Value pairs for command line scripts. You can use NPM to run these shorthand scripts to perform some process.

### Installing Node Packages

* We use the the **install** command to install packages locally. The **install** command creates a filder called **node_modules** and copies the package files into it. The install command also installs all of the dependencies for the given package.
  * crazy side note: when we install Babel, npm also installs more then 100 other packages that are dependencies for babel to run properly.

**Remember, Babel is an NPM package, and we install it in our project using the _NPM install_ command**

Now that we've installed Node, and NPM, we can move onto installing Babel in your project, by running the following two commands in the terminal.

_command 1_

```
npm install babel-cli -D
```

* _the babel-cli package is comprised mainly of command line tools._
* _the -D flag instructs NPM to add each package to a property called devDependencies in the package.json file. This is useful because once that project's dependencies are listed in the devDependencies property, other developers can run your project without having to install all the packages separately. Instead, these other developers can just use the 'NPM install' command, and it instructs NPM to look inside the package.json file, and download all the packages listed in devDependencies._

_command 2_

```
npm install babel-preset-env -D
```

* _the babel-preset-env package is contains the core code that actually does the mapping between ES5 and ES6._

Once you've installed Babel in your project, you need to tell Babel which version of the Javascript source code you are using, so that you can automatically transpile the ES6 to ES5. You do this inside of a file called .babelrc, which should live in the root directory.

* Specifically, use the 'presets' property, with the value of '[env]'. It should look like this:

```
{
 "presets": ["env"]
}
```

There is one last step before we can transpile our code. We need to specify a script in the package.json file that initiates the transpilation.

* Inside the package.json file, in the 'scripts' property that holds all of the command line shortcuts, we need to add the 'build' script.

```
"scripts": {
  "test": "echo \"Error: no test specified\" && exit 1",
  "build": "babel src -d lib"
}
```

When you run the "npm run build" command from the root directory of the project, it will write the transpilied code to a new directory called 'lib', and a file called main.js.

_Last command_
npm run build
