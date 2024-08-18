# VS Code Extension for SSG

This project creates and maintains a custom VS code extension.

The most appropriate approach for developing a tool that inserts scaffold markdown code into the VSCode editor window when specific keybindings are pressed would be to create a **custom VSCode extension**. This method provides you with the flexibility to define exactly what the keybindings do, including inserting specific text or markdown code into the editor.

### Steps to Create a Custom VSCode Extension

1. **Set Up Your Development Environment**:
   - Ensure you have Node.js installed.
   - Install the VSCode Extension Generator:
     ```bash
     npm install -g yo generator-code
     ```

2. **Generate the Extension**:
   - Open a terminal and run:
     ```bash
     yo code
     ```
   - Follow the prompts to set up your extension. Choose options such as "New Extension (TypeScript)" for more structured code.

3. **Implement the Command**:
   - Open the generated project in VSCode.
   - In the `src/extension.ts` file, you'll define your command. Here's a basic example to insert markdown scaffold code:

     ```typescript
     import * as vscode from 'vscode';

     export function activate(context: vscode.ExtensionContext) {
         let disposable = vscode.commands.registerCommand('extension.insertMarkdownScaffold', () => {
             const editor = vscode.window.activeTextEditor;
             if (editor) {
                 const scaffold = `
                 # Title
                 
                 ## Introduction
                 
                 - Point 1
                 - Point 2
                 
                 ## Details
                 
                 1. Step 1
                 2. Step 2
                 
                 ## Conclusion
                 `;
                 editor.edit(editBuilder => {
                     editBuilder.insert(editor.selection.active, scaffold);
                 });
             }
         });

         context.subscriptions.push(disposable);
     }

     export function deactivate() {}
     ```

   - This code registers a command that inserts a markdown scaffold into the currently active editor.

4. **Bind the Command to a Keybinding**:
   - Modify `package.json` to bind the command to a key combination:

     ```json
     "contributes": {
         "commands": [
             {
                 "command": "extension.insertMarkdownScaffold",
                 "title": "Insert Markdown Scaffold"
             }
         ],
         "keybindings": [
             {
                 "key": "ctrl+alt+m",
                 "command": "extension.insertMarkdownScaffold",
                 "when": "editorTextFocus"
             }
         ]
     }
     ```

   - In this example, `Ctrl+Alt+M` triggers the insertion of the markdown scaffold.

5. **Test the Extension**:
   - Press `F5` in VSCode to open a new VSCode window with your extension loaded.
   - Open a markdown file and test the keybinding (`Ctrl+Alt+M`) to ensure it inserts the scaffold code.

6. **Publish the Extension** (Optional):
   - If you wish to share your tool, you can publish it to the VSCode Marketplace following [Microsoft's publishing guide](https://code.visualstudio.com/api/working-with-extensions/publishing-extension).

### Why This Approach?

- **Customizability**: Creating an extension gives you full control over the functionality, allowing you to easily update or expand the tool in the future.
- **Keybinding Integration**: You can directly integrate with VSCode's keybinding system, ensuring that your tool fits seamlessly into your workflow.
- **Scalability**: If you want to add more features later (e.g., different scaffolds for different file types), the extension framework supports this easily.

This approach is ideal for integrating your tool smoothly into your VSCode environment while maintaining flexibility and control.
