---
layout: post
title: "python script to create shortcuts from all .exe in a folder"
categories: code
date: 2024-03-21
categories: [code, python]
---
<script>function copyCode(button) {
    var codeBlock = button.previousElementSibling;
    var code = codeBlock.innerText || codeBlock.textContent;
    
    // Create a temporary textarea element
    var tempTextarea = document.createElement('textarea');
    tempTextarea.value = code;
    
    // Append the textarea to the document
    document.body.appendChild(tempTextarea);
    
    // Select the text inside the textarea
    tempTextarea.select();
    tempTextarea.setSelectionRange(0, 99999); /* For mobile devices */
    
    // Copy the selected text
    document.execCommand('copy');
    
    // Remove the temporary textarea
    document.body.removeChild(tempTextarea);
    
    // Change the button text to indicate successful copying
    button.innerText = 'copied!';
    
    // Reset button text after 2 seconds
    setTimeout(function() {
        button.innerText = 'copy';
    }, 2000);
}
</script>

running this script will output shortcuts in their own folder. don't forget to edit the directories to suit your needs.

<div class="code-snippet">
    <pre><code>
    import os
import shutil
import winshell

# Directory to scan
scan_directory = "SOME DIRECTORY"
# Directory to create shortcuts
shortcut_directory = "SOME FOLDER"

# Function to scan the directory and create shortcuts
def create_shortcuts(directory):
    # Create shortcut directory if it doesn't exist
    if not os.path.exists(shortcut_directory):
        os.makedirs(shortcut_directory)

    # Iterate through each file in the directory
    for root, _, files in os.walk(directory):
        for file in files:
            # Check if the file is a .exe file
            if file.endswith(".exe"):
                # Exclude uninstallers and settings
                if "uninstall" not in file.lower() and "settings" not in file.lower() and "unin" not in file.lower():
                    # Create shortcut
                    game_exe_path = os.path.join(root, file)
                    shortcut_name = file.replace(".exe", ".lnk")
                    try:
                        winshell.CreateShortcut(
                            Path=os.path.join(shortcut_directory, shortcut_name),
                            Target=game_exe_path
                        )
                        print(f"Shortcut created for: {game_exe_path}")
                    except Exception as e:
                        print(f"Error creating shortcut for {game_exe_path}: {e}")

# Call the function to create shortcuts
print("Creating shortcuts...")
create_shortcuts(scan_directory)
print("Shortcut creation complete.")
    </code></pre>
    <button class="copy-button" onclick="copyCode(this)">Copy</button>
</div>
