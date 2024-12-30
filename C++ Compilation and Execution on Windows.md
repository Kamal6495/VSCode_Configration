
# C++ Compile and Run Task in VS Code

## Introduction
This guide explains how to set up and use a custom task in Visual Studio Code (VS Code) to compile and run a C++ program with input and output redirection. It is aimed at developers who want to streamline the process of compiling and running C++ programs with input from a file and output directed to another file.

## Prerequisites

1. **Visual Studio Code (VS Code)** installed on your machine.
2. **G++ (GNU Compiler Collection)** installed and properly set up. Make sure you can run `g++` and execute compiled C++ programs from the terminal.

## Steps to Set Up the Task

### Step 1: Create a `tasks.json` File

1. Open your C++ project folder in VS Code.
2. Press `Ctrl+Shift+P` (or `Cmd+Shift+P` on macOS) to open the Command Palette.
3. Type `Tasks: Configure Task` and select it from the dropdown.
4. Choose `Create tasks.json file from template`.
5. Select `Others` to create a custom task.
6. This will create a `.vscode` folder in your project (if it doesn’t already exist) and generate a `tasks.json` file.

### Step 2: Define the C++ Compile and Run Task

1. Open the `tasks.json` file within the `.vscode` folder.
2. Replace the contents with the following code:

```json
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "Compile and Run",
      "type": "shell",
      "command": "cmd",
      "args": [
        "/c",
        "g++ "${fileDirname}\${fileBasename}" -o "${fileDirname}\${fileBasenameNoExtension}" && "${fileDirname}\${fileBasenameNoExtension}" < "${fileDirname}\input.txt" > "${fileDirname}\output.txt""
      ],
      "presentation": {
        "reveal": "always",
        "panel": "shared"
      },
      "group": {
        "kind": "build",
        "isDefault": true
      },
      "problemMatcher": {
        "owner": "cpp",
        "fileLocation": [
          "relative",
          "${workspaceFolder}"
        ],
        "pattern": {
          "regexp": "^(.*):\d+:\d+:\s+(warning|error):\s+(.*)$",
          "file": 1,
          "severity": 2,
          "message": 3
        }
      }
    }
  ]
}
```

### Step 3: Explanation of the tasks.json Configuration

1. **Task Configuration (label, type, command)**:
   - `"label": "Compile and Run"`: The label that will be shown in the VS Code task list.
   - `"type": "shell"`: Specifies the type of task, which in this case is a shell task.
   - `"command": "cmd"`: The command to execute (the Windows command prompt).
   - `"args"`: A list of arguments passed to the command.
     - `"/c"`: Tells cmd to execute the following command and then terminate.
     - `"g++ "${fileDirname}\${fileBasename}" -o "${fileDirname}\${fileBasenameNoExtension}""`: Compiles the C++ file in the current directory.
     - `""${fileDirname}\${fileBasenameNoExtension}""`: Runs the compiled C++ program.
     - `"< "${fileDirname}\input.txt" > "${fileDirname}\output.txt""`: Redirects input from `input.txt` and output to `output.txt`.
   
2. **Presentation Settings**:
   - `"presentation": { "reveal": "always", "panel": "shared" }`: Controls how the task output is displayed in VS Code. It will always reveal the task's output in the terminal panel.
   
3. **Task Group**:
   - `"group": { "kind": "build", "isDefault": true }`: Makes this task part of the build group and sets it as the default task.
   
4. **Problem Matcher**:
   - `"problemMatcher": { ... }`: This section helps VS Code identify and show warnings or errors from the C++ compiler in the Problems panel.

### Step 4: Run the Task

1. Press `Ctrl+Shift+P` (or `Cmd+Shift+P` on macOS) to open the Command Palette.
2. Type `Run Task` and select it.
3. Choose `Compile and Run` from the list of tasks.
4. The task will compile and run the C++ program, using `input.txt` as the input and saving the output to `output.txt`.

### Step 5: Customize the Task (Optional)

You can customize the task by editing the arguments and settings within the `tasks.json` file. For example:
- Change `input.txt` and `output.txt` to other file names.
- Adjust the C++ compilation and execution commands based on your project setup.



## Controlling the Panel Behavior in VS Code

To modify the panel behavior in VS Code so that the task output is hidden or controlled differently, you can adjust the `presentation` section of your task configuration.

### 1. Hide the Panel Completely
If you want the panel to remain hidden and not be revealed at all, you can set the `reveal` property to `never`:

```json
"presentation": {
  "reveal": "never",
  "panel": "shared"
}
```
This means the terminal will not be automatically revealed when the task runs.

### 2. Reveal Panel Only on Errors
If you want the panel to be shown only when there are errors, you can set the `reveal` property to `silent`:

```json
"presentation": {
  "reveal": "silent",
  "panel": "shared"
}
```
With this setting, the panel will not pop up automatically, unless there is an error or warning during task execution.

### 3. Always Reveal the Panel (Default Behavior)
If you want the panel to always show up when the task runs (which is the default behavior), you can leave the configuration as it is:

```json
"presentation": {
  "reveal": "always",
  "panel": "shared"
}
```
This ensures that the terminal or output panel will always be shown when the task is executed.

### Summary of Presentation Options:
- `"reveal": "always"`: Always show the panel when the task runs.
- `"reveal": "silent"`: Only show the panel if there are issues or errors.
- `"reveal": "never"`: Never show the panel automatically.
- `"panel": "shared"`: Keeps the output in a shared terminal, which can be reused for other tasks. You can change this to `"panel": "new"` if you want each task to run in a new terminal instance.
