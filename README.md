import os
import shutil

# Folder to organize
folder = "TestFiles"

# File categories
categories = {
    "Images": [".jpg", ".jpeg", ".png", ".gif"],
    "Documents": [".pdf", ".docx", ".doc", ".txt"],
    "Videos": [".mp4", ".mkv", ".avi"],
    "Music": [".mp3", ".wav"],
    "Python": [".py"],
    "Others": []
}

# Create category folders
for category in categories:
    os.makedirs(os.path.join(folder, category), exist_ok=True)

# Organize files
for file in os.listdir(folder):
    file_path = os.path.join(folder, file)

    if os.path.isfile(file_path):
        extension = os.path.splitext(file)[1].lower()
        moved = False

        for category, extensions in categories.items():
            if extension in extensions:
                shutil.move(file_path, os.path.join(folder, category, file))
                moved = True
                break

        if not moved:
            shutil.move(file_path, os.path.join(folder, "Others", file))

print("Files organized successfully!")