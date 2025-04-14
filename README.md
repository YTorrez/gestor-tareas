# gestor-tareas
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gestor de Tareas Seguro</title>
    <style>
        :root {
            --primary: #3498db;
            --primary-hover: #2980b9;
            --success: #2ecc71;
            --success-hover: #27ae60;
            --danger: #e74c3c;
            --danger-hover: #c0392b;
            --warning: #f39c12;
            --warning-hover: #e67e22;
            --gray: #7f8c8d;
            --gray-hover: #95a5a6;
            --dark: #2c3e50;
            --light: #ecf0f1;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            line-height: 1.6;
            color: #333;
            /* Fondo tecnológico con imagen */
            background: url('https://images.unsplash.com/photo-1550751827-4bd374c3f58b?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=2070&q=80') no-repeat center center fixed;
            background-size: cover;
            position: relative;
        }

        /* Capa semitransparente para mejorar legibilidad */
        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: rgba(0, 0, 0, 0.7);
            z-index: -1;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        /* Estilos para las páginas de autenticación */
        .auth-container {
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }

        .auth-box {
            background: rgba(255, 255, 255, 0.9);
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
            width: 100%;
            max-width: 450px;
            margin: 20px;
            transition: all 0.3s ease;
            backdrop-filter: blur(5px);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }

        .auth-title {
            text-align: center;
            color: var(--dark);
            margin-bottom: 25px;
            font-size: 28px;
        }

        .auth-tabs {
            display: flex;
            margin-bottom: 20px;
            border-bottom: 1px solid #ddd;
        }

        .auth-tab {
            padding: 10px 20px;
            cursor: pointer;
            text-align: center;
            flex: 1;
            border-bottom: 3px solid transparent;
            transition: all 0.3s;
        }

        .auth-tab.active {
            border-bottom: 3px solid var(--primary);
            font-weight: bold;
            color: var(--primary);
        }

        .auth-tab:hover:not(.active) {
            background-color: rgba(0, 0, 0, 0.05);
        }

        .auth-form {
            display: none;
        }

        .auth-form.active {
            display: block;
        }

        .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: var(--dark);
        }

        .form-control {
            width: 100%;
            padding: 12px 15px;
            border: 1px solid #ddd;
            border-radius: 6px;
            font-size: 16px;
            transition: border 0.3s;
            background-color: rgba(255, 255, 255, 0.8);
        }

        .form-control:focus {
            border-color: var(--primary);
            outline: none;
            box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.2);
            background-color: white;
        }

        .btn {
            display: inline-block;
            padding: 12px 20px;
            border: none;
            border-radius: 6px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            text-align: center;
            transition: all 0.3s;
            width: 100%;
        }

        .btn-primary {
            background-color: var(--primary);
            color: white;
        }

        .btn-primary:hover {
            background-color: var(--primary-hover);
        }

        .btn-success {
            background-color: var(--success);
            color: white;
        }

        .btn-success:hover {
            background-color: var(--success-hover);
        }

        .btn-danger {
            background-color: var(--danger);
            color: white;
        }

        .btn-danger:hover {
            background-color: var(--danger-hover);
        }

        .btn-warning {
            background-color: var(--warning);
            color: white;
        }

        .btn-warning:hover {
            background-color: var(--warning-hover);
        }

        .btn-gray {
            background-color: var(--gray);
            color: white;
        }

        .btn-gray:hover {
            background-color: var(--gray-hover);
        }

        .text-center {
            text-align: center;
        }

        .mt-3 {
            margin-top: 15px;
        }

        .mt-4 {
            margin-top: 20px;
        }

        .mb-3 {
            margin-bottom: 15px;
        }

        .link {
            color: var(--primary);
            text-decoration: none;
            cursor: pointer;
        }

        .link:hover {
            text-decoration: underline;
        }

        .alert {
            padding: 12px 15px;
            border-radius: 6px;
            margin-bottom: 20px;
        }

        .alert-success {
            background-color: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }

        .alert-danger {
            background-color: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }

        /* Estilos para el gestor de tareas */
        .app-container {
            display: none;
            background-color: rgba(255, 255, 255, 0.9);
            border-radius: 10px;
            box-shadow: 0 0 20px rgba(0, 0, 0, 0.2);
            margin: 20px auto;
            padding: 25px;
            backdrop-filter: blur(5px);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }

        .app-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 30px;
            padding-bottom: 15px;
            border-bottom: 1px solid #ddd;
        }

        .app-title {
            color: var(--dark);
            margin: 0;
            font-size: 28px;
        }

        .user-info {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .user-avatar {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background-color: var(--primary);
            color: white;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
        }

        .task-manager {
            background: rgba(255, 255, 255, 0.8);
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            padding: 25px;
            margin-bottom: 30px;
        }

        .section-title {
            color: var(--dark);
            margin-bottom: 20px;
            font-size: 22px;
        }

        .task-list {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
        }

        .task-column {
            background: rgba(249, 249, 249, 0.9);
            padding: 20px;
            border-radius: 8px;
            border: 1px solid #eee;
        }

        .task-card {
            background: white;
            border: 1px solid #ddd;
            border-radius: 8px;
            padding: 18px;
            margin-bottom: 18px;
            position: relative;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.05);
            transition: transform 0.2s, box-shadow 0.2s;
        }

        .task-card:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }

        .task-card.pending {
            border-left: 5px solid var(--danger);
        }

        .task-card.completed {
            border-left: 5px solid var(--success);
        }

        .task-card h3 {
            margin-top: 0;
            color: var(--dark);
            margin-bottom: 10px;
        }

        .task-card p {
            margin: 8px 0;
            line-height: 1.5;
        }

        .task-meta {
            font-size: 14px;
            color: #666;
            margin-top: 10px;
        }

        .task-actions {
            margin-top: 15px;
            display: flex;
            gap: 10px;
        }

        .btn-sm {
            padding: 8px 12px;
            font-size: 14px;
        }

        .status-badge {
            position: absolute;
            top: 15px;
            right: 15px;
            padding: 4px 10px;
            border-radius: 20px;
            font-size: 12px;
            font-weight: bold;
            text-transform: uppercase;
        }

        .pending-badge {
            background-color: var(--danger);
            color: white;
        }

        .completed-badge {
            background-color: var(--success);
            color: white;
        }

        .conclusion-form {
            margin-top: 15px;
            padding-top: 15px;
            border-top: 1px dashed #ddd;
        }

        /* Responsive design */
        @media (max-width: 768px) {
            .task-list {
                grid-template-columns: 1fr;
            }
            
            .app-header {
                flex-direction: column;
                align-items: flex-start;
                gap: 15px;
            }
            
            .user-info {
                width: 100%;
                justify-content: flex-end;
            }
            
            .auth-box {
                padding: 20px;
            }
        }
    </style>
