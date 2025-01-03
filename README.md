# Saving_given_info
Saves given information from the user
import React, { useState } from 'react';

function Task({ task, toggleComplete, deleteTask }) {
  return (
    <li>
      <input
        type="checkbox"
        checked={task.completed}
        onChange={() => toggleComplete(task.id)} // Add semicolon here
      />
      <span style={{ textDecoration: task.completed ? 'line-through' : 'none' }}>
        {task.text}
      </span>
      <button onClick={() => deleteTask(task.id)}>Delete</button>
    </li>
  );
}

function TaskList() {
  const [tasks, setTasks] = useState([]);

  const addTask = (text) => {
    setTasks([...tasks, { id: Date.now(), text, completed: false }]);
  };

  const toggleComplete = (id) => {
    setTasks(
      tasks.map((task) => (task.id === id ? { ...task, completed: !task.completed } : task))
    );
  };

  const deleteTask = (id) => {
    setTasks(tasks.filter((task) => task.id !== id));
  };

  return (
    <div>
      <input type="text" placeholder="Add a task" onKeyDown={(e) => e.key === 'Enter' && addTask(e.target.value)} />
      <ul>
        {tasks.map((task) => (
          <Task key={task.id} task={task} toggleComplete={toggleComplete} deleteTask={deleteTask} />
        ))}
      </ul>
    </div>
  );
}

export default TaskList;
