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

### A. Create a new repository using this project as a template.

- Click on the green **New** button in your GitHub account.
- Under **Repository Template**, choose this repo: `builtforzero/bfz-starter-project`. 
- Enter a custom repository name and description. 
- Create the repository.

### B. Clone the new repository to a folder on your desktop. 
- Use the [instructions here](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/cloning-a-repository).
- Cloning saves a copy of the repository to your computer.

### C. Set up a GitHub Pages site.

- Go to your repository in GitHub. Click on the **Settings** tab.
- Scroll down to the **GitHub Pages** section.
- Under **Source**, select **master** from the dropdown menu. (This will be changed later!)
- **Save the URL** that is generated by GitHub. This is where your project will be hosted.

<br />

## 3. Set up the development environment

### A. Set up your project

Open your project folder in VSCode. Open the terminal. Type these commands into the terminal, one at a time:

1. **`yarn init -y`**
2. **`yarn add parcel-bundler concurrently gh-pages --save-dev`**

**More Details: What are we doing here?**

1. **`yarn init -y`:** Initializes the Yarn package manager and adds several files to your project. The **`-y`** flag (y for "yes") skips Yarn's custom setup questions and generates a `package.json` based on default settings. This is normally fine! Leave out the **`-y`** flag if you would like to [customize settings](https://classic.yarnpkg.com/en/docs/cli/init/). This command generates a `package.json` file, `yarn.lock` file, and the `node_modules` folder.

    - **`package.json`** is your **project manifest**; aka a record of the dependencies and scripts needed to run your code.
    - **`yarn.lock`** and **`node_modules`** are files that store and manage your project's dependencies. *You don't need to touch these files!*
    - **`dist`** is a folder that is only created after the first time you deploy to GitHub pages (in step 5 below). It contains all of the files in your `client` folder, bundled for the web by the Parcel package. *You don't need to touch this file!*

2. **`yarn add parcel-bundler concurrently gh-pages --save-dev`**: Adds the following packages as a development dependency to your project:

    - **[Parcel](https://parceljs.org/):** bundles assets for the web (i.e., translates your modern JS code into a version that *all* browsers can read and understand).
    - **[Concurrently](https://www.npmjs.com/package/concurrently):** a helper package that allows you to run multiple terminal commands in one line.
    - **[gh-pages](https://www.npmjs.com/package/gh-pages):** a package that can publish your project to GitHub Pages.

### **B. Add Scripts**

Go to the newly-created `package.json` file. In the `scripts` section of the file, copy and paste the following scripts. Replace `ENTER_URL_HERE` with the complete GitHub Pages URL of your project (created in step 2). 

```json
   "scripts": {
      "dev": "parcel ./client/index.html --open",
      "predeploy": "rm -rf .tmp .cache dist && parcel build ./client/index.html --public-url ENTER_URL_HERE",
      "deploy": "gh-pages -d dist"
   },
```

You can run these scripts in the terminal using yarn in order to set up a development environment and publish to GitHub pages. See Step 5!
Note: On a Windows machine you may need to replace the "rm" command with "rd /s" in the "predeploy" section.

<br />

## 4. [OPTIONAL] Add more packages or secrets to your project

### **A. Add or remove packages from your project**

  - To **add a package:**
    - **Search for the package** on the web or in **[Yarn's website](https://yarnpkg.com/)**.
    - **In the terminal,** type **`yarn add [package]`**. E.g. **`yarn add d3`** will download the D3 package and add it to your project as a dependency. 
    - **In your main JavaScript file,** require the package at the **very top**. Use the format **`const [package] = require('package name')`**, e.g. **`const d3 = require('d3')`**. Then, you can use the package's methods anywhere in your JS. Check the package's **documentation** for specific installation instructions.

  - To **remove a package,** type **`yarn remove [package]`** in the terminal. E.g., **`yarn remove d3`.**

  - To **install all dependencies** for an existing project, simply type **`yarn`** in the terminal.
 
  - **Helpful packages to consider:**
    - **[Papa Parse](https://yarnpkg.com/package/papaparse)**: fast CSV parser
    - **[Lodash](https://lodash.com/)**: suite of array and object methods
    - Add more here as you find it!
 

### **B. Add Secrets**
Environment variables can hold secrets (e.g. API keys) that we need available in our JavaScript code, but inaccessible once published. Here's how to set it up:

- Get the **[Dotenv](https://www.npmjs.com/package/dotenv)** package by running **`yarn add dotenv`** in the terminal.
- Create a new file in the root directory called **.env**. Add secrets to the file using the format **`SECRET_NAME = 123456789`**, one line per secret.
- Add the line **`require('dotenv').config();`** to the very top of your `main.js` file.
- Access secrets within your JS in the following format: **`const secret = process.env.SECRET_NAME;`**

<br />

## 5. Use a workflow

### **A. During Development**

- In the terminal, run the command **`yarn dev`** to start the development server.
- Go to http://localhost:1234.
- Make changes to files in the **client** folder, and the page will automatically reload on save (aka "hot" reload).

### **B. To Publish**

- In the terminal, run the commands **`yarn predeploy`** and then **`yarn deploy`**
- Commit all changes to GitHub using the normal workflow: 
  - `git add .`
  - `git commit -m [message]`
  - `git push origin master`
- Visit the homepage of your project (your GitHub pages URL + index.html) to view the published project.

<br />

## Further Reading

**[Package Management Basics](https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Understanding_client-side_tools/Package_management):** a nice, easy-to-follow introduction to package managers (specifically, npm)
