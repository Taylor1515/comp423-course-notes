# Setting up a dev container for Go

* Primary author: [Taylor Morris](https://github.com/Taylor1515)

* Reviewer: [Jack Coury](https://github.com/jcoury89)

* Site adapted from [Comp 423 Mkdocs Tutorial](https://comp423-25s.github.io/resources/MkDocs/tutorial/#what-you-will-learn)

## Prerequisites

Before we dive in, make sure you have:

1. A GitHub account: If you don’t have one yet, sign up at GitHub.
2. Git installed: Install Git if you don’t already have it.
3. Visual Studio Code (VS Code): Downloaded and installed.
4. Docker installed: Required to run the dev container.

## Creating the Repository

### Step 1: Create a Local Directory and Initialize Git

1. Open your terminal or command prompt.

2. Create a new directory for your project. (Note: Of course, if you'd like to organize this tutorial somewhere else on your machine, go ahead and change into that parent directory first. By default this will be in your user's home directory.):

        mkdir GoTutorial  
        cd GoTutorial  

3. Initialize a new Git repository:
 
        git init 

4. Create a README file:

        echo "# Go Tutorial" > README.md  
        git add README.md  
        git commit -m "Initial commit with README"

### Step 2: Create a Remote Repository on GitHub

1. Log in to your GitHub account and navigate to the Create a New Repository page.

2. Fill in the details as follows:

        Repository Name: GoTutorial  
        Description: "The results of completing a go tutorial."  
        Visibility: Public  

3. Do not initialize the repository with a README, .gitignore, or license.

4. Click Create Repository.

### Step 3: Link your Local Repository to GitHub

1. Add the GitHub repository as a remote:

        git remote add origin https://github.com/<your-username>/GoTutorial.git
        # Replace <your-username> with your GitHub username.

2. Check your default branch name with the subcommand git branch. If it's not main, rename it to main with the following command: git branch -M main. Old versions of git choose the name master for the primary branch, but these days main is the standard primary branch name.

3. Push your local commits to the GitHub repository:
 
        git push --set-upstream origin main 

4. Back in your web browser, refresh your GitHub repository to see that the same commit you made locally has now been pushed to remote. You can use git log locally to see the commit ID and message which should match the ID of the most recent commit on GitHub. This is the result of pushing your changes to your remote repository.

## Setting Up the Development Environment

### Step 1: Add Development Container Configuration

1. In VS Code, open the GoTutorial directory. You can do this via: File > Open Folder.

2. Install the Dev Containers extension for VS Code.

3. Create a .devcontainer directory in the root of your project with the following file inside of this "hidden" configuration directory:  
        
        .devcontainer/devcontainer.json

The devcontainer.json file defines the configuration for your development environment. Here, we're specifying the following:

* name: A descriptive name for your dev container.

* image: The Docker image to use, in this case, the latest version of a Go environment.

* customizations: Adds useful configurations to VS Code, like installing the Go extension.

* postCreateCommand: A command to run after the container is created. Here we are checking the current version of go that is installed. 

```
 {
	"name": "Go",
	"image": "mcr.microsoft.com/vscode/devcontainers/go:latest",
	"customizations": {
		"vscode": {
			"settings": { 
				"go.toolsManagement.checkForUpdates": "local",
				"go.useLanguageServer": true,
				"go.gopath": "/go"
			},
			"extensions": [
				"golang.Go"
			]
		}
	},
	"postCreateCommand": "go version",

	"remoteUser": "vscode"
}
```

### Step 2: Reopen the Project in a VSCode Dev Container

1. Reopen the project in the container by pressing Ctrl+Shift+P (or Cmd+Shift+P on Mac), typing "Dev Containers: Reopen in Container," and selecting the option. This may take a few minutes while the image is downloaded and the requirements are installed.

2. Once your dev container setup completes, close the current terminal tab (trash can), open a new terminal pane within VSCode, and try running go version to see your dev container is running a recent version of Go without much effort!

//Steps to create a new project, write a basic "Hello COMP423" program, compile, and run

## Getting Started with Go

Adapted from 

### Step 1: 