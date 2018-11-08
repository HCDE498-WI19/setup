# Getting Started in HCDE 498 #

This tutorial will help you set up your computer for the rest of the quarter. More installs will come up and be addressed, but this should make things relatively painless for the first few weeks! I am assuming that everyone in this class has taken HCDE 310 and remembers the basics of how to use Git and Bash/Terminal,so those will not be addressed in detail here.

## Step 0 ##

Create an HCDE 498 folder to hold all your files and folders for this class. You should put it somewhere easy to find/navigate to like your desktop.

## Step 1 ##

Install Google Chrome!

If you do not already have Chrome, you should download it for this class! It has great developer tools that make it easy to see how your HTML/CSS code is being interpreted. Other browsers have these tools as well, but we recommend chrome because it is the most used browser on the web and because its tools are easy to use (just right click and choose "inspect element" on a part of a website to see what's going on).

Link (https://www.google.com/chrome/browser/)

## Step 2 ##

Install Visual Studio Code (Link: https://code.visualstudio.com/)

We recommend using VS Code as your main code editor for this class. It is free, open-sourced, and has great extensions to make your life easier. It also has great documentation and many different shortcuts (https://code.visualstudio.com/docs). Try opening this file in VS Code and then clicking a link while holding ctrl/command.

## Step 3 ##

Install Node.js (Link: https://nodejs.org/en/)

To check if you already have Node.js, put this command into bash/terminal:

node --version

(You should reinstall to the latest stable version of node if your version of Node is before 8.11)


{ripped from info 340
Node.js is a command line runtime environment for the JavaScript programming language—that is, a program that is used to interpret and execute programming instructions written in JavaScript. Later in the quarter, we will be doing most of our javascript testing in the browser instead of in Node, but we will still use Node for other reasons. Node provides a platform for installing and running a wide variety of “helper” programs that are frequently used in web development.

Installing Node also installs an additional command line program called npm. npm is a package manager, or a program used to “manage” other programs—think of it as a command line “app store” for developer tools and libraries. npm is the most common way of installing and running a large number of tools used in professional web development.

}

You can install packages "globally" using this syntax:

npm install -g PACKAGE-NAME

To test this out, install "live-server", which will prove to make your life a lot easier this quarter, with this command:

npm install -g live-server

This is not the only way to install packages and there are other methods that are much more useful, especially for doing projects. Please see the extra steps for a deeper explanation of npm and do not try to install more packages until reading that in full.

## Step 4 ##

Test out live-server! In bash/terminal, navigate to the folder that this readme.md file is in. Type in this command:

live-server

If it does not start automatically, open up the localhost site given in the terminal.

The page that is being shown is the "index.html" file that is in the folder you are in. This is the defualt page that websites will look to at the root, but you can have other html files that are directed to from the "index.html" file, that will be explained later in the quarter. The "style.css" file is also the default css file to be used on websites. Your folders with website information should always have an "index.html" and "style.css".

Try changing some of the text in the "index.html" file and saving. Did the webpage change? Using live-server will make web development easier because you will not have to refresh the webpage every time you want to see how a change will look, just save your file and see the results?

Congratulations! You should be all set to start creating websites and doing exercises for this course.

## Bonus Steps ##

### Format on Save ###

One add-on type command for VS Code that I really like auto formats your code when you save it. Here is how you activate it in VS code:

Find the gear icon in the bottom left corner, and click the settings option.

In settings, click the "..." in the top right corner and click the option to open settings.json.

In the settings.json file, type this in:

"editor.formatOnSave": true,

Now, when you save your files your code will format itself according to the file type. Try it out for yourself in an .html or .css file. You can set the value to "false" if you want to turn it off.


### NPM Deeper Explanation ###

(This is all ripped from the info 340 book)

Importantly, note the included -g option. This tells npm that the package should be installed globally, making it available across the entire computer, rather than just from a particular folder. Because you want to be able to use a command line utility like live-server from any folder (e.g., for any project), command line utilities are always installed globally with the -g option.

It is also possible to omit that option and install a package locally. For example:

npm install lodash
Will download the lodash code library (a set of useful JavaScript functions). This package will be placed into a new folder in the current project directory called node_modules/, and can be imported and used in the current directory’s code. (It’s called a local install because the package is only available to the “local” project). You will of course need to install local packages once per project.

Because node packages can be very large, and projects can have lots of them, you want to be sure to not commit the node_modules/ folder to version control. Make sure that the folder is listed in your .gitignore file!

package.json
As projects become large, it is common for them to build up many dependencies: packages that must be installed in order for the program to work. In other words, there needs to be a certain set of packages in the project’s node_modules/ folder. npm is able to keep track of these dependencies by recording them in a specialized file called package.json that can be placed inside the project directory. A package.json file is a text file containing a JSON list of information about your project. For example:

{
  "name": "example",
  "version": "1.0.0",
  "private": true,
  "description": "A project with an example package.json",
  "main": "index.js",
  "scripts": {
    "test": "jest"
  },
  "author": "Joel Ross",
  "license": "ISC",
  "dependencies": {
    "lodash": "^4.17.4",
    "moment": "^2.18.1"
    },
  "devDependencies": {
    "html-validator": "^2.2.2"
  }
}
(You can create one of these files by using the command npm init in the current project directory, and then following the instructions to fill in the fields).

Notice that there are two packages listed under "dependencies": lodash and moment (the ^4.17.4 indicates which version of lodash). You can use npm to automatically install all of the packages listed under "dependencies" (as well as under "devDependencies") using the command:

npm install
Thus using npm install without any arguments means “install all of the requirements that have been listed for this project”. This is a good first step any time you download a project or checkout a repository from GitHub.

When installing specific packages, you can have npm automatically add them to the dependencies list by using the --save option:

npm install --save lodash
will install lodash locally, and add it to the package.json file as a dependency.

Similarly, the --save-dev option will instead save the package in the "devDependencies" list, which are dependencies needed only for development (writing the program’s code) and not for execution (running the program).

If you want to use a globally installed package in your local project (e.g., have it be a dependency but not have to download and install it again), you can use npm link to “include” the global package locally. For example, the below will allow you to use a globally installed version of lodash so you don’t have to download a copy for the project:

npm link lodash
Be sure to link any global packages before you run npm install so you don’t download any packages from package.json that you already have!

You can uninstall packages using npm uninstall, or can remove packages from the dependencies lists simply by editing the package.json file (e.g., with VS Code).

To sum up, you will use three commands with npm to install packages:

npm install -g PACKAGE-NAME to globally install command line programs.

npm install to locally install all of the dependencies for a project you check out.

npm install --save PACKAGE-NAME to locally install a new code package and record it in the package.json file.

While npm is the most popular package manager (and the one utilized in this course), there are others as well. For example, Yarn is a package manager created by Facebook that is compatible with npm and is quickly growing in popularity. Note that you will generally need to use one package manager or other; don’t try to mix them in a single project!