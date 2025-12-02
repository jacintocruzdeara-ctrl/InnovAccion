# InnovAccion
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Innovación - Gestión de Tareas</title>
    <style>
        :root {
            --primary: #2c3e50;
            --secondary: #3498db;
            --accent: #e74c3c;
            --light: #ecf0f1;
            --dark: #2c3e50;
            --success: #2ecc71;
            --warning: #f39c12;
            --danger: #e74c3c;
            --completed: #95a5a6;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
            color: var(--light);
        }
        
        .container {
            max-width: 1000px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            border-radius: 15px;
            padding: 30px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
        }
        
        header {
            text-align: center;
            margin-bottom: 30px;
            padding-bottom: 20px;
            border-bottom: 1px solid rgba(255, 255, 255, 0.2);
        }
        
        h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
            background: linear-gradient(90deg, #fff, #3498db);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }
        
        .subtitle {
            font-size: 1.1rem;
            opacity: 0.8;
        }
        
        .dashboard {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
            margin-bottom: 30px;
        }
        
        .card {
            background: rgba(255, 255, 255, 0.1);
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }
        
        .card h2 {
            font-size: 1.3rem;
            margin-bottom: 15px;
            color: var(--light);
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .card h2 i {
            color: var(--secondary);
        }
        
        .stats {
            display: flex;
            justify-content: space-between;
        }
        
        .stat {
            text-align: center;
        }
        
        .stat-value {
            font-size: 2rem;
            font-weight: bold;
            color: var(--secondary);
        }
        
        .stat-label {
            font-size: 0.9rem;
            opacity: 0.8;
        }
        
        .task-form {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
        }
        
        input, select, button {
            padding: 12px 15px;
            border: none;
            border-radius: 8px;
            font-size: 1rem;
        }
        
        input {
            flex: 1;
            background: rgba(255, 255, 255, 0.15);
            color: white;
        }
        
        input::placeholder {
            color: rgba(255, 255, 255, 0.6);
        }
        
        select {
            background: rgba(255, 255, 255, 0.15);
            color: white;
            cursor: pointer;
        }
        
        button {
            background: var(--secondary);
            color: white;
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: 600;
        }
        
        button:hover {
            background: #2980b9;
            transform: translateY(-2px);
        }
        
        button.danger {
            background: var(--danger);
        }
        
        button.danger:hover {
            background: #c0392b;
        }
        
        button.success {
            background: var(--success);
        }
        
        button.success:hover {
            background: #27ae60;
        }
        
        .task-list {
            margin-top: 20px;
        }
        
        .task-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px;
            margin-bottom: 10px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 8px;
            transition: all 0.3s ease;
        }
        
        .task-item:hover {
            background: rgba(255, 255, 255, 0.15);
            transform: translateX(5px);
        }
        
        .task-item.current {
            border-left: 5px solid var(--secondary);
            background: rgba(52, 152, 219, 0.2);
        }
        
        .task-item.completed {
            opacity: 0.7;
            background: rgba(149, 165, 166, 0.2);
        }
        
        .task-item.completed .task-title {
            text-decoration: line-through;
        }
        
        .task-info {
            display: flex;
            flex-direction: column;
            gap: 5px;
        }
        
        .task-title {
            font-weight: 600;
            font-size: 1.1rem;
        }
        
        .task-meta {
            display: flex;
            gap: 15px;
            font-size: 0.85rem;
            opacity: 0.8;
        }
        
        .priority {
            padding: 3px 8px;
            border-radius: 20px;
            font-size: 0.75rem;
            font-weight: bold;
        }
        
        .priority.high {
            background: var(--danger);
        }
        
        .priority.medium {
            background: var(--warning);
        }
        
        .priority.low {
            background: var(--success);
        }
        
        .task-actions {
            display: flex;
            gap: 10px;
        }
        
        .navigation {
            display: flex;
            justify-content: center;
            gap: 10px;
            margin-top: 20px;
        }
        
        .empty-state {
            text-align: center;
            padding: 40px 20px;
            opacity: 0.7;
        }
        
        .empty-state i {
            font-size: 3rem;
            margin-bottom: 15px;
            opacity: 0.5;
        }
        
        .filters {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
        }
        
        .filter-btn {
            flex: 1;
            background: rgba(255, 255, 255, 0.1);
        }
        
        .filter-btn.active {
            background: var(--secondary);
        }
        
        /* Nuevos estilos para subtareas */
        .subtask-form {
            display: flex;
            gap: 10px;
            margin: 15px 0;
            padding: 10px;
            background: rgba(255, 255, 255, 0.05);
            border-radius: 8px;
        }
        
        .subtasks-container {
            margin-left: 30px;
            border-left: 2px solid rgba(255, 255, 255, 0.2);
            padding-left: 15px;
        }
        
        .subtask-item {
            margin-left: 0;
            background: rgba(255, 255, 255, 0.05);
        }
        
        .subtask-item:hover {
            background: rgba(255, 255, 255, 0.08);
        }
        
        .expand-btn {
            background: transparent;
            border: none;
            color: var(--secondary);
            font-size: 1.2rem;
            cursor: pointer;
            padding: 0 5px;
        }
        
        .tree-view {
            margin-top: 20px;
            background: rgba(0, 0, 0, 0.2);
            border-radius: 8px;
            padding: 15px;
            max-height: 300px;
            overflow-y: auto;
        }
        
        .tree-node {
            margin: 5px 0;
            padding-left: 20px;
            position: relative;
        }
        
        .tree-node::before {
            content: '';
            position: absolute;
            left: 0;
            top: 0;
            bottom: 0;
            width: 2px;
            background: rgba(255, 255, 255, 0.2);
        }
        
        .tree-node:last-child::before {
            height: 10px;
        }
        
        .tree-node::after {
            content: '';
            position: absolute;
            left: 0;
            top: 10px;
            width: 10px;
            height: 2px;
            background: rgba(255, 255, 255, 0.2);
        }
        
        .tree-content {
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .tree-toggle {
            background: transparent;
            border: none;
            color: var(--secondary);
            cursor: pointer;
            width: 20px;
            height: 20px;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        @media (max-width: 768px) {
            .dashboard {
                grid-template-columns: 1fr;
            }
            
            .task-form {
                flex-direction: column;
            }
            
            .task-item {
                flex-direction: column;
                align-items: flex-start;
                gap: 10px;
            }
            
            .task-actions {
                align-self: flex-end;
            }
            
            .subtasks-container {
                margin-left: 15px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>Innovación</h1>
            <p class="subtitle">Sistema avanzado de gestión de tareas con estructura de lista doblemente enlazada y jerarquía de subtareas</p>
        </header>
        
        <div class="dashboard">
            <div class="card">
                <h2><i>📊</i> Estadísticas del Sistema</h2>
                <div class="stats">
                    <div class="stat">
                        <div class="stat-value" id="total-tasks">0</div>
                        <div class="stat-label">Total Tareas</div>
                    </div>
                    <div class="stat">
                        <div class="stat-value" id="completed-tasks">0</div>
                        <div class="stat-label">Completadas</div>
                    </div>
                    <div class="stat">
                        <div class="stat-value" id="current-task">-</div>
                        <div class="stat-label">Tarea Actual</div>
                    </div>
                    <div class="stat">
                        <div class="stat-value" id="pending-tasks">0</div>
                        <div class="stat-label">Pendientes</div>
                    </div>
                </div>
            </div>
            
            <div class="card">
                <h2><i>⚙️</i> Operaciones</h2>
                <div class="task-form">
                    <input type="text" id="task-input" placeholder="Nueva tarea...">
                    <select id="priority-select">
                        <option value="low">Baja Prioridad</option>
                        <option value="medium" selected>Media Prioridad</option>
                        <option value="high">Alta Prioridad</option>
                    </select>
                    <button id="add-front-btn">Añadir al Inicio</button>
                    <button id="add-end-btn">Añadir al Final</button>
                </div>
                
                <div class="subtask-form" id="subtask-form" style="display: none;">
                    <input type="text" id="subtask-input" placeholder="Nueva subtarea...">
                    <select id="subtask-priority-select">
                        <option value="low">Baja Prioridad</option>
                        <option value="medium" selected>Media Prioridad</option>
                        <option value="high">Alta Prioridad</option>
                    </select>
                    <button id="add-subtask-btn">Añadir Subtarea</button>
                </div>
                
                <div class="navigation">
                    <button id="prev-btn">← Anterior</button>
                    <button id="next-btn">Siguiente →</button>
                    <button id="remove-current-btn" class="danger">Eliminar Actual</button>
                    <button id="clear-completed-btn" class="danger">Limpiar Completadas</button>
                </div>
            </div>
        </div>
        
        <div class="card">
            <h2><i>📋</i> Lista de Tareas</h2>
            <div class="filters">
                <button class="filter-btn active" data-filter="all">Todas</button>
                <button class="filter-btn" data-filter="pending">Pendientes</button>
                <button class="filter-btn" data-filter="completed">Completadas</button>
            </div>
            <div class="task-list" id="task-list">
                <div class="empty-state">
                    <i>📝</i>
                    <p>No hay tareas pendientes. ¡Añade tu primera tarea!</p>
                </div>
            </div>
        </div>
        
        <div class="card">
            <h2><i>🌳</i> Vista de Árbol de Tareas</h2>
            <div class="tree-view" id="tree-view">
                <div class="empty-state">
                    <i>🌱</i>
                    <p>No hay tareas para mostrar en el árbol</p>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Clase para representar un nodo de tarea (modificada para incluir subtareas)
        class TaskNode {
            constructor(task, priority = 'medium') {
                this.task = task;
                this.priority = priority;
                this.timestamp = new Date();
                this.completed = false;
                this.prev = null;
                this.next = null;
                this.id = Date.now().toString() + Math.random().toString(36).substr(2, 5);
                // Nueva propiedad: arreglo que contendrá otras Tasks (subtareas)
                this.subtasks = [];
                // Propiedad para controlar la expansión en la UI
                this.expanded = false;
            }
            
            // Nuevo método para añadir subtareas
            addSubTask(nuevaSubTarea) {
                this.subtasks.push(nuevaSubTarea);
            }
        }

        // Clase para la lista doblemente enlazada de tareas
        class TaskMaster {
            constructor() {
                this.head = null;
                this.tail = null;
                this.current = null;
                this.size = 0;
                this.completedCount = 0;
            }

            // Añadir tarea al inicio
            addToFront(task, priority) {
                const newNode = new TaskNode(task, priority);
                
                if (!this.head) {
                    this.head = newNode;
                    this.tail = newNode;
                    this.current = newNode;
                } else {
                    newNode.next = this.head;
                    this.head.prev = newNode;
                    this.head = newNode;
                }
                this.size++;
                return newNode;
            }

            // Añadir tarea al final
            addToEnd(task, priority) {
                const newNode = new TaskNode(task, priority);
                
                if (!this.tail) {
                    this.head = newNode;
                    this.tail = newNode;
                    this.current = newNode;
                } else {
                    newNode.prev = this.tail;
                    this.tail.next = newNode;
                    this.tail = newNode;
                }
                this.size++;
                return newNode;
            }

            // Eliminar tarea actual
            removeCurrent() {
                if (!this.current) return null;
                
                const nodeToRemove = this.current;
                
                // Si la tarea está completada, actualizar el contador
                if (nodeToRemove.completed) {
                    this.completedCount--;
                }
                
                // Reajustar referencias
                if (nodeToRemove.prev) {
                    nodeToRemove.prev.next = nodeToRemove.next;
                } else {
                    this.head = nodeToRemove.next;
                }
                
                if (nodeToRemove.next) {
                    nodeToRemove.next.prev = nodeToRemove.prev;
                } else {
                    this.tail = nodeToRemove.prev;
                }
                
                // Actualizar current
                if (nodeToRemove.next) {
                    this.current = nodeToRemove.next;
                } else if (nodeToRemove.prev) {
                    this.current = nodeToRemove.prev;
                } else {
                    this.current = null;
                }
                
                this.size--;
                return nodeToRemove;
            }

            // Eliminar tarea por ID
            removeById(id) {
                let node = this.head;
                
                while (node) {
                    if (node.id === id) {
                        // Si es la tarea actual, usar removeCurrent
                        if (node === this.current) {
                            return this.removeCurrent();
                        }
                        
                        // Si la tarea está completada, actualizar el contador
                        if (node.completed) {
                            this.completedCount--;
                        }
                        
                        // Reajustar referencias
                        if (node.prev) {
                            node.prev.next = node.next;
                        } else {
                            this.head = node.next;
                        }
                        
                        if (node.next) {
                            node.next.prev = node.prev;
                        } else {
                            this.tail = node.prev;
                        }
                        
                        this.size--;
                        return node;
                    }
                    node = node.next;
                }
                return null;
            }

            // Navegar a la tarea anterior
            navigatePrev() {
                if (this.current && this.current.prev) {
                    this.current = this.current.prev;
                    return this.current;
                }
                return null;
            }

            // Navegar a la siguiente tarea
            navigateNext() {
                if (this.current && this.current.next) {
                    this.current = this.current.next;
                    return this.current;
                }
                return null;
            }

            // Marcar tarea como completada
            toggleComplete(id) {
                let node = this.head;
                
                while (node) {
                    if (node.id === id) {
                        node.completed = !node.completed;
                        
                        if (node.completed) {
                            this.completedCount++;
                        } else {
                            this.completedCount--;
                        }
                        
                        return node;
                    }
                    node = node.next;
                }
                return null;
            }

            // Limpiar tareas completadas
            clearCompleted() {
                let node = this.head;
                let count = 0;
                
                while (node) {
                    const nextNode = node.next;
                    
                    if (node.completed) {
                        // Si la tarea actual es la que se va a eliminar, mover current
                        if (node === this.current) {
                            if (node.next) {
                                this.current = node.next;
                            } else if (node.prev) {
                                this.current = node.prev;
                            } else {
                                this.current = null;
                            }
                        }
                        
                        // Eliminar la tarea
                        if (node.prev) {
                            node.prev.next = node.next;
                        } else {
                            this.head = node.next;
                        }
                        
                        if (node.next) {
                            node.next.prev = node.prev;
                        } else {
                            this.tail = node.prev;
                        }
                        
                        this.size--;
                        count++;
                    }
                    
                    node = nextNode;
                }
                
                this.completedCount = 0;
                return count;
            }

            // Obtener estado del sistema
            getStatus() {
                return {
                    totalTasks: this.size,
                    completedTasks: this.completedCount,
                    pendingTasks: this.size - this.completedCount,
                    currentTask: this.current ? this.current.task : 'Ninguna',
                    currentCompleted: this.current ? this.current.completed : false
                };
            }

            // Obtener todas las tareas como array para renderizar
            getAllTasks() {
                const tasks = [];
                let current = this.head;
                
                while (current) {
                    tasks.push(current);
                    current = current.next;
                }
                
                return tasks;
            }

            // Obtener tareas por filtro
            getFilteredTasks(filter) {
                const allTasks = this.getAllTasks();
                
                switch (filter) {
                    case 'pending':
                        return allTasks.filter(task => !task.completed);
                    case 'completed':
                        return allTasks.filter(task => task.completed);
                    default:
                        return allTasks;
                }
            }

            // Encontrar tarea por ID
            findById(id) {
                let node = this.head;
                
                while (node) {
                    if (node.id === id) {
                        return node;
                    }
                    node = node.next;
                }
                return null;
            }

            // Alternar estado de expansión de una tarea
            toggleExpansion(id) {
                const node = this.findById(id);
                if (node) {
                    node.expanded = !node.expanded;
                    return node;
                }
                return null;
            }
        }

        // Instancia de TaskMaster
        const taskMaster = new TaskMaster();

        // Elementos del DOM
        const taskInput = document.getElementById('task-input');
        const prioritySelect = document.getElementById('priority-select');
        const addFrontBtn = document.getElementById('add-front-btn');
        const addEndBtn = document.getElementById('add-end-btn');
        const prevBtn = document.getElementById('prev-btn');
        const nextBtn = document.getElementById('next-btn');
        const removeCurrentBtn = document.getElementById('remove-current-btn');
        const clearCompletedBtn = document.getElementById('clear-completed-btn');
        const taskList = document.getElementById('task-list');
        const totalTasksEl = document.getElementById('total-tasks');
        const completedTasksEl = document.getElementById('completed-tasks');
        const currentTaskEl = document.getElementById('current-task');
        const pendingTasksEl = document.getElementById('pending-tasks');
        const filterBtns = document.querySelectorAll('.filter-btn');
        const subtaskForm = document.getElementById('subtask-form');
        const subtaskInput = document.getElementById('subtask-input');
        const subtaskPrioritySelect = document.getElementById('subtask-priority-select');
        const addSubtaskBtn = document.getElementById('add-subtask-btn');
        const treeView = document.getElementById('tree-view');

        // Filtro actual
        let currentFilter = 'all';

        // Función RECURSIVA para imprimir el árbol de tareas
        function imprimirArbol(taskNode, prefijo = '') {
            // 1. Imprime la tarea actual
            console.log(prefijo + '- ' + taskNode.task);
            // 2. Paso Recursivo:
            // Llama a esta MISMA función para cada hijo.
            for (const subtask of taskNode.subtasks) {
                imprimirArbol(subtask, prefijo + '  ');
            }
            // 3. Caso Base (implícito):
            // Si un nodo no tiene 'subtasks', el 'for' loop
            // no se ejecuta y la función simplemente termina.
        }

        // Función para generar HTML del árbol de tareas
        function generarArbolHTML(taskNode, nivel = 0) {
            let html = '';
            const indentacion = '  '.repeat(nivel);
            
            // 1. Generar HTML para la tarea actual
            html += `<div class="tree-node" data-id="${taskNode.id}">`;
            html += `<div class="tree-content">`;
            
            // Botón para expandir/contraer si tiene subtareas
            if (taskNode.subtasks.length > 0) {
                html += `<button class="tree-toggle" onclick="toggleTreeExpansion('${taskNode.id}')">`;
                html += taskNode.expanded ? '−' : '+';
                html += `</button>`;
            } else {
                html += `<span class="tree-toggle" style="visibility: hidden;">•</span>`;
            }
            
            // Información de la tarea
            html += `<span class="${taskNode.completed ? 'completed' : ''}">${taskNode.task}</span>`;
            html += `<span class="priority ${taskNode.priority}">${taskNode.priority.toUpperCase()}</span>`;
            html += `</div>`;
            
            // 2. Paso Recursivo:
            // Generar HTML para cada subtarea si está expandido
            if (taskNode.expanded && taskNode.subtasks.length > 0) {
                for (const subtask of taskNode.subtasks) {
                    html += generarArbolHTML(subtask, nivel + 1);
                }
            }
            
            html += `</div>`;
            
            return html;
        }

        // Actualizar la interfaz de usuario
        function updateUI() {
            const status = taskMaster.getStatus();
            totalTasksEl.textContent = status.totalTasks;
            completedTasksEl.textContent = status.completedTasks;
            pendingTasksEl.textContent = status.pendingTasks;
            currentTaskEl.textContent = status.currentTask;
            
            // Mostrar/ocultar formulario de subtareas según si hay tarea actual
            if (taskMaster.current) {
                subtaskForm.style.display = 'flex';
            } else {
                subtaskForm.style.display = 'none';
            }
            
            // Actualizar estado de botones de navegación
            prevBtn.disabled = !taskMaster.current || !taskMaster.current.prev;
            nextBtn.disabled = !taskMaster.current || !taskMaster.current.next;
            removeCurrentBtn.disabled = !taskMaster.current;
            clearCompletedBtn.disabled = status.completedTasks === 0;
            addSubtaskBtn.disabled = !taskMaster.current;
            
            // Renderizar lista de tareas
            const tasks = taskMaster.getFilteredTasks(currentFilter);
            
            if (tasks.length === 0) {
                taskList.innerHTML = `
                    <div class="empty-state">
                        <i>📝</i>
                        <p>No hay tareas ${getFilterText(currentFilter)}. ¡Añade una nueva tarea!</p>
                    </div>
                `;
            } else {
                taskList.innerHTML = tasks.map(task => `
                    <div class="task-item ${task === taskMaster.current ? 'current' : ''} ${task.completed ? 'completed' : ''}" data-id="${task.id}">
                        <div class="task-info">
                            <div class="task-title">${task.task}</div>
                            <div class="task-meta">
                                <span>${task.timestamp.toLocaleString()}</span>
                                <span class="priority ${task.priority}">${task.priority.toUpperCase()}</span>
                                <span>${task.completed ? '✅ Completada' : '⏳ Pendiente'}</span>
                            </div>
                            ${task.subtasks.length > 0 ? `
                                <div class="subtasks-container" id="subtasks-${task.id}">
                                    ${task.subtasks.map(subtask => `
                                        <div class="task-item subtask-item ${subtask.completed ? 'completed' : ''}" data-id="${subtask.id}">
                                            <div class="task-info">
                                                <div class="task-title">${subtask.task}</div>
                                                <div class="task-meta">
                                                    <span>${subtask.timestamp.toLocaleString()}</span>
                                                    <span class="priority ${subtask.priority}">${subtask.priority.toUpperCase()}</span>
                                                    <span>${subtask.completed ? '✅ Completada' : '⏳ Pendiente'}</span>
                                                </div>
                                            </div>
                                            <div class="task-actions">
                                                <button class="${subtask.completed ? 'danger' : 'success'}" onclick="toggleComplete('${subtask.id}')">
                                                    ${subtask.completed ? 'Desmarcar' : 'Completar'}
                                                </button>
                                                <button class="danger" onclick="removeTask('${subtask.id}')">Eliminar</button>
                                            </div>
                                        </div>
                                    `).join('')}
                                </div>
                            ` : ''}
                        </div>
                        <div class="task-actions">
                            <button class="expand-btn" onclick="toggleSubtasks('${task.id}')">
                                ${task.subtasks.length > 0 ? (task.expanded ? '▲' : '▼') : ''}
                            </button>
                            <button class="${task.completed ? 'danger' : 'success'}" onclick="toggleComplete('${task.id}')">
                                ${task.completed ? 'Desmarcar' : 'Completar'}
                            </button>
                            <button class="danger" onclick="removeTask('${task.id}')">Eliminar</button>
                        </div>
                    </div>
                `).join('');
            }
            
            // Actualizar vista de árbol
            const allTasks = taskMaster.getAllTasks();
            if (allTasks.length === 0) {
                treeView.innerHTML = `
                    <div class="empty-state">
                        <i>🌱</i>
                        <p>No hay tareas para mostrar en el árbol</p>
                    </div>
                `;
            } else {
                let treeHTML = '';
                for (const task of allTasks) {
                    treeHTML += generarArbolHTML(task);
                }
                treeView.innerHTML = treeHTML;
            }
        }

        // Obtener texto para el filtro actual
        function getFilterText(filter) {
            switch (filter) {
                case 'pending': return 'pendientes';
                case 'completed': return 'completadas';
                default: return '';
            }
        }

        // Alternar visibilidad de subtareas
        window.toggleSubtasks = (id) => {
            const task = taskMaster.toggleExpansion(id);
            if (task) {
                updateUI();
            }
        };

        // Alternar expansión en el árbol
        window.toggleTreeExpansion = (id) => {
            const task = taskMaster.toggleExpansion(id);
            if (task) {
                updateUI();
            }
        };

        // Añadir tarea al inicio
        addFrontBtn.addEventListener('click', () => {
            const taskText = taskInput.value.trim();
            if (taskText) {
                taskMaster.addToFront(taskText, prioritySelect.value);
                taskInput.value = '';
                updateUI();
            }
        });

        // Añadir tarea al final
        addEndBtn.addEventListener('click', () => {
            const taskText = taskInput.value.trim();
            if (taskText) {
                taskMaster.addToEnd(taskText, prioritySelect.value);
                taskInput.value = '';
                updateUI();
            }
        });

        // Añadir subtarea a la tarea actual
        addSubtaskBtn.addEventListener('click', () => {
            const subtaskText = subtaskInput.value.trim();
            if (subtaskText && taskMaster.current) {
                const nuevaSubTarea = new TaskNode(subtaskText, subtaskPrioritySelect.value);
                taskMaster.current.addSubTask(nuevaSubTarea);
                subtaskInput.value = '';
                updateUI();
                
                // Imprimir el árbol en consola
                console.log("=== Árbol de tareas actualizado ===");
                const allTasks = taskMaster.getAllTasks();
                for (const task of allTasks) {
                    imprimirArbol(task);
                }
            }
        });

        // Navegar a la tarea anterior
        prevBtn.addEventListener('click', () => {
            taskMaster.navigatePrev();
            updateUI();
        });

        // Navegar a la siguiente tarea
        nextBtn.addEventListener('click', () => {
            taskMaster.navigateNext();
            updateUI();
        });

        // Eliminar tarea actual
        removeCurrentBtn.addEventListener('click', () => {
            taskMaster.removeCurrent();
            updateUI();
        });

        // Limpiar tareas completadas
        clearCompletedBtn.addEventListener('click', () => {
            const count = taskMaster.clearCompleted();
            if (count > 0) {
                updateUI();
            }
        });

        // Eliminar tarea específica
        window.removeTask = (id) => {
            taskMaster.removeById(id);
            updateUI();
        };

        // Alternar estado de completado
        window.toggleComplete = (id) => {
            taskMaster.toggleComplete(id);
            updateUI();
        };

        // Configurar filtros
        filterBtns.forEach(btn => {
            btn.addEventListener('click', () => {
                // Remover clase active de todos los botones
                filterBtns.forEach(b => b.classList.remove('active'));
                // Agregar clase active al botón clickeado
                btn.classList.add('active');
                // Actualizar filtro actual
                currentFilter = btn.dataset.filter;
                updateUI();
            });
        });

        // Permitir añadir tareas con Enter
        taskInput.addEventListener('keypress', (e) => {
            if (e.key === 'Enter') {
                const taskText = taskInput.value.trim();
                if (taskText) {
                    taskMaster.addToEnd(taskText, prioritySelect.value);
                    taskInput.value = '';
                    updateUI();
                }
            }
        });

        // Permitir añadir subtareas con Enter
        subtaskInput.addEventListener('keypress', (e) => {
            if (e.key === 'Enter') {
                const subtaskText = subtaskInput.value.trim();
                if (subtaskText && taskMaster.current) {
                    const nuevaSubTarea = new TaskNode(subtaskText, subtaskPrioritySelect.value);
                    taskMaster.current.addSubTask(nuevaSubTarea);
                    subtaskInput.value = '';
                    updateUI();
                    
                    // Imprimir el árbol en consola
                    console.log("=== Árbol de tareas actualizado ===");
                    const allTasks = taskMaster.getAllTasks();
                    for (const task of allTasks) {
                        imprimirArbol(task);
                    }
                }
            }
        });

        // Inicializar la UI
        updateUI();
    </script>
</body>
</html>
