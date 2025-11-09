# python-project
#python project repo.
import json
import os

TASKS_FILE = "tasks.json"

# -------------------------------
# Load tasks from file
# -------------------------------
def load_tasks():
    if os.path.exists(TASKS_FILE):
        with open(TASKS_FILE, "r") as file:
            return json.load(file)
    return []

# -------------------------------
# Save tasks to file
# -------------------------------
def save_tasks(tasks):
    with open(TASKS_FILE, "w") as file:
        json.dump(tasks, file, indent=4)

# -------------------------------
# Display all tasks
# -------------------------------
def view_tasks(tasks):
    if not tasks:
        print("\nNo tasks found!")
    else:
        print("\nYour To-Do List:")
        for i, task in enumerate(tasks, 1):
            status = "✅" if task["completed"] else "❌"
            print(f"{i}. {task['title']} [{status}]")

# -------------------------------
# Add a new task
# -------------------------------
def add_task(tasks):
    title = input("Enter task name: ").strip()
    if title:
        tasks.append({"title": title, "completed": False})
        save_tasks(tasks)
        print("Task added successfully!")
    else:
        print("Task name cannot be empty!")

# -------------------------------
# Mark task as complete
# -------------------------------
def complete_task(tasks):
    view_tasks(tasks)
    try:
        task_num = int(input("\nEnter task number to mark as complete: "))
        if 1 <= task_num <= len(tasks):
            tasks[task_num - 1]["completed"] = True
            save_tasks(tasks)
            print("Task marked as complete!")
        else:
            print("Invalid task number.")
    except ValueError:
        print("Please enter a valid number.")

# -------------------------------
# Delete a task
# -------------------------------
def delete_task(tasks):
    view_tasks(tasks)
    try:
        task_num = int(input("\nEnter task number to delete: "))
        if 1 <= task_num <= len(tasks):
            removed = tasks.pop(task_num - 1)
            save_tasks(tasks)
            print(f"Task '{removed['title']}' deleted!")
        else:
            print("Invalid task number.")
    except ValueError:
        print("Please enter a valid number.")

# -------------------------------
# Main menu
# -------------------------------
def main():
    tasks = load_tasks()

    while True:
        print("\n==== TO-DO MANAGER ====")
        print("1. View Tasks")
        print("2. Add Task")
        print("3. Mark Task Complete")
        print("4. Delete Task")
        print("5. Exit")

        choice = input("Enter your choice: ").strip()

        if choice == "1":
            view_tasks(tasks)
        elif choice == "2":
            add_task(tasks)
        elif choice == "3":
            complete_task(tasks)
        elif choice == "4":
            delete_task(tasks)
        elif choice == "5":
            print("Goodbye!")
            break
        else:
            print("Invalid choice! Try again.")

if __name__ == "_main_":
    main()
