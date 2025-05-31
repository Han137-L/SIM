# simple_task_list.py

class Task:
    def __init__(self, description, due_date=None, priority=None):
        self.description = description
        self.completed = False
        self.due_date = due_date
        self.priority = priority

    def mark_complete(self):
        self.completed = True

    def __str__(self):
        status = "✓" if self.completed else "✗"
        due_date_str = f" (Due: {self.due_date})" if self.due_date else ""
        priority_str = f" [Priority: {self.priority}]" if self.priority else ""
        return f"[{status}] {self.description}{due_date_str}{priority_str}"


class TaskList:
    def __init__(self):
        self.tasks = []

    def add_task(self, description, due_date=None, priority=None):
        new_task = Task(description, due_date, priority)
        self.tasks.append(new_task)

    def view_tasks(self):
        for index, task in enumerate(self.tasks):
            print(f"{index + 1}. {task}")

    def mark_task_complete(self, index):
        if 0 <= index < len(self.tasks):
            self.tasks[index].mark_complete()
        else:
            print("Invalid task number.")

    def delete_task(self, index):
        if 0 <= index < len(self.tasks):
            del self.tasks[index]
        else:
            print("Invalid task number.")


def main():
    task_list = TaskList()

    while True:
        print("\nSimple Task List")
        print("1. Add Task")
        print("2. View Tasks")
        print("3. Mark Task as Complete")
        print("4. Delete Task")
        print("5. Exit")

        choice = input("Choose an option: ")

        if choice == '1':
            task_description = input("Enter task description: ")
            due_date_input = input("Enter due date (YYYY-MM-DD) or leave blank: ")
            due_date = due_date_input if due_date_input else None
            
            # Validate date format if provided
            if due_date and not validate_date(due_date):
                print("Invalid date format. Please use YYYY-MM-DD.")
                continue
            
            priority = input("Enter priority (High, Medium, Low) or leave blank: ")
            priority = priority if priority in ['High', 'Medium', 'Low'] else None
            
            task_list.add_task(task_description, due_date, priority)
        elif choice == '2':
            task_list.view_tasks()
        elif choice == '3':
            task_number = int(input("Enter task number to mark as complete: ")) - 1
            task_list.mark_task_complete(task_number)
        elif choice == '4':
            task_number = int(input("Enter task number to delete: ")) - 1
            task_list.delete_task(task_number)
        elif choice == '5':
            print("Exiting the task list.")
            break
        else:
            print("Invalid choice. Please try again.")


def validate_date(date_text):
    try:
        datetime.strptime(date_text, '%Y-%m-%d')
        return True
    except ValueError:
        return False


if __name__ == "__main__":
    main()
# This code implements a simple task list application that allows users to add, view, mark as complete, and delete tasks.
git clone <https://github.com/Han137-L/SIM.git>
