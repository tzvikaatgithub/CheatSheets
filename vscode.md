# Installation

On Mac you can install with brew `brew install visual-studio-code`

# Settings

https://code.visualstudio.com/docs/getstarted/settings#:~:text=You%20can%20open%20the%20settings,Ctrl%2BShift%2BP).

Open settings.json:
  * FIle > Preferences > Settings
  * Ctrl , (or Cmd ,) and then click on the squiggly icon at top right

I bound <leader>k to workbench.action.openDefaultKeybindingsFile - which opens the full list of all known commands at that time

# Extensions

dotfiles has settings.json for Vim extension with custom key bindings.
use "command" for the `:<command>`

to look up the command to rebing:
  * Windows, Linux: File > Preferences > Keyboard Shortcuts > keybindings.json link
  * macOS: Code > Preferences > Keyboard Shortcuts > keybindings.json link

or if you know the keys, you can switch in the search to "record commans", then use the stroke then find the command executed by that stroke

## Python

### Debugging

To debug Python code you need to run debugger (can be configured).

Breakpoints: use F9 to insert breakpoints.

Execute Line by Line: Shift+Enter.

Python Interactive Window: Ctrl+Enter

# Custom Extensions

Custom vscode keybinding using a custom extension
If you want the custom <leader>f keybinding to trigger a search that only includes a specific folder and leave the standard Ctrl + F behavior unchanged, you can create a custom command that performs the search with the desired search.include pattern and bind the <leader>f key combination to that command.
Here's an example of how you could create a custom command in Visual Studio Code:
Open the Command Palette by pressing Ctrl + Shift + P (or Cmd + Shift + P on macOS)
Type Developer: Open Keyboard Shortcuts and select the option to open the keybindings.json file
Add the following code to the keybindings.json file to create a custom command:
```json
{
    "key": "<leader>f",
    "command": "extension.customFindInFolder",
    "when": "editorTextFocus && vim.active"
}
```

This creates a custom command named extension.customFindInFolder and binds it to the <leader>f key combination.
Next, you need to create an extension that implements the extension.customFindInFolder command:
Open the Command Palette by pressing Ctrl + Shift + P (or Cmd + Shift + P on macOS)
Type Developer: New Extension (TypeScript) and select the option to create a new extension
Replace the generated code with the following:
```typescript
import * as vscode from 'vscode';
export function activate(context: vscode.ExtensionContext) {
    context.subscriptions.push(
        vscode.commands.registerCommand('extension.customFindInFolder', () => {
            const searchPath = '/path/to/folder/**/*';
            vscode.commands.executeCommand('workbench.action.findInFiles', {
                query: '',
                pattern: searchPath
            });
        })
    );
}
export function deactivate() {}
```
This creates an extension that implements the extension.customFindInFolder command and performs a search that only includes files in the folder located at /path/to/folder.
Finally, you need to activate the extension by opening the Command Palette, typing Developer: Open Extensions and selecting the extension you just created.
Now, when you press the <leader>f key combination in Vim mode, the custom command will perform a search that only includes files in the folder located at /path/to/folder. The standard Ctrl + F behavior will remain unchanged.

Here are some resources you can refer to if you run into issues implementing the custom search in Visual Studio Code:
* Visual Studio Code's official documentation on the workbench.action.findInFiles command, which provides information on how to perform a search in Visual Studio Code: https://code.visualstudio.com/docs/editor/codebasics#_search-across-files
* Visual Studio Code's official documentation on how to create a custom command in Visual Studio Code: https://code.visualstudio.com/docs/extensions/example-hello-world#_create-a-command
* Visual Studio Code's official documentation on how to create a Visual Studio Code extension: https://code.visualstudio.com/docs/extensions/overview
* Visual Studio Code's official documentation on how to bind a custom command to a keybinding: https://code.visualstudio.com/docs/getstarted/keybindings#_custom-keybindings

These resources should provide enough information for you to configure the custom search in Visual Studio Code successfully. If you run into any specific issues, feel free to ask for more help.

# Workspaces

By default when you open a folder (or file?) in VSCode, it will be a single folder workspace.

You can open multi-folder workspace using a file, which defines the folders to open.

```json
{
  "folders": [
    {
      "path": "/path/to/my-folder-a"
    },
    {
      "path": "/path/to/my-folder-b"
    }
  ]
}
```

[Workspaces in Visual Studio Code](https://code.visualstudio.com/docs/editor/workspaces#_multiroot-workspaces)