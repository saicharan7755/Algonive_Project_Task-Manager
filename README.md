# 📝 Task Manager

This is a simple and efficient **Task Manager** designed for daily use, developed as part of an internship project for **Algonive**.

---

## 📋 Project Overview

The Task Manager streamlines your daily workflow by allowing you to organize, prioritize, and track tasks with ease. Whether you're managing personal to-dos or professional tasks, this tool helps you stay productive and focused.

---

## ✨ Key Features

- **Add Tasks:** Create new tasks with detailed descriptions and set deadlines.
- **Categorize Tasks:** Classify tasks by priority level and type.
- **Mark as Completed:** Easily mark tasks as finished.
- **Remove Tasks:** Delete completed tasks to keep your list organized.
- **Simple CLI Interface:** Intuitive and lightweight command-line usage.

---

## 🛠️ Technologies Used

- **Programming Languages:** C / C++

  🔧 1. Data Structures
✅ Task Definition
Each task is represented by a struct that stores task-specific details:

cpp

Copy

Edit

    struct Task {
    string title;
    string description;
    string deadline;   // Format: DD-MM-YYYY
    string priority;   // High / Medium / Low
    bool completed = false;
    };
				
🗂️ Task Storage
Tasks are stored in a map, where each key is a category (like "Work", "Personal") and the value is a vector of tasks in that category:

cpp

Copy

Edit

     map<string, vector<Task>> taskManager;
					
➕ 2. Adding a Task

Users are prompted to enter task details like title, description, deadline, and priority. The task is then added to the correct category:

cpp

Copy

Edit

    void addTask() {
    Task newTask;
    string category;

    cout << "\nEnter Task Title: ";
    cin.ignore();
    getline(cin, newTask.title);

    cout << "Enter Task Description: ";
    getline(cin, newTask.description);

    cout << "Enter Task Category: ";
    getline(cin, category);

    cout << "Enter Deadline (DD-MM-YYYY): ";
    getline(cin, newTask.deadline);

    cout << "Enter Priority (High/Medium/Low): ";
    getline(cin, newTask.priority);

    newTask.completed = false;
    taskManager[category].push_back(newTask);

    cout << "✅ Task added successfully.\n";
    }
				
📋 3. Viewing Tasks

Displays all tasks grouped by category in a neat tabular format with status and description:

cpp

Copy

Edit

    void displayTasks() {
    if (taskManager.empty()) {
        cout << "\n⚠️ No tasks available.\n";
        return;
    }

    cout << "\n📋 Task List:\n";
    for (const auto& categoryPair : taskManager) {
        cout << "\n📁 Category: " << categoryPair.first << "\n";
        cout << setw(5) << "No." << setw(25) << "Title" << setw(15) << "Deadline" 
             << setw(10) << "Priority" << setw(12) << "Status" << "\n";
        cout << "-----------------------------------------------------------------------\n";

        for (size_t i = 0; i < categoryPair.second.size(); ++i) {
            const Task& task = categoryPair.second[i];
            cout << setw(5) << (i + 1)
                 << setw(25) << task.title
                 << setw(15) << task.deadline
                 << setw(10) << task.priority
                 << setw(12) << (task.completed ? "✅ Done" : "❌ Pending") << "\n";
            cout << "    📄 Description: " << task.description << "\n";
        }
    }
    }
				
✏️ 4. Editing a Task

Allows the user to update task fields. Empty inputs keep the current value unchanged:

cpp

Copy

