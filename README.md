# BFZ GitHub Pages Starter Project

Use this starter code to set up a project that uses packages and publishes to GitHub pages. This tutorial covers the following steps:

1. Get software
2. Set up the project in GitHub
3. Set up the development environment
4. [Optional] Add more packages or secrets to your project
5. Use a workflow


<br />

## 1. Get software

To use this starter project, first download required software:

- [**Visual Studio Code**](https://code.visualstudio.com/): free text editor for desktop
- [**Git**](https://git-scm.com/): version control software; comes with `Git Bash` command-line shell
- [**Node.js**](https://nodejs.org/en/): server-side programming language
- [**Yarn**](https://classic.yarnpkg.com/en/docs/install/#windows-stable): package manager (requires Node to be installed first)

Sign up for a [GitHub account](https://github.com/) and make sure you're part of the [Built for Zero](https://github.com/builtforzero) organization.

<br />

## 2. Set up the project in GitHub

### A. Create a new repository using this project as a template:

- Click on the green **New** button in your GitHub account.
- Under **Repository Template**, choose this repo: `builtforzero/bfz-starter-project`. 
- Enter a custom repository name and description. 
- Create the repository.

### B. Clone the new repository to a folder. 
- Use the [instructions here](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/cloning-a-repository).
- Cloning saves a copy of the repository to your computer.

### C. Set up a GitHub Pages site

- Go to your repository in GitHub. Click on the **Settings** tab.
- Scroll down to the **GitHub Pages** section.
- Under **Source**, select **master** from the dropdown menu. (This will be changed later!)
- **Save the URL** that is generated by GitHub. This is where your project will be hosted.

<br />

## 3. Set up the development environment

### A. Set up your project

Open your project folder in VSCode. Open the terminal. Type these commands into the terminal, one at a time:

1. **`yarn init`**
2. **`yarn add parcel-bundler concurrently gh-pages --save-dev`**

**More Details: What are we doing here?**

1. **`yarn init`:** Initializes the Yarn package manager. This adds several new folders and files to your project, out of which you will only need to directly change the `package.json` file.

    - **`package.json`:** your **project manifest**; aka a record of the dependencies and scripts needed to run your code.
    - **`yarn.lock`** and **`node_modules`**: files that store and manage your project's dependencies. *You don't need to touch these files!*
    - **`dist`** (added after step 4 below): a folder with assets in your `client` folder that are bundled for the web by the Parcel package. *You don't need to touch this file!*

2. **`yarn add parcel-bundler concurrently gh-pages --save-dev`**: Adds the following packages as a development dependency to your project:

    - **[Parcel](https://parceljs.org/):** bundles assets for the web (i.e., translates your modern JS code into a version that *all* browsers can read and understand).
    - **[Concurrently](https://www.npmjs.com/package/concurrently):** a helper package that allows you to run multiple terminal commands in one line.
    - **[gh-pages](https://www.npmjs.com/package/gh-pages):** a package that can publish your project to GitHub Pages.

<br />

### **B. Add Scripts**

Go to the newly-created `package.json` file. In the `scripts` section of the file, copy and paste the following scripts. Replace `ENTER_URL_HERE` with the complete GitHub Pages URL of your project (created in step 2).
    
    "scripts": {
        "dev": "parcel ./client/index.html",
        "predeploy": "rm -rf .tmp .cache dist && parcel build ./client/index.html --public-url ENTER_URL_HERE",
        "deploy": "gh-pages -d dist"
     },

<br />

## 4. [OPTIONAL] Add more packages or secrets to your project

### **A. Add more packages to your project**

- **In the terminal:** type `yarn add package-name`, replacing `package-name` with the package you wish to install
- **In `client/main.js`:** require the package at the top of the file, in the format `const [package variable] = require('package name')`. For example, to use the D3 package, I would add `const d3 = require('d3')` to the top of my `main.js` file. Then, I can use D3 methods like normal.
- Check the documentation of the package to see how to add it to your JS file!

<br />

### **B. Add Secrets**
Environment variables can hold secrets (e.g. API keys) that we need available in our JavaScript code, but inaccessible once published. Here's how to set it up:

- Get the **[Dotenv](https://www.npmjs.com/package/dotenv)** package by running `yarn add dotenv` in the terminal.
- Create a new file in the root directory called **.env**. Add secrets to the file using the format `SECRET_NAME = 123456789`, one line per secret.
- Add the line `require('dotenv').config();` to the very top of your `main.js` file.
- Access secrets within your JS in the following format: `const secret = process.env.SECRET_NAME;`

<br />

## 5. Use a workflow

### **A. During Development**

- In the terminal, run the command `yarn dev` to start the development server.
- Go to http://localhost:1234.
- Make changes to files in the `client` folder, and the page will automatically reload on save.

<br />

### **B. To Publish**

- In the terminal, run the commands `yarn predeploy` and then `yarn deploy`
- Commit all changes to GitHub using the normal workflow: 
  - `git add .`
  - `git commit -m [message]`
  - `git push origin master`
- Visit your GitHub Pages URL to view the published project

<br />

## Further Reading & Resources

**[Package Management Basics](https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Understanding_client-side_tools/Package_management):** a nice, easy-to-follow introduction to package managers (specifically, npm)
