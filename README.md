# Ex03 To-Do List using JavaScript
## Date:

## AIM
To create a To-do Application with all features using JavaScript.

## ALGORITHM
### STEP 1
Build the HTML structure (index.html).

### STEP 2
Style the App (style.css).

### STEP 3
Plan the features the To-Do App should have.

### STEP 4
Create a To-do application using Javascript.

### STEP 5
Add functionalities.

### STEP 6
Test the App.

### STEP 7
Open the HTML file in a browser to check layout and functionality.

### STEP 8
Fix styling issues and refine content placement.

### STEP 9
Deploy the website.

### STEP 10
Upload to GitHub Pages for free hosting.

## PROGRAM
index.html :
```
<!DOCTYPE html>

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Todo App</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>

```
My Todo List
---
Organize your tasks easily
```
<!-- Add Todo -->
<div class="input-section">
    <input type="text" id="todoInput" placeholder="Enter a new task...">
    <button id="addBtn">Add Task</button>
</div>

<!-- Todo Statistics -->
<div class="task-info">
    <span id="totalTasks">Total: 0</span>
    <span id="completedTasks">Completed: 0</span>
    <span id="remainingTasks">Remaining: 0</span>
</div>

<!-- Filter Buttons -->
<div class="filters">
    <button class="filter-btn active" data-filter="all">All</button>
    <button class="filter-btn" data-filter="active">Active</button>
    <button class="filter-btn" data-filter="completed">Completed</button>
</div>

<!-- Todo List -->
<ul id="todoList"></ul>

<!-- Clear Completed -->
<button id="clearCompleted">Clear Completed</button>
```
---
<script src="script.js"></script>
```

</body>
</html>
```
---
style.css :
```
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: Arial, sans-serif;
  }

body {
min-height: 100vh;
display: flex;
justify-content: center;
align-items: flex-start;
padding: 50px 20px;
background: linear-gradient(135deg, #667eea, #764ba2);
}

.container {
width: 100%;
max-width: 650px;
background-color: white;
padding: 30px;
border-radius: 15px;
box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
}

h1 {
text-align: center;
color: #333;
margin-bottom: 8px;
}

.subtitle {
text-align: center;
color: #777;
margin-bottom: 25px;
}

/* Input Section */
.input-section {
display: flex;
gap: 10px;
margin-bottom: 20px;
}

.input-section input {
flex: 1;
padding: 13px;
border: 2px solid #ddd;
border-radius: 8px;
font-size: 16px;
outline: none;
}

.input-section input:focus {
border-color: #667eea;
}

#addBtn {
padding: 13px 20px;
border: none;
border-radius: 8px;
background-color: #667eea;
color: white;
font-size: 15px;
cursor: pointer;
}

#addBtn:hover {
background-color: #5366d8;
}

/* Task Statistics */
.task-info {
display: flex;
justify-content: space-between;
background-color: #f5f5f5;
padding: 12px;
border-radius: 8px;
margin-bottom: 20px;
font-size: 14px;
color: #555;
}

/* Filter Buttons */
.filters {
display: flex;
justify-content: center;
gap: 10px;
margin-bottom: 20px;
}

.filter-btn {
padding: 8px 15px;
border: none;
border-radius: 20px;
background-color: #e5e5e5;
cursor: pointer;
font-size: 14px;
}

.filter-btn:hover,
.filter-btn.active {
background-color: #667eea;
color: white;
}

/* Todo List */
#todoList {
list-style: none;
margin-bottom: 20px;
}

.todo-item {
display: flex;
align-items: center;
justify-content: space-between;
background-color: #f8f8f8;
padding: 13px;
margin-bottom: 10px;
border-radius: 8px;
gap: 10px;
}

.todo-left {
display: flex;
align-items: center;
gap: 12px;
flex: 1;
}

.todo-text {
word-break: break-word;
font-size: 16px;
color: #333;
}

.todo-text.completed {
text-decoration: line-through;
color: #999;
}

/* Action Buttons */
.actions {
display: flex;
gap: 8px;
}

.edit-btn,
.delete-btn {
border: none;
padding: 7px 10px;
border-radius: 5px;
color: white;
cursor: pointer;
}

.edit-btn {
background-color: #f0a500;
}

.delete-btn {
background-color: #e74c3c;
}

.edit-btn:hover {
background-color: #d99000;
}

.delete-btn:hover {
background-color: #c0392b;
}

/* Clear Completed Button */
#clearCompleted {
width: 100%;
padding: 12px;
border: none;
border-radius: 8px;
background-color: #333;
color: white;
font-size: 15px;
cursor: pointer;
}

#clearCompleted:hover {
background-color: #555;
}

/* Responsive Design */
@media (max-width: 550px) {
.container {
padding: 20px;
}

```
---
input-section { flex-direction: column; }