Edit

    void editTask() {
    string category;
    int index;

    cout << "\nEnter Category of Task to Edit: ";
    cin.ignore();
    getline(cin, category);

    if (taskManager.find(category) == taskManager.end()) {
        cout << "⚠️ No tasks found in this category.\n";
        return;
    }

    displayTasks();
    cout << "\nEnter Task Number to Edit: ";
    cin >> index;

    if (index < 1 || index > taskManager[category].size()) {
        cout << "❌ Invalid task number.\n";
        return;
    }

    Task& task = taskManager[category][index - 1];
    cin.ignore();

    string input;
    cout << "Enter New Title (leave blank to keep current): ";
    getline(cin, input);
    if (!input.empty()) task.title = input;

    cout << "Enter New Description (leave blank to keep current): ";
    getline(cin, input);
    if (!input.empty()) task.description = input;

    cout << "Enter New Deadline (leave blank to keep current): ";
    getline(cin, input);
    if (!input.empty()) task.deadline = input;

    cout << "Enter New Priority (leave blank to keep current): ";
    getline(cin, input);
    if (!input.empty()) task.priority = input;

    cout << "✅ Task updated successfully.\n";
    }
				
❌ 5. Deleting a Task

Removes a task from the given category by index:

cpp

Copy

Edit

    void deleteTask() {
    string category;
    int index;

    cout << "\nEnter Category of Task to Delete: ";
    cin.ignore();
    getline(cin, category);

    if (taskManager.find(category) == taskManager.end()) {
        cout << "⚠️ No tasks found in this category.\n";
        return;
    }

    displayTasks();
    cout << "\nEnter Task Number to Delete: ";
    cin >> index;

    if (index < 1 || index > taskManager[category].size()) {
        cout << "❌ Invalid task number.\n";
        return;
    }

    taskManager[category].erase(taskManager[category].begin() + index - 1);
    cout << "✅ Task deleted successfully.\n";

    if (taskManager[category].empty()) {
        taskManager.erase(category);
    }
    }
				
✅ 6. Marking a Task as Completed

Marks a task as completed by setting its completed flag:

cpp

Copy

Edit

    void markTaskCompleted() {
    string category;
    int index;

    cout << "\nEnter Category of Task to Mark Completed: ";
    cin.ignore();
    getline(cin, category);

    if (taskManager.find(category) == taskManager.end()) {
        cout << "⚠️ No tasks found in this category.\n";
        return;
    }

    displayTasks();
    cout << "\nEnter Task Number to Mark as Completed: ";
    cin >> index;

    if (index < 1 || index > taskManager[category].size()) {
        cout << "❌ Invalid task number.\n";
        return;
    }

    taskManager[category][index - 1].completed = true;
    cout << "✅ Task marked as completed.\n";
    }
				
🧹 7. Removing All Completed Tasks

Deletes all completed tasks from all categories. Also removes empty categories:

cpp

Copy

Edit

    void removeCompletedTasks() {
    for (auto it = taskManager.begin(); it != taskManager.end(); ) {
        vector<Task>& tasks = it->second;
        tasks.erase(remove_if(tasks.begin(), tasks.end(),
                              [](const Task& t) { return t.completed; }), tasks.end());

        if (tasks.empty()) {
            it = taskManager.erase(it);
        } else {
            ++it;
        }
    }

    cout << "🧹 All completed tasks removed.\n";
    }
				
🧭 8. Main Menu

The entire program runs in a loop until the user exits:

cpp

Copy

Edit

    void menu() {
    int choice;
    do {
        cout << "\n====== Task Management Menu ======\n";
        cout << "1. Add Task\n";
        cout << "2. View All Tasks\n";
        cout << "3. Edit Task\n";
        cout << "4. Delete Task\n";
        cout << "5. Mark Task as Completed\n";
        cout << "6. Remove All Completed Tasks\n";
        cout << "0. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1: addTask(); break;
            case 2: displayTasks(); break;
            case 3: editTask(); break;
            case 4: deleteTask(); break;
            case 5: markTaskCompleted(); break;
            case 6: removeCompletedTasks(); break;
            case 0: cout << "👋 Exiting...\n"; break;
            default: cout << "❌ Invalid choice. Try again.\n";
        }
    } while (choice != 0);
    }
				
And it's all started with:

cpp

Copy

Edit

    int main() {
    cout << "=== Welcome to Task Manager ===\n";
    menu();
    return 0;
    }

## 🙏 Acknowledgments

- Developed as part of an internship project for **Algonive**
- Inspired by classic data compression algorithms and educational resources
