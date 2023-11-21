# Exp-5-Develop-a-complete-Todo-application-with-all-features
```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Todo App</title>
  <style>
    body {
        font-family: Arial, sans-serif;
        margin: 0;
        padding: 0;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        height: 100vh;
        background-color: #f4f4f4;
      }
      
      .container {
        text-align: center;
      }
      
      .input-container {
        margin-bottom: 20px;
      }
      
      #taskInput {
        padding: 8px;
      }
      
      .task-list {
        list-style-type: none;
        padding: 0;
        width: 300px;
      }
      
      .task {
        display: flex;
        justify-content: space-between;
        align-items: center;
        background-color: #fff;
        padding: 10px;
        margin: 5px 0;
        border-radius: 5px;
      }
      
      .complete-task {
        text-decoration: line-through;
        opacity: 0.7;
      }
      
  </style>
</head>
<body>
  <div class="container">
    <h1>Todo App</h1>
    <div id="taskInputContainer" class="input-container">
      <input type="text" id="taskInput" placeholder="Add a new task">
      <button onclick="addTask()">Add Task</button>
    </div>
    <ul id="taskList" class="task-list"></ul>
  </div>

  <script>
    document.addEventListener('DOMContentLoaded', function () {
        fetchTasks();
      });
      
      function addTask() {
        const taskInput = document.getElementById('taskInput');
        const task = taskInput.value;
      
        if (task.trim() === '') {
          alert('Please enter a task');
          return;
        }
      
        const tasks = getTasksFromStorage();
        tasks.push({ text: task, completed: false });
        saveTasksToStorage(tasks);
      
        taskInput.value = '';
        fetchTasks();
      }
      
      function toggleComplete(index) {
        const tasks = getTasksFromStorage();
        tasks[index].completed = !tasks[index].completed;
        saveTasksToStorage(tasks);
        fetchTasks();
      }
      
      function deleteTask(index) {
        const tasks = getTasksFromStorage();
        tasks.splice(index, 1);
        saveTasksToStorage(tasks);
        fetchTasks();
      }
      
      function fetchTasks() {
        const taskList = document.getElementById('taskList');
        taskList.innerHTML = '';
      
        const tasks = getTasksFromStorage();
      
        tasks.forEach((task, index) => {
          const listItem = document.createElement('li');
          listItem.className = `task ${task.completed ? 'complete-task' : ''}`;
          listItem.innerHTML = `
            <span>${task.text}</span>
            <div>
              <button onclick="toggleComplete(${index})">${task.completed ? 'Undo' : 'Complete'}</button>
              <button onclick="deleteTask(${index})">Delete</button>
            </div>
          `;
          taskList.appendChild(listItem);
        });
      }
      
      function getTasksFromStorage() {
        const storedTasks = localStorage.getItem('tasks');
        return storedTasks ? JSON.parse(storedTasks) : [];
      }
      
      function saveTasksToStorage(tasks) {
        localStorage.setItem('tasks', JSON.stringify(tasks));
      }
      
  </script>
</body>
</html>

```

# output
![Screenshot (84)](https://github.com/21002624/Exp-5-Develop-a-complete-Todo-application-with-all-features/assets/113762183/409c7a39-2384-410b-9ff2-f197784073cb)
