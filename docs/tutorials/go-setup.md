# Setting up a dev container for Go

* Primary author: [Taylor Morris](https://github.com/Taylor1515)

* Reviewer: [Jack Coury](https://github.com/jcoury89)

* This site has been heavily influenced by and uses information from the [Comp 423 Mkdocs Tutorial](https://comp423-25s.github.io/resources/MkDocs/tutorial/#what-you-will-learn)

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

```json
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



## Getting Started with Go

This section has been heavily influenced and using information from Go Documentations Getting [Started Tutorial](https://go.dev/doc/tutorial/getting-started)

### Step 1: Setup

1. Ensure you are inside of the GoTutorial directory and container.

2. Use go version to ensure go is installed in the container.

3. Create and enter a directory inside of GoTutorial called hello:

        mkdir hello
        cd hello

### Step 2: Write Some Code

1. Use mod to enable dependancy tracking for your code.
     
     When your code imports packages contained in other modules, you manage those dependencies through your code's own module. That module is defined by a go.mod file that tracks the modules that provide those packages. That go.mod file stays with your code, including in your source code repository.

     To enable dependency tracking for your code by creating a go.mod file, run the go mod init command, giving it the name of the module your code will be in. The name is the module's module path.

     For the purposes of this tutorial, just use example/hello. 

            go mod init example/hello
            go: creating new go.mod: module example/hello

2. Create a file called hello.go

3. Paste the following code into your hello.go file and save: 

        package main

        import "fmt"

        func main() {
            fmt.Println("Hello COMP423")
        }
    This is your Go code. In this code, you:

    * Declare a main package (a package is a way to group functions, and it's made up of all the files in the same directory).
    
    * Import the popular fmt package, which contains functions for formatting text, including printing to the console. This package is one of the standard library packages you got when you downloaded your GoTutorial container.
    
    * Implement a main function to print a message to the console. A main function executes by default when you run the main package.

### Step 3: Runing your code

There are two ways to run our hello.go file

#### Option 1: Use the run subcommand

1. Use the following comand to see the greeting

        go run .

    You should see "Hello COMP 423" printed on the consol.

!!!NOTE
    While the go run command is a useful shortcut for compiling and running a program when you're making frequent changes, it doesn't generate a binary executable.

#### Option 2. Use the build subcommand to complile and run the built binary directly.

1. From the command line in the hello directory, run the go build command to compile the code into an executable. 

        go build

2. From the command line in the hello directory, run the new hello executable to confirm that the code works. 

        ./hello

!!!NOTE
    Using the build subcommand in go is similar to using GCC in COMP 211 for C and C++. Build generates a binary executable file that we can then run directly in the terminal. 

## Pushing Changes to the Repository

### Step 1: Add and commit your changed

1. Add changes:

        git add .

2. Commit changes and leave a descriptive message:

        git commit -m "Completed container setup and Go tutorial"

### Step 2: Push Changes to GitHub

1. push changes:

        git push origin main

2. Login to GitHub and makesure the repository has updated with your go file.

## Congratulations

You have setup a development container for go and written your first program! Use what you learned here to keep GO-ing!