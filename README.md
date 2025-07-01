# 📝 Task Manager Application

A modern, efficient **Task Manager** developed in C++ for daily productivity, as part of the Algonive internship program. This project demonstrates practical C++ development with a focus on user experience and code clarity.

---

## 📖 Table of Contents

- [Project Overview](#project-overview)
- [Features](#features)
- [Technology Stack](#technology-stack)
- [Code Structure & Implementation](#code-structure--implementation)
- [Installation & Compilation](#installation--compilation)
- [Usage Guide](#usage-guide)
- [Troubleshooting](#troubleshooting)
- [Acknowledgements](#acknowledgements)
- [Contact](#contact)

---

## 📋 Project Overview

The Task Manager is a command-line utility tailored to help users organize, prioritize, and monitor their daily tasks efficiently. With support for categorization, prioritization, editing, and completion tracking, it offers a comprehensive toolkit for both personal and professional workflow management.

---

## ✨ Features

- **Add Tasks:** Capture new tasks with descriptions, deadlines, priorities, and categories.
- **Categorize:** Group tasks by custom categories (e.g., Work, Personal).
- **Status Tracking:** Mark tasks as complete/incomplete with a single command.
- **Edit & Update:** Modify any task detail interactively.
- **Remove Tasks:** Delete individual or all completed tasks to maintain focus.
- **CLI Interface:** Lightweight, responsive command-line menu system.

---

## 🛠️ Technology Stack

- **Language:** C++ (C++11 standard)
- **Libraries:** STL (`<iostream>`, `<iomanip>`, `<string>`, `<vector>`, `<map>`, `<algorithm>`)
- **Platform:** Cross-platform (Windows, Linux, macOS)
- **Tools:** g++, MinGW, Visual Studio, or any C++11-compliant compiler

---

## 🗂️ Code Structure & Implementation

### 1. Data Model

```cpp
// Represents a single task with all relevant fields.
struct Task {
    std::string title;         // Task name (short and descriptive)
    std::string description;   // Detailed information about the task
    std::string deadline;      // Deadline in DD-MM-YYYY format
    std::string priority;      // Priority can be High, Medium, or Low
    bool completed = false;    // Completion status (false by default)
};
```

### 2. Storage

```cpp
// Stores tasks grouped by category for easy retrieval and management.
std::map<std::string, std::vector<Task>> taskManager;
```

### 3. Core Functions

#### Add a Task

```cpp
// Prompts the user for task details and adds to the appropriate category.
void addTask();
```

#### Display All Tasks

```cpp
// Prints all tasks grouped by category, with status and details.
void displayTasks();
```

#### Edit a Task

```cpp
// Allows users to update any field of a selected task.
void editTask();
```

#### Delete a Task

```cpp
// Removes a specific task from a chosen category.
void deleteTask();
```

#### Mark as Completed

```cpp
// Sets the completion status of a task to true.
void markTaskCompleted();
```

#### Remove All Completed Tasks

```cpp
// Cleans up all tasks marked as completed across all categories.
void removeCompletedTasks();
```

#### Main Menu

```cpp
// The main loop to present options and handle user actions.
void menu();
```

#### Entry Point

```cpp
// Program starts here.
int main() {
    std::cout << "=== Welcome to Task Manager ===\n";
    menu();
    return 0;
}
```

---

## 🚀 Installation & Compilation

### 1. Clone the Repository

```sh
git clone https://github.com/saicharan7755/Algonive_Project_Task-Manager.git
cd Algonive_Project_Task-Manager
```

### 2. Extract Source Files

If provided as a ZIP (`task_manager.zip`):

```sh
unzip task_manager.zip
```
> Ensure `main.cpp` and related files are present in the directory.

### 3. Install a C++ Compiler

- **Windows:** [MinGW](http://www.mingw.org/) or Visual Studio
- **Linux:** Install with `sudo apt install g++`
- **macOS:** Install with `xcode-select --install`

### 4. Compile the Program

```sh
g++ -std=c++11 -o task_manager main.cpp
```
> Replace `main.cpp` with your actual file name if different.

### 5. Run the Application

```sh
./task_manager      # On Linux/macOS
task_manager.exe    # On Windows
```

---

## 🧭 Usage Guide

- Start the program to access the interactive menu.
- Choose options by entering corresponding numbers.
- Enter task details as prompted; leave blank to retain existing values during edits.
- Mark, edit, or delete tasks as your workflow requires.
- Exit by selecting option `0`.

---

## 🩺 Troubleshooting

- **Compiler not found:** Ensure your C++ compiler is installed and configured in your system PATH.
- **File not found:** Verify that `main.cpp` is in your current directory.
- **Permission denied:** (Linux/macOS) Use `chmod +x task_manager` to make the binary executable.
- **Input errors:** Always provide valid input as prompted; invalid entries will be handled gracefully.

---

## 🙏 Acknowledgements

- Developed as part of the Algonive internship program.
- Inspired by classic CLI task managers and educational C++ resources.

---

## 📬 Contact

For questions, suggestions, or collaboration inquiries:

- **Email:** nistalacharan@gmail.com
- **LinkedIn:** [Sai Charan N](https://www.linkedin.com/in/sai-charan-n-0b6515348?utm_source=share&utm_campaign=share_via&utm_content=profile&utm_medium=android_app)

---

> *Thank you for exploring and using this Task Manager! Contributions and feedback are welcome.*
