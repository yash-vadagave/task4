#include <iostream>
using namespace std;
#include <vector>
#include <string>

struct Task 
{
    string description;
    bool completed;
};

class ToDoList 
{
private:
    vector<Task> tasks;

public:
    void addTask(const string& description) 
    {
        Task newTask = {description, false};
        tasks.push_back(newTask);
        cout << "Task added: " << description <<endl;
    }

    void viewTasks() 
    {
        for (size_t i = 0; i < tasks.size(); ++i) 
        {
            cout << i + 1 << ". " << tasks[i].description;
            if (tasks[i].completed) 
            {
                cout << " [Completed]";
            }
            cout <<endl;
        }
    }

    void markTaskCompleted(size_t taskIndex) 
    {
        if (taskIndex >= 0 && taskIndex < tasks.size()) 
        {
            tasks[taskIndex].completed = true;
            cout << "Task marked as completed: " << tasks[taskIndex].description << endl;
        } 
        else 
        {
            cout << "Invalid task index." << endl;
        }
    }

    void removeTask(size_t taskIndex) 
    {
        if (taskIndex >= 0 && taskIndex < tasks.size()) 
        {
            tasks.erase(tasks.begin() + taskIndex);
            cout << "Task removed." << endl;
        } 
        else 
        {
            cout << "Invalid task index." <<endl;
        }
    }
};

int main() 
{
    ToDoList toDoList;

    while (true) 
    {
        cout << "Options:\n";
        cout << "1. Add Task\n";
        cout << "2. View Tasks\n";
        cout << "3. Mark Task as Completed\n";
        cout << "4. Remove Task\n";
        cout << "5. Exit\n";
        cout << "Enter option: ";
        
        int option;
        cin >> option;

        switch (option) 
        {
            case 1: 
            {
                string description;
                cout << "Enter task description: ";
                cin.ignore(); 
                getline(cin, description);
                toDoList.addTask(description);
                break;
            }
            case 2: 
            {
                toDoList.viewTasks();
                break;
            }
            case 3: 
            {
                size_t taskIndex;
                cout << "Enter task index: ";
                cin >> taskIndex;
                toDoList.markTaskCompleted(taskIndex - 1);
                break;
            }
            case 4: 
            {
                size_t taskIndex;
                cout << "Enter task index: ";
                cin >> taskIndex;
                toDoList.removeTask(taskIndex - 1);
                break;
            }
            case 5: 
            {
                cout << "Exiting." <<endl;
                return 0;
            }
            default: 
            {
                cout << "Invalid option. Please try again." <<endl;
                break;
            }
        }
    }

    return 0;
}
