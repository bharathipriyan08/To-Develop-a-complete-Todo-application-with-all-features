##Develop a complete Todo application with all features

```
#program:

import React, { useState } from 'react';
import './App.css';

function App() {
  const [tasks, setTasks] = useState([]);
  const [newTask, setNewTask] = useState('');
  const [editTaskId, setEditTaskId] = useState(null);

  const handleAddTask = () => {
    if (newTask.trim() !== '') {
      const newTaskItem = {
        id: Date.now(),
        text: newTask,
        completed: false,
      };
      setTasks([...tasks, newTaskItem]);
      setNewTask('');
    }
  };

  const handleEditTask = (id, newText) => {
    const updatedTasks = tasks.map((task) => {
      if (task.id === id) {
        return {
          ...task,
          text: newText,
        };
      }
      return task;
    });
    setTasks(updatedTasks);
    setEditTaskId(null);
  };

  const handleDeleteTask = (id) => {
    const updatedTasks = tasks.filter((task) => task.id !== id);
    setTasks(updatedTasks);
  };

  const handleToggleComplete = (id) => {
    const updatedTasks = tasks.map((task) => {
      if (task.id === id) {
        return {
          ...task,
          completed: !task.completed,
        };
      }
      return task;
    });
    setTasks(updatedTasks);
  };

  return (
    <div className="todo-app">
      <h1 style={{textAlign:"center"}}>TODO LIST</h1>
      <div className="task-input">
        <input
          type="text"
          value={newTask}
          onChange={(e) => setNewTask(e.target.value)}
          placeholder="Enter a new task"
        />
        <button onClick={handleAddTask}>Add</button>
      </div>
      <ul className="task-list">
        {tasks.map((task) => (
          <li key={task.id} className={task.completed ? 'completed' : ''}>
            <input
              type="checkbox"
              checked={task.completed}
              onChange={() => handleToggleComplete(task.id)}
            />
            {editTaskId === task.id ? (
              <input
                type="text"
                value={task.text}
                onChange={(e) => handleEditTask(task.id, e.target.value)}
              />
            ) : (
              <span>{task.text}</span>
            )}
            <div className="task-actions">
              {/* {editTaskId === task.id ? (
                <button onClick={() => handleEditTask(task.id, task.text)}>Save</button>
              ) : (
                <button onClick={() => setEditTaskId(task.id)}>Edit</button>
              )} */}
              <button onClick={() => handleDeleteTask(task.id)}>Delete</button>
            </div>
          </li>
        ))}
      </ul>
    </div>
  );
}
export default App;
```

##output:

![image](https://github.com/bharathipriyan08/tolo/assets/113762012/332817fe-011f-4779-8329-746d943f20fe)
