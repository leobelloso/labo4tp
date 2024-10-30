## Creación de una Aplicación de Gestión de Tareas con Apache Cordova

### 1. Estructura Básica de la Aplicación

Primero, crearemos una nueva aplicación Cordova:

``` bash
cordova create TaskManager com.example.taskmanager TaskManager
cd TaskManager
cordova platform add android
```

### 2. Estructura de Archivos

La estructura de archivos de tu proyecto Cordova incluirá:

```www/```: Contiene todos los archivos web (HTML, CSS, JS).

```plugins/```: Carpeta donde se instalan los plugins de Cordova.

```platforms/```: Contiene los archivos específicos de cada plataforma (Android, iOS, etc.).

### 3. Creación del HTML

En el archivo ```www/index.html```, crearemos la estructura básica de la aplicación:

``` html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Task Manager</title>
    <link rel="stylesheet" href="css/styles.css">
    <script src="cordova.js"></script>
    <script src="js/index.js"></script>
</head>
<body>
    <header>
        <h1>Task Manager</h1>
    </header>
    <main>
        <form id="task-form">
            <input type="text" id="task-input" placeholder="Nueva tarea">
            <button type="submit">Agregar</button>
        </form>
        <ul id="task-list"></ul>
    </main>
    <footer>
        <p>© 2024 Task Manager</p>
    </footer>
</body>
</html>
```

### 4. Estilo con CSS

En ```www/css/styles.css```, definimos los estilos para nuestra interfaz:

``` css
body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
}

header {
    background-color: #4CAF50;
    color: white;
    padding: 1rem;
    width: 100%;
    text-align: center;
}

main {
    padding: 1rem;
    width: 100%;
    max-width: 600px;
}

form {
    display: flex;
    justify-content: space-between;
    margin-bottom: 1rem;
}

input[type="text"] {
    flex: 1;
    padding: 0.5rem;
    margin-right: 1rem;
    border: 1px solid #ccc;
    border-radius: 4px;
}

button {
    padding: 0.5rem 1rem;
    background-color: #4CAF50;
    color: white;
    border: none;
    border-radius: 4px;
}

ul {
    list-style: none;
    padding: 0;
}

li {
    padding: 0.5rem;
    margin-bottom: 0.5rem;
    border: 1px solid #ccc;
    border-radius: 4px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}
```

### 5. Funcionalidad con JavaScript

En ```www/js/index.js```, agregamos la lógica de la aplicación:

``` javascript
document.addEventListener('deviceready', function() {
    var taskForm = document.getElementById('task-form');
    var taskInput = document.getElementById('task-input');
    var taskList = document.getElementById('task-list');

    // Cargar tareas guardadas
    loadTasks();

    taskForm.addEventListener('submit', function(e) {
        e.preventDefault();
        addTask(taskInput.value);
        taskInput.value = '';
    });

    function addTask(task) {
        var li = document.createElement('li');
        li.textContent = task;

        var deleteButton = document.createElement('button');
        deleteButton.textContent = 'Eliminar';
        deleteButton.addEventListener('click', function() {
            taskList.removeChild(li);
            saveTasks();
        });

        li.appendChild(deleteButton);
        taskList.appendChild(li);
        saveTasks();
    }

    function saveTasks() {
        var tasks = [];
        taskList.querySelectorAll('li').forEach(function(task) {
            tasks.push(task.firstChild.textContent);
        });
        localStorage.setItem('tasks', JSON.stringify(tasks));
    }

    function loadTasks() {
        var tasks = JSON.parse(localStorage.getItem('tasks'));
        if (tasks) {
            tasks.forEach(function(task) {
                addTask(task);
            });
        }
    }
}, false);

```
### 6. Plugins de Cordova

Para las notificaciones locales, instalaremos el plugin ```cordova-plugin-local-notifications```:

``` bash
cordova plugin add cordova-plugin-local-notifications
```

En ```www/js/index.js```, configuramos las notificaciones:

``` javascript
document.addEventListener('deviceready', function() {
    // ...código existente...

    // Notificación al agregar una tarea
    cordova.plugins.notification.local.schedule({
        title: 'Task Manager',
        text: 'Nueva tarea agregada!',
        foreground: true
    });

    // ...código existente...
}, false);
```
Para el almacenamiento local, usaremos el almacenamiento del navegador (localStorage) que ya implementamos en el código de ejemplo. Sin embargo, podrías considerar el plugin ```cordova-sqlite-storage``` para almacenamiento más avanzado:

``` bash
cordova plugin add cordova-sqlite-storage
```

### 7. Integración con Backend (Firebase)

Para conectar con Firebase, agregamos el SDK de Firebase en ```www/index.html```:

``` html
<head>
    <!-- ...otros enlaces... -->
    <script src="https://www.gstatic.com/firebasejs/8.6.1/firebase-app.js"></script>
    <script src="https://www.gstatic.com/firebasejs/8.6.1/firebase-database.js"></script>
</head>
```

Luego, inicializamos Firebase en ```www/js/index.js```:

``` javascript
var firebaseConfig = {
    apiKey: "TU_API_KEY",
    authDomain: "TU_AUTH_DOMAIN",
    databaseURL: "TU_DATABASE_URL",
    projectId: "TU_PROJECT_ID",
    storageBucket: "TU_STORAGE_BUCKET",
    messagingSenderId: "TU_MESSAGING_SENDER_ID",
    appId: "TU_APP_ID"
};
firebase.initializeApp(firebaseConfig);

function addTaskToFirebase(task) {
    firebase.database().ref('tasks/').push(task);
}

// Al agregar una tarea
taskForm.addEventListener('submit', function(e) {
    e.preventDefault();
    var task = taskInput.value;
    addTask(task);
    addTaskToFirebase(task); // Guardar en Firebase
    taskInput.value = '';
});
```

### 8. Compilación
Finalmente, para compilar la aplicación para Android:
``` bash
cordova build android
cordova run android
```

