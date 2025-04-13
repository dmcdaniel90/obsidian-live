
## Basics

>[!terminal] Opening a file in VS Code in the current window
>```bash
>code -r <path> 


### Keyboard Shortcuts


| Action    | Keyboard Shortcut    |
| --- | --- |
| Toggle Sidebar    | `Cmd + B  `  |
| Open Command Palette | `Cmd + Shift + P` |
| Open File Switcher | `Cmd + P` |
| Toggle Integrated Terminal | Ctrl + `  |
| Open Settings | `Cmd + ,` |
| Open Settings UI | `Opt + Cmd + ,` |

## Productivity Tricks

### Essential Navigation

| Action | Keyboard Shortcut |
| --- | --- |
| Jump to Previous File | `Cmd + P + P` |
| Focus Sidebar | `Cmd + 0` |
| Focus Editor | `Cmd + 1` |
| Open Explorer | `Cmd + Shift + E` |
| Open Debug | `Cmd + Shift + D` |
| Open Extensions | `Cmd + Shift + X` |

### HTML with Emmet

#### Emmet Basics

>[!url] See Emmet cheatsheet [HERE](https://docs.emmet.io/cheat-sheet/)

>[!tip] Use `tab` to cycle through highlighted parameters after generating an Emmet completion

>[!tip] With the addition of Github Copilot, remember to add `>` at the end to trigger Emmet completion instead of Copilot. Or you can hit `Ctrl + Space`.
>
>```html
><!-- Example -->
>link>
>```

>[!code] Inserting Emmet code between existing code
>```html
><div>(.col-6>#myElement.is-large)+(.col-6>#mySecondElement.is-small)</div>

#### Wrapping markup in a container

>[!tip] Use 'Balance Outward/Inward' + 'Wrap in Abbreviation' from the command palette to wrap code in a tag instead of copy and paste.
>- Balance has been custom mapped to `Cmd + K + (O / I)`
>- Wrap has been custom mapped to `Cmd + K + W`

### Styling with Emmet

> You can use Emmet for more than just HTML. It also includes abbreviations for style declarations. Here are some examples.

| Abbreviation    | Value     |
| --- | --- |
| `bgi`    | `background-image`     |
| `bgs` |` background-size` |
| `bgc` | `background-color` |
| `h100p` | `height: 100%` |
| `maw800` | `max-width: 800px` |
| `mh1400` | `max-height: 1400px` |

### Updating Image Sizes

> A common requirement is to provide an initial width/height for an image. We do this so that the browser knows how much space to reserve for the image. This keeps the page from jumping around before and after the image is downloaded from the server.

>[!tip] You can use Emmet to automatically update image sizes.
>
>- Put your cursor in the `img` tag in the "index.html" page
>- Open the Command Palette `Cmd/Ctrl + Shift + P`
>- Select "Emmet: Update Image Size"
>- 
>  This also works for images in CSS

## Navigation and Refactoring

### Moving, Duplicating, and Deleting

| Action     | Keyboard Shortcut     |
| --- | --- |
| Duplicate Line    | `Opt + Shift + Down/Up Arrow`     |
| Move Line | `Opt + Down/Up Arrow` |
| Delete Line | `Cmd + Shift + K` |

>[!tip] Note that you don't need to select a line in VS Code to copy/cut it. Just put your cursor anywhere on the line and press `Cmd/Ctrl + C` or `Cmd/Ctrl + X` and the entire line will be cut or copied. This is the default behaviour of the editor.

### Folding Sections

>[!tip] Use the "Fold" command in the command palette to fold HTML, methods, classes, and other structures. The command is `Opt + Cmd + [`

#### Folding by Region

> You can create arbitrary regions to be folded in VSCode. To create a region start a comment block with `//#region {optional name}` and end the block with `//#endregion`. (This is for JS in this case)

### Multiple Cursors

> While not a feature you will use often, there are certain cases.

| Action     | Keyboard Shortcut     |
| --- | --- |
| Select all instances    | `Cmd + Shift + L`     |
| Incrementally select instances | `Cmd + Shift + D` |
| Skip an Instance | `Cmd + K + D` |

### Rename refactor

> Renaming variables with multiple cursors is a bad idea as you may possibly miss an instance and it does not change instances in other files. Use the Rename capability instead by clicking on an instance and pressing `F2`

>[!tip] To see all instances in a project, place your cursor on an instance and press `Shift + F12`

### Finding Things

#### Find

> The Find feature can search strings to replace one or all instances (`Cmd + F`). It also supports regex.
> Ex. `png|jpeg` + 'Use regular expression' + `Opt + Enter` to add a cursor at each instance

#### Symbol Browser

>The other way to find things is with the Symbol Browser. There are two easy ways to access it besides the Command Palette.
> - via `Cmd + P` then entering `@`
> - keyboard shortcut `Shift + Cmd + O`

>[!tip] In code files, group by classes, functions, methods and variables by adding `:` after the `@`

>[!tip] Search an entire workspace by using `Cmd + T` or entering `#`

### Extract refactor

>This is very useful for when you want to extract code into it's own method.
>`Cmd + .` :FasArrowRight: `Extract...`


## Debugging

### Simple Debugging
> VS Code includes a debugger for Node.js out-of-the-box. You can run any JavaScript file with the debugger without any configuration whatsoever. 
> - Simply click on the left-hand margin of the line number
> - Press `F5` and select 'Node.js'

>[!tip] You can also use the Debug Console in the bottom panel and enter the name of the command or object you want to run/inspect.

#### Logpoints
>[!tip] You can also use breakpoints to simply log out values to the Debug Console instead of using `console.log` by right clicking in the left-margin and selecting `Add Logpoint`. This is good for when you do not want your entire application to pause execution.

### Simple Launch Config

> In most instances, you will need to specify a "Launch Configuration" for VS Code. These are commonly referred to as "Launch Configs". This is a file that specifies how VS Code should run your project.

>[!important] For debugging console applications, you must specify in your launch.json to use the correct `"program"` value and to use `"console": "integratedTerminal"`

>[!tip] In Typescript builds, you can use `Cmd + Shift + B` to instruct VSCode to "watch" or to "watch and build".

### Auto Attach

> While browser debugging is common, it is easier to debug your code in the same place that you write it. VSCode allows you to specify a type of launcher and a url to launch it against.
> ```json
> {
> "version": "0.2.0",
> "configurations": [
> 		{
> 			"type": "chrome",
> 			"request": "launch",
> 			"name": "Launch Project 3",
> 			"url": "http://localhost:3000",
> 			"webroot": "${workspaceFolder}"	
> 		}
> 	]
> }

### Compound Launch Configs

> Often you need to run multiple processes at once, but debug them as if they were the same project. A common scenario for this is running a React, Angular or Vue app, along with some sort of API service using Express or Hapi. VS Code has a feature called "Compound Launch Configurations" that allow you to launch multiple debug processes at one.

> For example in a React/Express app, you will need to create a Chrome process that runs from the root and another Node process that runs from `/server`. Then create a compound config that includes both of these configs. You can then add breakpoints to both your `App.js` and your `server/routes/index.js`.
>  ```json
> {
> "version": "0.2.0",
> "compounds": [
> 	{
> 		"name": "Launch Project 4",
> 		"configurations": ["Launch Program", "Launch Chrome"]
> 	}
> ],
> "configurations": [
> 		{
> 			"type": "chrome",
> 			"request": "launch",
> 			"name": "Launch Chrome",
> 			"url": "http://localhost:3000",
> 			"webroot": "${workspaceFolder}"	
> 		},
> 		{
> 			"type": "node",
> 			"request": "launch",
> 			"name": "Launch Program",
> 			"program": "${workspaceFolder}/server/server.js"
> 		}
> 	]
> }