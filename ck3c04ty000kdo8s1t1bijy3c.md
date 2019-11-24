## Walking Through the create-react-app Files

Hey guys, 

In the [previous blog post](https://jormee.hashnode.dev/getting-started-ii-create-react-app-ck2owq9uw005loks1usno0wd1), we looked at how we can get our react applications started with `create-react-app`. This post will walk us through the boilerplate (or template) files created for us by this simple command and how we can use them in building our applications.

For this post, I have created a new react boilerplate called pomodoro and this is what it looks like at the moment.
![react-app.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1573142910226/2wQPh4t8R.jpeg)

And if we open up our project file in the code editor (I use VS code), here's what we have:


![boilerplate files for new react-app](https://cdn.hashnode.com/res/hashnode/image/upload/v1574534295672/Mz4Bu-wAQ.png)

### Walkthrough of All Files

1. `node_modules/`

This folder contains all libraries and packages required for react to run. They consist of many npm packages and any new package you install for your application is stored in this folder. You would notice that this folder has a slightly faded color. This is VS code letting us know that the file is being ignored.

Q: __*What does this mean and why?*__

A: By default, node modules are ignored because of their size and because they are not really needed in the git repo and can be recovered easily. All other files that are/should be ignored are those that are not needed for you application to run and sensitive files that contain sensitive information such as API keys, Authentication tokens etc. We'll look at them more deeply at a later time.

2.`public/`

This folder contains the `favicon.ico` file (which is the small icon file displayed next to the site name in the browser tab), `index.html` file (the main html file of the react app), logos files, `robots.txt` file. (which tells web crawlers which pages can be requested from your site to avoid overloading your site with requests) and a `manifest.json` file, which allows you to specify the behavior of your application when saved on user devices (as PWAs).

3.`src/`

Presently contains all boilerplate codes for starting up, styling and testing our react application. This is the folder where we write all our code, and create each component that powers our app.

4.`.gitignore` file

This file specifies all the files and folders we want git to ignore. The files specified in this file will not be tracked, staged, committed or pushed to the repository because they are not needed for the application to run (e.g. test files) or they contain sensitive information that cannot be exposed (e.g. .env files) or node_modules folder that is too big.

5.`package-lock.json` file

This is an automatically generated file that should not be tampered with. It contains information that describes the tree that was generated exactly, such that later installs are able to generate identical trees, regardless of intermediate dependency updates.

6.`package.json` file.

Earlier, I mentioned that the node_modules can be ignored because they can be easily recovered, the package.json file makes this possible.

This file contains all information about your application such as dependencies (libraries, packages needed for your application to run), dev-dependencies (packages used in building the application, but are not required for it to run such as nodemon), scripts (these defines what is run whenever any of the commands are executed in the terminal. For example, when we run `npm start` in the terminal, what really runs is  `react-scripts start`)etc.

If you clone a repository to your machine, it would not come with the node_modules folder, since it was ignored, hence the project will not run on your device until the node modules required are installed. To install the required node modules, enter the following command into the terminal
```npm install```
or
```yarn install```

This command will check the package.json file and install all dependencies of the project.

Now that we are all full acquainted with the react environment, we can now start to learn the building blocks in the next post in  this series.

### Links

Feel free to visit the following links for further reading on the topics/files we have covered.
+ [package-lock.json](https://docs.npmjs.com/files/package-lock.json)
+ [package.json](https://docs.npmjs.com/files/package.json)
+ [.gitignore](https://help.github.com/en/github/using-git/ignoring-files)
+ [manifest.json](https://developer.mozilla.org/en-US/docs/Web/Manifest)
+ [robots.txt](https://neilpatel.com/blog/robots-txt/)
+ [node_modules](https://docs.npmjs.com/files/folders.html)