</head>
<body>
    <!-- Páginas de Autenticación -->
    <div class="auth-container" id="authPage">
        <div class="auth-box">
            <h1 class="auth-title">Gestor de Tareas Seguro</h1>
            
            <div class="auth-tabs">
                <div class="auth-tab active" data-tab="login">Iniciar Sesión</div>
                <div class="auth-tab" data-tab="register">Registrarse</div>
                <div class="auth-tab" data-tab="recover">Recuperar Contraseña</div>
            </div>
            
            <!-- Formulario de Login -->
            <form id="loginForm" class="auth-form active">
                <div id="loginAlert" class="alert" style="display: none;"></div>
                
                <div class="form-group">
                    <label for="loginUsername">Usuario</label>
                    <input type="text" id="loginUsername" class="form-control" required>
                </div>
                
                <div class="form-group">
                    <label for="loginPassword">Contraseña</label>
                    <input type="password" id="loginPassword" class="form-control" required>
                </div>
                
                <div class="form-group">
                    <button type="submit" class="btn btn-primary">Ingresar</button>
                </div>
                
                <div class="text-center mt-3">
                    <span class="link" data-tab="recover">¿Olvidaste tu contraseña?</span>
                </div>
            </form>
            
            <!-- Formulario de Registro -->
            <form id="registerForm" class="auth-form">
                <div id="registerAlert" class="alert" style="display: none;"></div>
                
                <div class="form-group">
                    <label for="registerName">Nombre Completo</label>
                    <input type="text" id="registerName" class="form-control" required>
                </div>
                
                <div class="form-group">
                    <label for="registerUsername">Usuario</label>
                    <input type="text" id="registerUsername" class="form-control" required>
                </div>
                
                <div class="form-group">
                    <label for="registerEmail">Correo Electrónico</label>
                    <input type="email" id="registerEmail" class="form-control" required>
                </div>
                
                <div class="form-group">
                    <label for="registerPassword">Contraseña</label>
                    <input type="password" id="registerPassword" class="form-control" required minlength="6">
                </div>
                
                <div class="form-group">
                    <label for="registerConfirmPassword">Confirmar Contraseña</label>
                    <input type="password" id="registerConfirmPassword" class="form-control" required>
                </div>
                
                <div class="form-group">
                    <button type="submit" class="btn btn-success">Registrarse</button>
                </div>
                
                <div class="text-center mt-3">
                    ¿Ya tienes cuenta? <span class="link" data-tab="login">Inicia sesión</span>
                </div>
            </form>
            
            <!-- Formulario de Recuperación -->
            <form id="recoverForm" class="auth-form">
                <div id="recoverAlert" class="alert" style="display: none;"></div>
                
                <div class="form-group">
                    <label for="recoverEmail">Correo Electrónico</label>
                    <input type="email" id="recoverEmail" class="form-control" required>
                </div>
                
                <div class="form-group">
                    <button type="submit" class="btn btn-warning">Recuperar Contraseña</button>
                </div>
                
                <div class="text-center mt-3">
                    <span class="link" data-tab="login">Volver al login</span>
                </div>
            </form>
        </div>
    </div>
    
    <!-- Aplicación - Gestor de Tareas -->
    <div class="container app-container" id="appPage">
        <div class="app-header">
            <h1 class="app-title">Gestor de Tareas Seguro</h1>
            <div class="user-info">
                <div class="user-avatar" id="userAvatar"></div>
                <button id="logoutBtn" class="btn btn-gray btn-sm">Cerrar Sesión</button>
            </div>
        </div>
        
        <div class="task-manager">
            <h2 class="section-title">Agregar Nueva Tarea</h2>
            <form id="taskForm">
                <div class="form-group">
                    <label for="clientName">Nombre del Cliente</label>
                    <input type="text" id="clientName" class="form-control" required>
                </div>
                
                <div class="form-group">
                    <label for="clientAddress">Dirección del Cliente</label>
                    <input type="text" id="clientAddress" class="form-control" required>
                </div>
                
                <div class="form-group">
                    <label for="taskDetail">Detalle del Trabajo</label>
                    <textarea id="taskDetail" class="form-control" required></textarea>
                </div>
                
                <div class="form-group">
                    <button type="submit" class="btn btn-primary">Guardar Tarea</button>
                </div>
            </form>
        </div>
        
        <div class="task-manager">
            <h2 class="section-title">Lista de Tareas</h2>
            <div class="task-list">
                <div class="task-column">
                    <h3>Tareas Pendientes</h3>
                    <div id="pendingTasks"></div>
                </div>
                
                <div class="task-column">
                    <h3>Tareas Completadas</h3>
                    <div id="completedTasks"></div>
                </div>
            </div>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // Elementos del DOM
            const authPage = document.getElementById('authPage');
            const appPage = document.getElementById('appPage');
            const tabs = document.querySelectorAll('.auth-tab');
            const forms = document.querySelectorAll('.auth-form');
            const loginForm = document.getElementById('loginForm');
            const registerForm = document.getElementById('registerForm');
            const recoverForm = document.getElementById('recoverForm');
            const taskForm = document.getElementById('taskForm');
            const logoutBtn = document.getElementById('logoutBtn');
            const pendingTasksContainer = document.getElementById('pendingTasks');
            const completedTasksContainer = document.getElementById('completedTasks');
            const userAvatar = document.getElementById('userAvatar');
            
            // Alertas
            const loginAlert = document.getElementById('loginAlert');
            const registerAlert = document.getElementById('registerAlert');
            const recoverAlert = document.getElementById('recoverAlert');
            
            // Base de datos de usuarios (simulada)
            let usersDB = JSON.parse(localStorage.getItem('usersDB')) || [
                {
                    id: 1,
                    name: 'Administrador',
                    username: 'admin',
                    email: 'admin@example.com',
                    password: 'admin123',
                    createdAt: new Date().toISOString()
                }
            ];
            
            // Base de datos de recuperaciones (simulada)
            let recoveryDB = JSON.parse(localStorage.getItem('recoveryDB')) || [];
            
            // Tareas
            let tasksDB = JSON.parse(localStorage.getItem('tasksDB')) || [];
            
            // Cambiar entre pestañas
            tabs.forEach(tab => {
                tab.addEventListener('click', function() {
                    // Remover clase active de todas las pestañas
                    tabs.forEach(t => t.classList.remove('active'));
                    // Agregar clase active a la pestaña clickeada
                    this.classList.add('active');
                    
                    // Ocultar todos los formularios
                    forms.forEach(form => form.classList.remove('active'));
                    // Mostrar el formulario correspondiente
                    const tabName = this.getAttribute('data-tab');
                    document.getElementById(`${tabName}Form`).classList.add('active');
                    
                    // Limpiar alertas
                    loginAlert.style.display = 'none';
                    registerAlert.style.display = 'none';
                    recoverAlert.style.display = 'none';
                });
            });
            
            // Enlaces para cambiar de pestaña
            document.querySelectorAll('.link').forEach(link => {
                link.addEventListener('click', function() {
                    const tabName = this.getAttribute('data-tab');
                    tabs.forEach(tab => {
                        if (tab.getAttribute('data-tab') === tabName) {
                            tab.click();
                        }
                    });
                });
            });
            
            // Login
            loginForm.addEventListener('submit', function(e) {
                e.preventDefault();
                
                const username = document.getElementById('loginUsername').value;
                const password = document.getElementById('loginPassword').value;
                
                // Validar credenciales
                const user = usersDB.find(u => u.username === username && u.password === password);
                
                if (user) {
                    // Iniciar sesión
                    localStorage.setItem('currentUser', JSON.stringify(user));
                    showAppPage();
                    loadTasks();
                } else {
                    showAlert(loginAlert, 'Usuario o contraseña incorrectos', 'danger');
                }
            });
            
            // Registro
            registerForm.addEventListener('submit', function(e) {
                e.preventDefault();
                
                const name = document.getElementById('registerName').value;
                const username = document.getElementById('registerUsername').value;
                const email = document.getElementById('registerEmail').value;
                const password = document.getElementById('registerPassword').value;
                const confirmPassword = document.getElementById('registerConfirmPassword').value;
                
                // Validaciones
                if (password !== confirmPassword) {
                    showAlert(registerAlert, 'Las contraseñas no coinciden', 'danger');
                    return;
                }
                
                if (usersDB.some(u => u.username === username)) {
                    showAlert(registerAlert, 'El nombre de usuario ya está en uso', 'danger');
                    return;
                }
                
                if (usersDB.some(u => u.email === email)) {
                    showAlert(registerAlert, 'El correo electrónico ya está registrado', 'danger');
                    return;
                }
                
                // Crear nuevo usuario
                const newUser = {
                    id: Date.now(),
                    name,
                    username,
                    email,
                    password,
                    createdAt: new Date().toISOString()
                };
                
                usersDB.push(newUser);
                localStorage.setItem('usersDB', JSON.stringify(usersDB));
                
                showAlert(registerAlert, 'Registro exitoso. Ahora puedes iniciar sesión.', 'success');
                document.getElementById('registerForm').reset();
                tabs[0].click(); // Cambiar a pestaña de login
            });
            
            // Recuperación de contraseña
            recoverForm.addEventListener('submit', function(e) {
                e.preventDefault();
                
                const email = document.getElementById('recoverEmail').value;
                const user = usersDB.find(u => u.email === email);
                
                if (user) {
                    // Generar token de recuperación (simulado)
                    const token = Math.random().toString(36).substring(2, 15) + Math.random().toString(36).substring(2, 15);
                    const recoveryRequest = {
                        email,
                        token,
                        createdAt: new Date().toISOString(),
                        expiresAt: new Date(Date.now() + 3600000).toISOString() // Expira en 1 hora
                    };
                    
                    recoveryDB.push(recoveryRequest);
                    localStorage.setItem('recoveryDB', JSON.stringify(recoveryDB));
                    
                    // En un entorno real, aquí enviaríamos un correo con el token
                    showAlert(recoverAlert, `Se ha enviado un enlace de recuperación a ${email} (simulado)`, 'success');
                } else {
                    showAlert(recoverAlert, 'No existe una cuenta con ese correo electrónico', 'danger');
                }
            });
            
            // Logout
            logoutBtn.addEventListener('click', function() {
                localStorage.removeItem('currentUser');
                showAuthPage();
            });
            
            // Agregar tarea
            taskForm.addEventListener('submit', function(e) {
                e.preventDefault();
                
                const clientName = document.getElementById('clientName').value;
                const clientAddress = document.getElementById('clientAddress').value;
                const taskDetail = document.getElementById('taskDetail').value;
                
                if (clientName && clientAddress && taskDetail) {
                    addTask(clientName, clientAddress, taskDetail);
                    taskForm.reset();
                }
            });
            
            // Función para mostrar alertas
            function showAlert(element, message, type) {
                element.textContent = message;
                element.className = `alert alert-${type}`;
                element.style.display = 'block';
            }
            
            // Función para mostrar página de autenticación
            function showAuthPage() {
                authPage.style.display = 'flex';
                appPage.style.display = 'none';
                loginForm.reset();
                registerForm.reset();
                recoverForm.reset();
                tabs[0].click(); // Mostrar pestaña de login
            }
            
            // Función para mostrar aplicación
            function showAppPage() {
                authPage.style.display = 'none';
                appPage.style.display = 'block';
                
                // Mostrar avatar de usuario
                const currentUser = JSON.parse(localStorage.getItem('currentUser'));
                if (currentUser) {
                    userAvatar.textContent = currentUser.name.charAt(0).toUpperCase();
                }
            }
            
            // Función para agregar tarea
            function addTask(clientName, clientAddress, taskDetail) {
                const currentUser = JSON.parse(localStorage.getItem('currentUser'));
                
                const newTask = {
                    id: Date.now(),
                    clientName,
                    clientAddress,
                    taskDetail,
                    status: 'pending',
                    conclusion: '',
                    createdAt: new Date().toISOString(),
                    createdBy: currentUser.username,
                    completedAt: null,
                    completedBy: null
                };
                
                tasksDB.push(newTask);
                localStorage.setItem('tasksDB', JSON.stringify(tasksDB));
                renderTasks();
            }
            
            // Función para completar tarea
            function completeTask(taskId, conclusion) {
                const currentUser = JSON.parse(localStorage.getItem('currentUser'));
                const taskIndex = tasksDB.findIndex(task => task.id === taskId);
                
                if (taskIndex !== -1) {
                    tasksDB[taskIndex].status = 'completed';
                    tasksDB[taskIndex].conclusion = conclusion;
                    tasksDB[taskIndex].completedAt = new Date().toISOString();
                    tasksDB[taskIndex].completedBy = currentUser.username;
                    
                    localStorage.setItem('tasksDB', JSON.stringify(tasksDB));
                    renderTasks();
                }
            }
            
            // Función para eliminar tarea
            function deleteTask(taskId) {
                tasksDB = tasksDB.filter(task => task.id !== taskId);
                localStorage.setItem('tasksDB', JSON.stringify(tasksDB));
                renderTasks();
            }
            
            // Función para renderizar tareas
            function renderTasks() {
                pendingTasksContainer.innerHTML = '';
                completedTasksContainer.innerHTML = '';
                
                tasksDB.forEach(task => {
                    const taskCard = document.createElement('div');
                    taskCard.className = `task-card ${task.status}`;
                    
                    const statusBadge = document.createElement('span');
                    statusBadge.className = `status-badge ${task.status}-badge`;
                    statusBadge.textContent = task.status === 'pending' ? 'Pendiente' : 'Completada';
                    
                    const clientName = document.createElement('h3');
                    clientName.textContent = task.clientName;
                    
                    const clientAddress = document.createElement('p');
                    clientAddress.innerHTML = `<strong>Dirección:</strong> ${task.clientAddress}`;
                    
                    const taskDetail = document.createElement('p');
                    taskDetail.innerHTML = `<strong>Trabajo a realizar:</strong> ${task.taskDetail}`;
                    
                    const createdInfo = document.createElement('p');
                    createdInfo.className = 'task-meta';
                    createdInfo.innerHTML = `<strong>Creada por:</strong> ${task.createdBy}<br>
                                          <strong>Fecha:</strong> ${new Date(task.createdAt).toLocaleString()}`;
                    
                    if (task.status === 'completed') {
                        const conclusion = document.createElement('p');
                        conclusion.innerHTML = `<strong>Conclusión:</strong> ${task.conclusion}`;
                        
                        const completedInfo = document.createElement('p');
                        completedInfo.className = 'task-meta';
                        completedInfo.innerHTML = `<strong>Completada por:</strong> ${task.completedBy}<br>
                                                <strong>Fecha:</strong> ${new Date(task.completedAt).toLocaleString()}`;
                        
                        const deleteBtn = document.createElement('button');
                        deleteBtn.className = 'btn btn-danger btn-sm';
                        deleteBtn.textContent = 'Eliminar';
                        deleteBtn.onclick = () => deleteTask(task.id);
                        
                        const taskActions = document.createElement('div');
                        taskActions.className = 'task-actions';
                        taskActions.appendChild(deleteBtn);
                        
                        taskCard.appendChild(statusBadge);
                        taskCard.appendChild(clientName);
                        taskCard.appendChild(clientAddress);
                        taskCard.appendChild(taskDetail);
                        taskCard.appendChild(conclusion);
                        taskCard.appendChild(createdInfo);
                        taskCard.appendChild(completedInfo);
                        taskCard.appendChild(taskActions);
                        
                        completedTasksContainer.appendChild(taskCard);
                    } else {
                        const conclusionForm = document.createElement('div');
                        conclusionForm.className = 'conclusion-form';
                        
                        const conclusionLabel = document.createElement('label');
                        conclusionLabel.textContent = 'Agregar conclusión para completar:';
                        
                        const conclusionInput = document.createElement('textarea');
                        conclusionInput.className = 'form-control';
                        conclusionInput.placeholder = 'Describe cómo se completó la tarea...';
                        conclusionInput.id = `conclusion-${task.id}`;
                        
                        const completeBtn = document.createElement('button');
                        completeBtn.className = 'btn btn-success btn-sm';
                        completeBtn.textContent = 'Completar';
                        completeBtn.onclick = () => {
                            const conclusion = document.getElementById(`conclusion-${task.id}`).value;
                            if (conclusion) {
                                completeTask(task.id, conclusion);
                            } else {
                                alert('Por favor ingresa una conclusión para completar la tarea.');
                            }
                        };
                        
                        const deleteBtn = document.createElement('button');
                        deleteBtn.className = 'btn btn-danger btn-sm';
                        deleteBtn.textContent = 'Eliminar';
                        deleteBtn.onclick = () => deleteTask(task.id);
                        
                        const taskActions = document.createElement('div');
                        taskActions.className = 'task-actions';
                        taskActions.appendChild(completeBtn);
                        taskActions.appendChild(deleteBtn);
                        
                        conclusionForm.appendChild(conclusionLabel);
                        conclusionForm.appendChild(conclusionInput);
                        
                        taskCard.appendChild(statusBadge);
                        taskCard.appendChild(clientName);
                        taskCard.appendChild(clientAddress);
                        taskCard.appendChild(taskDetail);
                        taskCard.appendChild(createdInfo);
                        taskCard.appendChild(conclusionForm);
                        taskCard.appendChild(taskActions);
                        
                        pendingTasksContainer.appendChild(taskCard);
                    }
                });
            }
            
            // Cargar tareas
            function loadTasks() {
                renderTasks();
            }
            
            // Verificar si hay usuario logueado al cargar
            const currentUser = localStorage.getItem('currentUser');
            if (currentUser) {
                showAppPage();
                loadTasks();
            } else {
                showAuthPage();
            }
        });
    </script>
</body>
</html>
