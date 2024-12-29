# Customizing `tasks.json` and `keybindings.json` in Visual Studio Code (VS Code)

The custom `tasks.json` and `keybindings.json` configuration in Visual Studio Code (VS Code) allows to automate the process of running a program with a specific key combination, enhancing the development process.

## Overview:

### `tasks.json` Configuration:

- **Purpose:** This file defines custom tasks that can be executed in VS Code. In this case, it is configured to run a specific program (e.g., a compiled executable).
  
- **Components:**
  - **`label`:** A name for the task, such as "Run Program," which identifies the task.
  - **`command`:** The actual command to run the program, for example, the path to an executable file (`./program_name`).
  - **`group`:** Specifies the type of task (e.g., build), organizing it under predefined categories like build or test tasks.
  - **`problemMatcher`:** Used for error detection, which is left empty here since it’s not required for simply running the program.

- **Functionality:** When executed, the task runs the specified program, allowing you to streamline the process without manually entering commands in the terminal.

### `keybindings.json` Configuration:

- **Purpose:** This file binds specific key combinations to VS Code commands, enabling you to trigger tasks using a keyboard shortcut.

- **Components:**
  - **`key`:** Defines the shortcut to trigger the task, e.g., `ctrl+shift+r`.
  - **`command`:** The command to run the task, specifically `workbench.action.tasks.build` to run a task.
  - **`args`:** The task label (from `tasks.json`), which identifies the task to be executed, such as "Run Program."

- **Functionality:** Pressing the specified key combination will automatically execute the task you’ve defined, providing a faster and more efficient way to run your program without navigating through menus.

## How It Improves Workflow:

- **Efficiency:** It allows you to run your program with a single keystroke, saving time and reducing the need for manual terminal commands.
- **Customization:** You can easily modify the task to suit different programs or commands, and bind multiple shortcuts for different tasks.
- **Automation:** The integration between tasks and keybindings lets you automate common development steps (like compiling and running code) directly from the VS Code environment.

## Summary:

This setup enables, to run programs or scripts directly from VS Code using a custom keyboard shortcut, streamlining the development and testing process.





# For Multiple Tasks Like Java, C++, so on use this method Provided Below
## Visual Studio Code Task Setup

This contains an example of how to define multiple tasks in the `tasks.json` file for Visual Studio Code. The `tasks` are defined as an `array`  of objects separated by `comma (,)`, each representing a specific command or script to be run within VS Code.

## Structure and Syntax:
   - The `tasks` array holds multiple tasks.
   - Each task contains properties like `label`, `type`, `command`, `args`, `group`, `problemMatcher`, and `detail` to control what the task does.
   

## Example `tasks.json`

```json
{
    "version": "0.0.0",
    "tasks": [
        {
            "label": "Java",
         //some commands
        },
        {
            "label": "C++",
            //some commands
        },
        {
            "label": "python",
        //some commands
        }
    ]
}