#addBtn { width: 100%; }

.task-info { flex-direction: column; gap: 8px; text-align: center; }

.todo-item { align-items: flex-start; flex-direction: column; }

.todo-left { width: 100%; }

.actions { align-self: flex-end; }

```

}
```
---
script.js :
```
const todoInput = document.getElementById("todoInput");
const addBtn = document.getElementById("addBtn");
const todoList = document.getElementById("todoList");
const clearCompletedBtn = document.getElementById("clearCompleted");

const totalTasks = document.getElementById("totalTasks");
const completedTasks = document.getElementById("completedTasks");
const remainingTasks = document.getElementById("remainingTasks");

const filterButtons = document.querySelectorAll(".filter-btn");

let todos = JSON.parse(localStorage.getItem("todos")) || [];
let currentFilter = "all";

/* Save Todos to Local Storage */
function saveTodos() {
localStorage.setItem("todos", JSON.stringify(todos));
}

/* Display Todos */
function displayTodos() {
todoList.innerHTML = "";

```
---
const filteredTodos = todos.filter(function(todo) { if (currentFilter === "active") { return !todo.completed; }
```
if (currentFilter === "completed") {
    return todo.completed;
}

return true;
```
---
});

filteredTodos.forEach(function(todo) { const li = document.createElement("li"); li.className = "todo-item";
```
const leftDiv = document.createElement("div");
leftDiv.className = "todo-left";

const checkbox = document.createElement("input");
checkbox.type = "checkbox";
checkbox.checked = todo.completed;

checkbox.addEventListener("change", function() {
    todo.completed = checkbox.checked;
    saveTodos();
    displayTodos();
});

const taskText = document.createElement("span");
taskText.className = "todo-text";

if (todo.completed) {
    taskText.classList.add("completed");
}

taskText.textContent = todo.text;

leftDiv.appendChild(checkbox);
leftDiv.appendChild(taskText);

const actionsDiv = document.createElement("div");
actionsDiv.className = "actions";

/* Edit Button */
const editBtn = document.createElement("button");
editBtn.textContent = "Edit";
editBtn.className = "edit-btn";

editBtn.addEventListener("click", function() {
    const newText = prompt("Edit your task:", todo.text);

    if (newText !== null && newText.trim() !== "") {
        todo.text = newText.trim();
        saveTodos();
        displayTodos();
    }
});

/* Delete Button */
const deleteBtn = document.createElement("button");
deleteBtn.textContent = "Delete";
deleteBtn.className = "delete-btn";

deleteBtn.addEventListener("click", function() {
    todos = todos.filter(function(item) {
        return item.id !== todo.id;
    });

    saveTodos();
    displayTodos();
});

actionsDiv.appendChild(editBtn);
actionsDiv.appendChild(deleteBtn);

li.appendChild(leftDiv);
li.appendChild(actionsDiv);

todoList.appendChild(li);
```
---
});

updateStatistics();
```

}

/* Add New Todo */
function addTodo() {
const task = todoInput.value.trim();

```
---
if (task === "") { alert("Please enter a task!"); return; }

const newTodo = { id: Date.now(), text: task, completed: false };

todos.push(newTodo);

saveTodos(); displayTodos();

todoInput.value = ""; todoInput.focus();
```

}

/* Add Task Button */
addBtn.addEventListener("click", addTodo);

/* Add Task Using Enter Key */
todoInput.addEventListener("keypress", function(event) {
if (event.key === "Enter") {
addTodo();
}
});

/* Filter Tasks */
filterButtons.forEach(function(button) {
button.addEventListener("click", function() {
filterButtons.forEach(function(btn) {
btn.classList.remove("active");
});
```
button.classList.add("active");

currentFilter = button.dataset.filter;

displayTodos();
```
---
});
```

});

/* Clear Completed Tasks */
clearCompletedBtn.addEventListener("click", function() {
todos = todos.filter(function(todo) {
return !todo.completed;
});

```
---
saveTodos(); displayTodos();
```

});

/* Update Statistics */
function updateStatistics() {
const total = todos.length;

```
---
const completed = todos.filter(function(todo) { return todo.completed; }).length;

const remaining = total - completed;

totalTasks.textContent = "Total: " + total; completedTasks.textContent = "Completed: " + completed; remainingTasks.textContent = "Remaining: " + remaining;


```

}

/* Load Todos When Page Opens */
displayTodos();
```
---


## OUTPUT





## RESULT
The program for creating To-do list using JavaScript is executed successfully.
