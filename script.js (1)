// Selectors
const taskInput = document.getElementById('taskInput');
const addTaskBtn = document.getElementById('addTaskBtn');
const taskList = document.getElementById('taskList');
const filterButtons = document.querySelectorAll('.filters button');

// Load tasks from localStorage
const savedTasks = JSON.parse(localStorage.getItem('tasks')) || [];
savedTasks.forEach(task => addTaskToDOM(task.text, task.completed));

// Add Task
addTaskBtn.addEventListener('click', () => {
  const taskText = taskInput.value.trim();
  if (taskText) {
    const task = { text: taskText, completed: false };
    addTaskToDOM(taskText, false);
    saveTaskToLocalStorage(task);
    taskInput.value = '';
  }
});

// Add Task to DOM
function addTaskToDOM(taskText, isCompleted) {
  const li = document.createElement('li');
  li.className = `task-item ${isCompleted ? 'completed' : ''}`;

  li.innerHTML = `
    <span>${taskText}</span>
    <div class="action-buttons">
      <button class="mark-complete" onclick="toggleComplete(this)">Complete</button>
      <button class="delete-task" onclick="deleteTask(this)">Delete</button>
    </div>
  `;

  taskList.appendChild(li);
}

// Save Task to Local Storage
function saveTaskToLocalStorage(task) {
  savedTasks.push(task);
  localStorage.setItem('tasks', JSON.stringify(savedTasks));
}

// Update Task in Local Storage
function updateTaskInLocalStorage(taskText, isCompleted) {
  const task = savedTasks.find(task => task.text === taskText);
  if (task) task.completed = isCompleted;
  localStorage.setItem('tasks', JSON.stringify(savedTasks));
}

// Remove Task from Local Storage
function removeTaskFromLocalStorage(taskText) {
  const taskIndex = savedTasks.findIndex(task => task.text === taskText);
  if (taskIndex > -1) savedTasks.splice(taskIndex, 1);
  localStorage.setItem('tasks', JSON.stringify(savedTasks));
}

// Toggle Complete
function toggleComplete(button) {
  const taskItem = button.closest('.task-item');
  const taskText = taskItem.querySelector('span').textContent;
  const isCompleted = taskItem.classList.toggle('completed');
  button.textContent = isCompleted ? 'Undo' : 'Complete';
  updateTaskInLocalStorage(taskText, isCompleted);
}

// Delete Task
function deleteTask(button) {
  const taskItem = button.closest('.task-item');
  const taskText = taskItem.querySelector('span').textContent;
  taskList.removeChild(taskItem);
  removeTaskFromLocalStorage(taskText);
}

// Filter Tasks
filterButtons.forEach(button => {
  button.addEventListener('click', () => {
    const filter = button.dataset.filter;
    const tasks = document.querySelectorAll('.task-item');

    tasks.forEach(task => {
      switch (filter) {
        case 'all':
          task.style.display = 'flex';
          break;
        case 'completed':
          task.style.display = task.classList.contains('completed') ? 'flex' : 'none';
          break;
        case 'pending':
          task.style.display = !task.classList.contains('completed') ? 'flex' : 'none';
          break;
      }
    });
  });
});