# Plugins 

- https://github.com/JetBrains/intellij-platform-plugin-template

Create a new IntelliJ plugin project with the following dependencies:

com.intellij.modules.platform
org.jetbrains.annotations
com.intellij.openapi.application
com.intellij.openapi.editor
com.intellij.openapi.fileEditor
com.intellij.openapi.project
com.intellij.openapi.util
com.intellij.openapi.actionSystem
In the plugin.xml file of your project, define a new action that will generate the table of contents:

```xml
<actions>
    <group id="MarkdownToc" text="Markdown Table of Contents">
    <action id="GenerateMarkdownToc" class="com.example.GenerateMarkdownTocAction" text="Generate Table of Contents" />
    </group>
</actions>
```
Create a new Java class called GenerateMarkdownTocAction that extends com.intellij.openapi.actionSystem.AnAction and implements the actionPerformed method:

```java
public class GenerateMarkdownTocAction extends AnAction {
    @Override
    public void actionPerformed(AnActionEvent e) {
        // Get the current editor and file
        Editor editor = FileEditorManager.getInstance(e.getProject()).getSelectedTextEditor();
        VirtualFile file = FileDocumentManager.getInstance().getFile(editor.getDocument());

        // Generate the table of contents
        String toc = generateTableOfContents(file);

        // Insert the table of contents into the editor
        editor.getDocument().insertString(editor.getCaretModel().getOffset(), toc);
    }

    private String generateTableOfContents(VirtualFile file) {
        // Read the contents of the file
        String text = VfsUtil.loadText(file);

        // Parse the headers and generate the table of contents
        String[] lines = text.split("\n");
        StringBuilder toc = new StringBuilder();
        int level = 0;
        for (String line : lines) {
            if (line.startsWith("#")) {
                // Get the header level
                int headerLevel = line.indexOf(" ");
                if (headerLevel > level) {
                    // Start a new sublist
                    toc.append("\n");
                    toc.append("  ".repeat(headerLevel - level));
                    toc.append("- ");
                } else if (headerLevel == level) {
                    // Add a new item to the current list
                    toc.append("\n");
                    toc.append("  ".repeat(headerLevel));
                    toc.append("- ");
                } else {
                    // End the current sublist and start a new one
                    toc.append("\n");
                    toc.append("  ".repeat(level - headerLevel));
                    toc.append("}\n");
                    toc.append("  ".repeat(headerLevel - level));
                    toc.append("- ");
                }

                // Add the header text
                String headerText = line.substring(headerLevel + 1);
                toc.append("[");
                toc.append(headerText);
                toc.append("]");
                toc.append("(#");
                toc.append(headerText.toLowerCase().replaceAll(" ", "-"));
                toc.append(")");

                // Update the current header level
                level = headerLevel;
            }
        }

        // Return the table of contents
        return toc.toString();
    }
}
```
Build and install the plugin in IntelliJ IDEA.

Open a Markdown file in the editor and right-click to display the context menu. Click "Generate Table of Contents" to generate a table of contents based on the headers in the file.

Add the intellij plugin to your build.gradle file:

plugins {
id 'java'
id 'org.jetbrains.intellij' version '0.7.2'
}

Configure the intellij plugin to specify the IntelliJ version and the location of the plugin descriptor file:


intellij {
version '2021.3.1'
pluginName 'MyPlugin'
pluginDescription 'My awesome IntelliJ plugin'
pluginVersion '1.0.0'
pluginVendor 'My Company'
pluginUrl 'https://mycompany.com/myplugin'
ideaIC {
plugins = [
'com.intellij.modules.platform'
]
}
testIdea {
plugins = [
'com.intellij.modules.platform'
]
}
descriptor {
displayName 'My Plugin'
id 'com.mycompany.myplugin'
version pluginVersion
changeNotes """
Initial release
"""
}
}

Add your plugin's source code to the src/main directory.

Build the plugin using the buildPlugin task:


./gradlew buildPlugin

The resulting plugin ZIP file will be located in the build/distributions directory.

Install the plugin in IntelliJ IDEA by going to File -> Settings -> Plugins -> Install Plugin from Disk and selecting the plugin ZIP file.

the plugin.xml file is created in the src/main/resources/META-INF directory.