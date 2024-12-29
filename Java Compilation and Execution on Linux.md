
# Setting Up Visual Studio Code for Java Compilation and Execution on Linux

This guide provides a step-by-step process to configure Visual Studio Code (VS Code) to compile and run Java programs on Linux, including input and output redirection. It also explains how to customize key bindings for convenience.

---

## Prerequisites

Before you begin, ensure the following are installed and set up on your system:

1. **Visual Studio Code**:  
   Download and install VS Code from [here](https://code.visualstudio.com/Download).
   ``"Sytem installer is recomended."``

3. **JDK (Java Development Kit)**:  
   Install the JDK by running:
   ```bash
   sudo apt update && sudo apt install openjdk-11-jdk
   ```
   Basic Terminal Knowledge:  
   Familiarity with basic terminal commands is helpful.

# Step 1: Create the Configuration File (tasks.json)

### Open Your Project in VS Code:
- Launch VS Code.
- Open the folder where your Java files are located.

### Create the .vscode Directory:
If the .vscode directory does not exist in your project folder, create it using:
```bash
mkdir .vscode
```

### Create tasks.json:
Inside the .vscode directory, create the tasks.json file:
```bash
touch .vscode/tasks.json
```

### Add Configuration:
Open tasks.json in VS Code and copy the following configuration:
```json
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "Compile and Run Java",
      "type": "shell",
      "command": "bash",
      "args": [
        "-c",
        "javac ${relativeFile} && timeout 10 /usr/bin/time -v --output=${fileDirname}/sys.txt java -cp ${fileDirname} ${fileBasenameNoExtension} < ${fileDirname}/input.txt > ${fileDirname}/output.txt"
      ],
      "presentation": {
        "reveal": "never",        // Ensures the panel doesn't stay visible
        "panel": "new",          // Opens the panel only when needed
        "clear": true             // Clears the panel before each task run
      },
      "group": {
        "kind": "build",
        "isDefault": true
      },
      "problemMatcher": {
        "owner": "java",
        "fileLocation": [
          "relative",
          "${workspaceFolder}"
        ],
        "pattern": {
          "regexp": "^(.*):(\d+):(\d+):\s+(warning|error):\s+(.*)$",
          "file": 1,
          "line": 2,
          "column": 3,
          "severity": 4,
          "message": 5
        }
      }
    }
  ]
}
```

### Explanation of Presentation for Panel Hiding:
- `"reveal": "never"`: Ensures the terminal/panel doesn't remain visible after the task finishes running.
- `"panel": "new"`: Opens a new panel during execution if required.
- `"clear": true`: Clears any previous output in the terminal panel for a clean view.

### Replace the "presentation" section:To Show Panel
```json
"presentation": {
    "reveal": "always",
    "panel": "shared",
    "clear": false
}
```

### Save the File:
Press Ctrl+S to save the file.

# Step 2: Create Input and Output Files

### Navigate to Your Java File's Directory:
Open the terminal and move to the directory where your Java source code resides:
```bash
cd /path/to/your/project
```

### Create Input File:
Create an input.txt file to provide input for your program:
```bash
touch input.txt
```

### Create Output File (Optional):
While the task will auto-create output.txt if it doesn't exist, you can create it manually:
```bash
touch output.txt
```

### Edit input.txt:
Open input.txt in VS Code or any text editor and add the input values required by your program.

### Arrange input.txt and output.txt for Better Workflow:
- Place input.txt at the Top-Right Panel:
    1. Open input.txt and drag its tab to the top-right corner of the editor.
    2. VS Code will highlight the top-right panel for placement. Release the tab to dock it there.
- Place output.txt at the Bottom-Right Panel:
    1. Open output.txt and drag its tab to the bottom-right corner.
    2. VS Code will highlight the bottom-right panel for placement. Release the tab to dock it.

# Step 3: Run the Task in VS Code

### Open Your Java File:
In VS Code, open the Java file you want to compile and run.

### Run the Task:
Press Ctrl+Shift+B to execute the Compile and Run Java task.

### What the Task Does:
- **Compilation**: Compiles the currently open Java file using javac.
- **Input Redirection**: Feeds data from input.txt into the program.
- **Output Redirection**: Saves the program's output to output.txt.
- **Performance Metrics**: Logs system metrics (e.g., execution time, memory usage) to sys.txt.

### Monitor Output:
- **Program Output**: Check output.txt.
- **Performance Metrics**: Check sys.txt.

# Step 4: Customize Key Bindings (If `Ctrl+Shift+B`Not Working)

### Open Keyboard Shortcuts Editor:
Go to File > Preferences > Keyboard Shortcuts (or press Ctrl+K Ctrl+S).

### Search for ``"Run Build Task"``:
In the search bar, type "Run Build Task".

### Change Key Binding:
- Click the pencil icon next to the existing shortcut.
- Press your desired key combination (e.g., Ctrl+Alt+B).
- Press Enter to save the new binding.

# Step 5: Verifying Output

After running the task:
- **Program Output**: Open output.txt to view the program's results.
- **System Performance Metrics**: Open sys.txt to see execution time, memory usage, and other performance details.

### Debugging Errors:
- Check the Problems tab in VS Code.
- Check the Output tab in the terminal panel.

## Troubleshooting

### javac: Command Not Found:
- Install the JDK if not already installed:
```bash
sudo apt update && sudo apt install openjdk-11-jdk
```

### Missing Input/Output Files:
- Ensure input.txt is created and present in the same directory as your Java file. The task will create output.txt automatically if it doesn't exist.

### Timeout Issues:
The task uses a timeout command of 10 seconds. If your program needs more time, increase the timeout in tasks.json:
```json
timeout 20 /usr/bin/time -v ...
```

# Summary of Features

- **Automated Compilation and Execution**: Simplifies running Java programs directly from VS Code.
- **Input/Output Handling**: Redirects input from input.txt and saves output to output.txt.
- **Performance Metrics**: Logs detailed system performance data to sys.txt.
- **Customizable Key Bindings**: Allows you to assign a custom shortcut for running tasks.
- **Clean Presentation**: Configurable terminal behavior for tailored workflow.

By following these steps, you can seamlessly compile and run your Java programs in VS Code on Linux, with robust input/output handling and performance monitoring.
