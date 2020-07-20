# BFZ Starter Project
Starter code for BFZ projects hosted on GitHub pages.


## 1. Get software

To use this starter project, first download required software:

- [**Visual Studio Code**](https://code.visualstudio.com/): free text editor for desktop
- [**Git**](https://git-scm.com/): version control software; comes with `Git Bash` command-line shell
- [**Node.js**](https://nodejs.org/en/): server-side programming language; comes with the **Node Package Manager** (`npm`)

Sign up for a [GitHub account](https://github.com/) and make sure you're part of the [Built for Zero](https://github.com/builtforzero) organization.

## 2. Set up the project in GitHub

Create a new repository using this project as a template:

- Click on the green **New** button in GitHub.
- Under **Repository Template**, choose this repo: `builtforzero/bfz-starter-project`. 
- Enter a custom repository name and description. 
- Create the repository.

Clone the new repository to your computer using the [instructions here](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/cloning-a-repository).

Finally, go back to the repository in GitHub and set up a GitHub Pages site.

- While viewing the repository in GitHub, click on the **Settings** tab.
- Scroll down to the **GitHub Pages** section.
- Under **Source**, select **master branch** from the dropdown menu.
- Save the URL that is generated by GitHub. This is where your project will be hosted.


## 3. Set up the development environment

Open your project folder in VSCode. Click on `Ctrl` + `Shift` + `` ` `` to open a new terminal. Navigate to the `bash` terminal (if you're not already there). Type these commands into the terminal, one at a time:

- `npm init -y`
- `npm install parcel-bundler nodemon concurrently --save-dev`
- `npm install express --save`
- `npm install gh-pages`
- `npm install dotenv`
- `npm install d3`

These commands will install several new folders and packages to your project.

Go to the `package.json` file. In the `scripts` section of the file, copy and paste the following scripts. Replace `ENTER_URL_HERE` with the complete GitHub Pages URL of your project (created in step 2).

    "build-watch": "parcel watch ./client/index.html",
    "start-watch": "nodemon server/index.js",
    "dev": "concurrently --kill-others \"npm run start-watch\" \"npm run build-watch\"",
    "build": "parcel build ./client/index.html",
    "start": "npm run build && node server/index.js",
    "predeploy": "rm -rf dist && parcel build ./client/index.html --public-url ENTER_URL_HERE",
    "deploy": "gh-pages -d dist",


#### **Install More Packages**

- **In the terminal:** type `npm install package-name`, replacing `package-name` with the package you wish to install
- **In `client/main.js`:** require the package at the top of the file, in the format `const d3 = require('d3')`

Some helpful packages:

- [**Papa Parse**](https://www.papaparse.com/): fast loading and parsing of CSV files. Use `npm install papaparse`.
- [**AWS SDK**](https://aws.amazon.com/sdk-for-node-js/): API that connects to Amazon Web Services. Use `npm install aws-sdk`.


#### **Add Secrets**
Add secret environment variables (e.g. API keys) to the `.env` file and use them in your JavaScript.

- **In the `.env` file:** add secrets using the format `API_KEY=123456789`, one line per secret.
- **In the `client/main.js` file:** access the environment variables using the format `const apiKey = process.env.API_KEY;`


## 4. Workflow

During development:

- In the terminal, type `npm run dev` to start the development server
- Go to http://localhost:3000
- Make changes to files in the `client` folder, and the page will automatically reload on save

To publish:
- In the terminal, type `npm run predeploy`, and then `npm run deploy`
- Commit all changes to GitHub using `git add .` , `git commit -m [message]`, and `git push origin master`
- Visit the GitHub Pages URL to view the published project
