# VS Code Extension for SSG

This project creates and maintains a custom VS code extension.

## Creating a custom extension

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

## Why use a Node Version Manager

Using a Node.js version manager like **Volta** or **nvm (Node Version Manager)** is generally the better approach compared to installing Node.js directly. Here are the reasons why:

### 1. **Flexibility**:
   - **Version Control**: A version manager allows you to easily switch between different versions of Node.js, which is particularly useful if you work on multiple projects that require different versions.
   - **Testing**: If you need to test your code across different Node.js versions, a version manager makes this straightforward.

### 2. **Isolation**:
   - **Project-specific Versions**: You can set different Node.js versions per project, ensuring that each project uses the appropriate version without conflicts.
   - **Global vs. Local**: Version managers allow you to have both global and project-specific Node.js installations, which prevents potential conflicts between projects.

### 3. **Ease of Updates**:
   - **Simple Upgrades**: Upgrading Node.js is simpler with a version manager. You can install new versions and set them as the default with just a few commands, without having to manually uninstall and reinstall.

### 4. **Community Best Practice**:
   - **Widely Adopted**: Using a version manager is a common best practice in the Node.js community, especially among developers who work on various projects or contribute to open source.

### **Choosing Between Volta and nvm**

- **Volta**:
  - **Speed**: Volta is known for its speed, particularly in switching between versions and setting up environments.
  - **Ease of Use**: Volta automatically installs the correct Node.js version based on the project's configuration, making it more user-friendly.
  - **Cross-platform**: Works on macOS, Linux, and Windows.

- **nvm**:
  - **Popularity**: nvm has been around longer and has a larger user base, which can be advantageous when searching for community support.
  - **Simplicity**: nvm is straightforward and effective for managing multiple Node.js versions.

### **Recommendation**
- If you value speed and ease of use, **Volta** is a great choice.
- If you prefer a widely adopted tool with a large community, **nvm** might be the better option.

Both tools are effective, so the choice often comes down to personal preference and your specific workflow needs.

## Installing Node Version Manager

Yes, you can install `nvm-windows` using **Chocolatey** (choco), which is a popular package manager for Windows. This method is straightforward and automates the installation process. Here’s how you can do it:

### 1. **Ensure Chocolatey is Installed**
   - If you don’t have Chocolatey installed, you can follow the instructions on the [official Chocolatey website](https://chocolatey.org/install) to install it.

### 2. **Install nvm-windows Using Chocolatey**
   - Open a command prompt or PowerShell window with administrator privileges.
   - Run the following command to install `nvm-windows`:

     ```bash
     choco install nvm
     ```

   - Follow the on-screen prompts to complete the installation.

### 3. **Verify the Installation**
   - After installation, you can verify that `nvm-windows` is installed by running:

     ```bash
     nvm version
     ```

   - If the command returns the version number of `nvm`, the installation was successful.

### 4. **Using nvm-windows**
   - You can now use `nvm` to manage Node.js versions just as you would with the manual installation. Some basic commands include:

     - **Install a Node.js Version**:
       ```bash
       nvm install latest
       ```
     - **Switch to a Specific Node.js Version**:
       ```bash
       nvm use 14.17.0
       ```
     - **List Installed Node.js Versions**:
       ```bash
       nvm list
       ```

### 5. **Upgrade nvm-windows (Optional)**
   - If you need to upgrade `nvm-windows` later, you can do so with Chocolatey:

     ```bash
     choco upgrade nvm
     ```

Using Chocolatey simplifies the installation process and ensures that `nvm-windows` is installed correctly with minimal effort.

## Instaling latest LTS version of Node

To install the latest Long Term Support (LTS) version of Node.js using `nvm-windows`, you can follow these steps:

### 1. **Check Available Node.js Versions**
   - Open a command prompt or PowerShell window.
   - Run the following command to see all available Node.js versions, including the LTS versions:

     ```bash
     nvm list available
     ```

   - This command lists all the versions available for installation, including the latest LTS version.

### 2. **Install the Latest LTS Version**
   - To install the latest LTS version, you can use the following command:

     ```bash
     nvm install --lts
     ```

   - This will download and install the latest LTS version of Node.js.

### 3. **Set the LTS Version as the Default**
   - After installation, you can set the installed LTS version as the default version to be used:

     ```bash
     nvm use --lts
     nvm alias default lts
     ```

   - This ensures that the LTS version is used whenever you open a new terminal session.

### 4. **Verify the Installation**
   - To verify that the LTS version is installed and currently in use, run:

     ```bash
     node -v
     ```

   - This should display the version number of the installed LTS version.

By following these steps, you'll have the latest LTS version of Node.js installed and set as the default on your system using `nvm-windows`.
