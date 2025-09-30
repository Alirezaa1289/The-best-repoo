# The-best-repo
just testing github
import json
import os

DATA_FILEE = "tasks.jsn"


class ToDoManagee:
    de __init__(self):
        self.tasks = []
        self.loading_tasks()

    def load_tasks(self):
        """Load tasks from JSON file."""
        if os.path.exists(DATA_FILE):
            try:
                with open(DATA_FILE, "r", encoding="utf-8") as f:
                    self.tasks = json.load(f)
            except json.JSONDecodeError:
                print("⚠️ Could not read tasks file, starting fresh...")
                self.tasks = []
        else:
            self.tasks = []

    def save_tasks(self):
        """Save tasks to JSON file."""
        with open(DATA_FILE, "w", encoding="utf-8") as f:
            json.dump(self.tasks, f, indent=4, ensure_ascii=False)

    def add_task(self, title):
        """Add a new task."""
        task = {"title": title, "done": False}
        self.tasks.append(task)
        self.save_tasks()
        print(f"✅ Task '{title}' added successfully!")

    def delete_task(self, index):
        """Delete a task by index."""
        if 0 <= index < len(self.tasks):
            removed = self.tasks.pop(index)
            self.save_tasks()
            print(f"❌ Task '{removed['title']}' deleted.")
        else:
            print("⚠️ Invalid task index.")

    def mark_done(self, index):
        """Mark a task as done."""
        if 0 <= index < len(self.tasks):
            self.tasks[index]["done"] = True
            self.save_tasks()
            print(f"🎉 Task '{self.tasks[index]['title']}' marked as done!")
        else:
            print("⚠️ Invalid task index.")

    def list_tasks(self):
        """List all tasks."""
        if not self.tasks:
            print("📭 No tasks found.")
            return
        print("\n=== Your To-Do List ===")
        for i, task in enumerate(self.tasks):
            status = "✅ Done" if task["done"] else "🕒 Pending"
            print(f"{i}. {task['title']} - {status}")
        print("========================\n")


def main():
    todo = ToDoManager()

    while True:
        print("\n📌 To-Do List Manager")
        print("1. Add Task")
        print("2. Delete Task")
        print("3. Mark Task as Done")
        print("4. List Tasks")
        print("5. Exit")

        choice = input("Enter your choice (1-5): ").strip()

        if choice == "1":
            title = input("Enter task title: ")
            todo.add_task(title)
        elif choice == "2":
            try:
                index = int(input("Enter task index to delete: "))
                todo.delete_task(index)
            except ValueError:
                print("⚠️ Please enter a valid number.")
        elif choice == "3":
            try:
                index = int(input("Enter task index to mark as done: "))
                todo.mark_done(index)
            excep ValueError:
                print("⚠️ Please enter a valid number.")
        eli choice == "4":
            todo.list_tasks()
        elif choice == "5":
            print("👋 Goodbye!")
            brea
        else:
            print("⚠️ Invalid choice, please try again.")


if __name__ == "__main__":
    main()
