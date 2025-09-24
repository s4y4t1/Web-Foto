<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PhotoDrive - Your Photo Storage</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Roboto, Oxygen, Ubuntu, sans-serif;
        }

        :root {
            --primary-color: #1a73e8;
            --secondary-color: #f1f3f4;
            --text-color: #202124;
            --border-color: #dadce0;
            --hover-color: rgba(26, 115, 232, 0.08);
            --delete-color: #ea4335;
            --card-shadow: 0 1px 2px 0 rgba(60, 64, 67, 0.3), 0 1px 3px 1px rgba(60, 64, 67, 0.15);
            --header-height: 64px;
        }

        body {
            background-color: #fff;
            color: var(--text-color);
            min-height: 100vh;
            transition: all 0.3s ease;
        }

        /* Login Page Styles */
        .login-container {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
            background: linear-gradient(135deg, #1a73e8 0%, #6c5ce7 100%);
            padding: 20px;
        }

        .login-card {
            background: white;
            border-radius: 8px;
            padding: 40px;
            width: 100%;
            max-width: 450px;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.15);
        }

        .logo {
            text-align: center;
            margin-bottom: 30px;
        }

        .logo i {
            font-size: 42px;
            color: var(--primary-color);
        }

        .logo h1 {
            font-weight: 500;
            margin-top: 10px;
            color: var(--text-color);
        }

        .input-group {
            margin-bottom: 24px;
        }

        .input-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 500;
        }

        .input-group input {
            width: 100%;
            padding: 14px;
            border: 1px solid var(--border-color);
            border-radius: 4px;
            font-size: 16px;
            transition: border 0.3s;
        }

        .input-group input:focus {
            outline: none;
            border-color: var(--primary-color);
        }

        .btn {
            width: 100%;
            padding: 14px;
            background-color: var(--primary-color);
            color: white;
            border: none;
            border-radius: 4px;
            font-size: 16px;
            font-weight: 500;
            cursor: pointer;
            transition: background-color 0.3s;
        }

        .btn:hover {
            background-color: #1565c0;
        }

        /* Main App Styles */
        .app-container {
            display: none;
            height: 100vh;
            overflow: hidden;
        }

        .header {
            height: var(--header-height);
            display: flex;
            align-items: center;
            padding: 0 24px;
            border-bottom: 1px solid var(--border-color);
            justify-content: space-between;
        }

        .header-left {
            display: flex;
            align-items: center;
        }

        .menu-toggle {
            margin-right: 20px;
            cursor: pointer;
            font-size: 20px;
        }

        .logo-small {
            display: flex;
            align-items: center;
            font-weight: 500;
        }

        .logo-small i {
            margin-right: 10px;
            color: var(--primary-color);
        }

        .header-right {
            display: flex;
            align-items: center;
        }

        .user-info {
            display: flex;
            align-items: center;
            margin-right: 16px;
        }

        .user-avatar {
            width: 36px;
            height: 36px;
            border-radius: 50%;
            background-color: var(--primary-color);
            color: white;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-right: 8px;
            font-weight: 500;
        }

        .logout-btn {
            background: none;
            border: none;
            color: var(--primary-color);
            cursor: pointer;
            font-size: 14px;
        }

        .main-content {
            display: flex;
            height: calc(100vh - var(--header-height));
        }

        .sidebar {
            width: 250px;
            background-color: var(--secondary-color);
            border-right: 1px solid var(--border-color);
            padding: 24px 0;
            overflow-y: auto;
        }

        .sidebar-item {
            padding: 12px 24px;
            display: flex;
            align-items: center;
            cursor: pointer;
            transition: background-color 0.2s;
        }

        .sidebar-item:hover {
            background-color: var(--hover-color);
        }

        .sidebar-item.active {
            background-color: #e8f0fe;
            color: var(--primary-color);
            font-weight: 500;
        }

        .sidebar-item i {
            margin-right: 16px;
            font-size: 18px;
        }

        .content-area {
            flex: 1;
            padding: 24px;
            overflow-y: auto;
            background-color: #f8f9fa;
        }

        .content-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 24px;
        }

        .content-title {
            font-size: 24px;
            font-weight: 500;
        }

        .upload-btn {
            background-color: var(--primary-color);
            color: white;
            border: none;
            padding: 10px 16px;
            border-radius: 4px;
            cursor: pointer;
            display: flex;
            align-items: center;
            font-weight: 500;
        }

        .upload-btn i {
            margin-right: 8px;
        }

        .photos-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            gap: 20px;
        }

        .photo-card {
            background: white;
            border-radius: 8px;
            overflow: hidden;
            box-shadow: var(--card-shadow);
            transition: transform 0.3s;
        }

        .photo-card:hover {
            transform: translateY(-4px);
        }

        .photo-thumbnail {
            height: 160px;
            overflow: hidden;
            position: relative;
        }

        .photo-thumbnail img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .photo-info {
            padding: 12px;
        }

        .photo-name {
            font-weight: 500;
            margin-bottom: 4px;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }

        .photo-meta {
            display: flex;
            justify-content: space-between;
            color: #5f6368;
            font-size: 13px;
        }

        .photo-actions {
            display: flex;
            padding: 8px 12px;
            border-top: 1px solid var(--border-color);
            justify-content: space-between;
        }

        .action-btn {
            background: none;
            border: none;
            cursor: pointer;
            color: #5f6368;
            font-size: 14px;
        }

        .action-btn:hover {
            color: var(--primary-color);
        }

        .delete-btn:hover {
            color: var(--delete-color);
        }

        /* Upload Modal */
        .modal {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: rgba(0, 0, 0, 0.5);
            display: none;
            align-items: center;
            justify-content: center;
            z-index: 1000;
        }

        .modal-content {
            background-color: white;
            padding: 24px;
            border-radius: 8px;
            width: 90%;
            max-width: 500px;
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }

        .modal-title {
            font-size: 20px;
            font-weight: 500;
        }

        .close-btn {
            background: none;
            border: none;
            font-size: 24px;
            cursor: pointer;
            color: #5f6368;
        }

        .file-input-container {
            border: 2px dashed var(--border-color);
            border-radius: 8px;
            padding: 40px 20px;
            text-align: center;
            margin-bottom: 20px;
            cursor: pointer;
        }

        .file-input-container:hover {
            background-color: var(--hover-color);
        }

        .file-input-container i {
            font-size: 48px;
            color: var(--primary-color);
            margin-bottom: 16px;
        }

        .file-input {
            display: none;
        }

        .modal-actions {
            display: flex;
            justify-content: flex-end;
            margin-top: 20px;
        }

        .cancel-btn {
            background: none;
            border: none;
            padding: 10px 16px;
            margin-right: 12px;
            cursor: pointer;
            color: #5f6368;
        }

        /* Empty state */
        .empty-state {
            text-align: center;
            padding: 60px 20px;
            color: #5f6368;
        }

        .empty-state i {
            font-size: 64px;
            margin-bottom: 16px;
            opacity: 0.5;
        }

        /* Responsive styles */
        @media (max-width: 768px) {
            .sidebar {
                width: 200px;
            }
            
            .photos-grid {
                grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
            }
        }

        @media (max-width: 576px) {
            .main-content {
                flex-direction: column;
            }
            
            .sidebar {
                width: 100%;
                height: auto;
                border-right: none;
                border-bottom: 1px solid var(--border-color);
                padding: 0;
                overflow-x: auto;
                display: flex;
            }
            
            .sidebar-item {
                padding: 16px;
                white-space: nowrap;
            }
            
            .content-area {
                height: calc(100vh - var(--header-height) - 60px);
            }
            
            .login-card {
                padding: 24px;
            }
        }
    </style>
</head>
<body>
    <!-- Login Page -->
    <div class="login-container" id="loginPage">
        <div class="login-card">
            <div class="logo">
                <i class="fas fa-cloud-upload-alt"></i>
                <h1>PhotoDrive</h1>
            </div>
            <div class="input-group">
                <label for="username">Username</label>
                <input type="text" id="username" placeholder="Enter your username">
            </div>
            <button class="btn" id="loginBtn">Sign In</button>
        </div>
    </div>

    <!-- Main App -->
    <div class="app-container" id="appContainer">
        <header class="header">
            <div class="header-left">
                <div class="menu-toggle">
                    <i class="fas fa-bars"></i>
                </div>
                <div class="logo-small">
                    <i class="fas fa-cloud-upload-alt"></i>
                    <span>PhotoDrive</span>
                </div>
            </div>
            <div class="header-right">
                <div class="user-info">
                    <div class="user-avatar" id="userAvatar">U</div>
                    <span id="userName">User</span>
                </div>
                <button class="logout-btn" id="logoutBtn">Logout</button>
            </div>
        </header>

        <div class="main-content">
            <aside class="sidebar">
                <div class="sidebar-item active" data-section="photos">
                    <i class="fas fa-images"></i>
                    <span>My Photos</span>
                </div>
                <div class="sidebar-item" data-section="recycle">
                    <i class="fas fa-trash"></i>
                    <span>Recycle Bin</span>
                </div>
            </aside>

            <main class="content-area">
                <div class="content-header">
                    <h2 class="content-title" id="sectionTitle">My Photos</h2>
                    <button class="upload-btn" id="uploadBtn">
                        <i class="fas fa-upload"></i>
                        Upload
                    </button>
                </div>

                <div class="photos-grid" id="photosContainer">
                    <!-- Photos will be loaded here -->
                </div>
            </main>
        </div>
    </div>

    <!-- Upload Modal -->
    <div class="modal" id="uploadModal">
        <div class="modal-content">
            <div class="modal-header">
                <h3 class="modal-title">Upload Photo</h3>
                <button class="close-btn" id="closeModal">&times;</button>
            </div>
            <label for="fileInput" class="file-input-container">
                <i class="fas fa-cloud-upload-alt"></i>
                <p>Click to select a photo or drag and drop</p>
            </label>
            <input type="file" id="fileInput" class="file-input" accept="image/*">
            <div class="modal-actions">
                <button class="cancel-btn" id="cancelUpload">Cancel</button>
                <button class="btn" id="confirmUpload" disabled>Upload</button>
            </div>
        </div>
    </div>

    <script>
        // DOM elements
        const loginPage = document.getElementById('loginPage');
        const appContainer = document.getElementById('appContainer');
        const usernameInput = document.getElementById('username');
        const loginBtn = document.getElementById('loginBtn');
        const logoutBtn = document.getElementById('logoutBtn');
        const userAvatar = document.getElementById('userAvatar');
        const userName = document.getElementById('userName');
        const sidebarItems = document.querySelectorAll('.sidebar-item');
        const sectionTitle = document.getElementById('sectionTitle');
        const photosContainer = document.getElementById('photosContainer');
        const uploadBtn = document.getElementById('uploadBtn');
        const uploadModal = document.getElementById('uploadModal');
        const closeModal = document.getElementById('closeModal');
        const cancelUpload = document.getElementById('cancelUpload');
        const fileInput = document.getElementById('fileInput');
        const confirmUpload = document.getElementById('confirmUpload');

        // App state
        let currentUser = '';
        let currentSection = 'photos';
        let uploadedPhotos = JSON.parse(localStorage.getItem('uploadedPhotos')) || [];
        let deletedPhotos = JSON.parse(localStorage.getItem('deletedPhotos')) || [];

        // Initialize the app
        function initApp() {
            // Check if user is already logged in
            const savedUser = localStorage.getItem('currentUser');
            if (savedUser) {
                currentUser = savedUser;
                showApp();
            }

            // Set up event listeners
            loginBtn.addEventListener('click', handleLogin);
            logoutBtn.addEventListener('click', handleLogout);
            
            sidebarItems.forEach(item => {
                item.addEventListener('click', () => {
                    sidebarItems.forEach(i => i.classList.remove('active'));
                    item.classList.add('active');
                    currentSection = item.getAttribute('data-section');
                    updateContent();
                });
            });

            uploadBtn.addEventListener('click', () => {
                uploadModal.style.display = 'flex';
            });

            closeModal.addEventListener('click', () => {
                uploadModal.style.display = 'none';
            });

            cancelUpload.addEventListener('click', () => {
                uploadModal.style.display = 'none';
            });

            fileInput.addEventListener('change', () => {
                confirmUpload.disabled = !fileInput.files.length;
            });

            confirmUpload.addEventListener('click', handleUpload);
        }

        // Handle user login
        function handleLogin() {
            const username = usernameInput.value.trim();
            if (username) {
                currentUser = username;
                localStorage.setItem('currentUser', username);
                showApp();
            } else {
                alert('Please enter a username');
            }
        }

        // Handle user logout
        function handleLogout() {
            currentUser = '';
            localStorage.removeItem('currentUser');
            loginPage.style.display = 'flex';
            appContainer.style.display = 'none';
        }

        // Show the main app interface
        function showApp() {
            userAvatar.textContent = currentUser.charAt(0).toUpperCase();
            userName.textContent = currentUser;
            loginPage.style.display = 'none';
            appContainer.style.display = 'block';
            updateContent();
        }

        // Update content based on current section
        function updateContent() {
            if (currentSection === 'photos') {
                sectionTitle.textContent = 'My Photos';
                renderPhotos(uploadedPhotos);
            } else if (currentSection === 'recycle') {
                sectionTitle.textContent = 'Recycle Bin';
                renderPhotos(deletedPhotos, true);
            }
        }

        // Render photos in the grid
        function renderPhotos(photos, isRecycleBin = false) {
            photosContainer.innerHTML = '';
            
            if (photos.length === 0) {
                photosContainer.innerHTML = `
                    <div class="empty-state">
                        <i class="fas fa-${isRecycleBin ? 'trash' : 'images'}"></i>
                        <h3>No ${isRecycleBin ? 'deleted' : 'uploaded'} photos</h3>
                        <p>${isRecycleBin ? 'Photos you delete will appear here' : 'Upload your first photo to get started'}</p>
                    </div>
                `;
                return;
            }
            
            // Filter photos by current user if in main section
            const userPhotos = isRecycleBin ? 
                photos : 
                photos.filter(photo => photo.uploadedBy === currentUser);
                
            if (userPhotos.length === 0 && !isRecycleBin) {
                photosContainer.innerHTML = `
                    <div class="empty-state">
                        <i class="fas fa-images"></i>
                        <h3>No photos uploaded yet</h3>
                        <p>Upload your first photo to get started</p>
                    </div>
                `;
                return;
            }
            
            userPhotos.forEach(photo => {
                const photoCard = document.createElement('div');
                photoCard.className = 'photo-card';
                
                photoCard.innerHTML = `
                    <div class="photo-thumbnail">
                        <img src="${photo.url}" alt="${photo.name}">
                    </div>
                    <div class="photo-info">
                        <div class="photo-name">${photo.name}</div>
                        <div class="photo-meta">
                            <span>${formatFileSize(photo.size)}</span>
                            <span>${photo.uploadedBy}</span>
                        </div>
                    </div>
                    <div class="photo-actions">
                        <button class="action-btn download-btn">
                            <i class="fas fa-download"></i> Download
                        </button>
                        <button class="action-btn ${isRecycleBin ? 'restore-btn' : 'delete-btn'}">
                            <i class="fas fa-${isRecycleBin ? 'trash-restore' : 'trash'}"></i> 
                            ${isRecycleBin ? 'Restore' : 'Delete'}
                        </button>
                    </div>
                `;
                
                // Add event listeners
                const downloadBtn = photoCard.querySelector('.download-btn');
                const actionBtn = photoCard.querySelector(isRecycleBin ? '.restore-btn' : '.delete-btn');
                
                downloadBtn.addEventListener('click', () => {
                    downloadPhoto(photo);
                });
                
                actionBtn.addEventListener('click', () => {
                    if (isRecycleBin) {
                        restorePhoto(photo);
                    } else {
                        deletePhoto(photo);
                    }
                });
                
                photosContainer.appendChild(photoCard);
            });
        }

        // Handle file upload
        function handleUpload() {
            const file = fileInput.files[0];
            if (!file || !file.type.startsWith('image/')) {
                alert('Please select a valid image file');
                return;
            }
            
            const reader = new FileReader();
            reader.onload = function(e) {
                const newPhoto = {
                    id: Date.now(),
                    name: file.name,
                    size: file.size,
                    type: file.type,
                    url: e.target.result,
                    uploadedBy: currentUser,
                    uploadedAt: new Date().toISOString()
                };
                
                uploadedPhotos.push(newPhoto);
                localStorage.setItem('uploadedPhotos', JSON.stringify(uploadedPhotos));
                
                uploadModal.style.display = 'none';
                fileInput.value = '';
                confirmUpload.disabled = true;
                
                if (currentSection === 'photos') {
                    updateContent();
                }
            };
            reader.readAsDataURL(file);
        }

        // Delete a photo
        function deletePhoto(photo) {
            if (confirm('Are you sure you want to delete this photo?')) {
                // Remove from uploaded photos
                uploadedPhotos = uploadedPhotos.filter(p => p.id !== photo.id);
                localStorage.setItem('uploadedPhotos', JSON.stringify(uploadedPhotos));
                
                // Add to deleted photos
                deletedPhotos.push(photo);
                localStorage.setItem('deletedPhotos', JSON.stringify(deletedPhotos));
                
                updateContent();
            }
        }

        // Restore a photo from recycle bin
        function restorePhoto(photo) {
            // Remove from deleted photos
            deletedPhotos = deletedPhotos.filter(p => p.id !== photo.id);
            localStorage.setItem('deletedPhotos', JSON.stringify(deletedPhotos));
            
            // Add back to uploaded photos
            uploadedPhotos.push(photo);
            localStorage.setItem('uploadedPhotos', JSON.stringify(uploadedPhotos));
            
            updateContent();
        }

        // Download a photo
        function downloadPhoto(photo) {
            const a = document.createElement('a');
            a.href = photo.url;
            a.download = photo.name;
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
        }

        // Format file size to human readable format
        function formatFileSize(bytes) {
            if (bytes === 0) return '0 Bytes';
            const k = 1024;
            const sizes = ['Bytes', 'KB', 'MB', 'GB'];
            const i = Math.floor(Math.log(bytes) / Math.log(k));
            return parseFloat((bytes / Math.pow(k, i)).toFixed(2)) + ' ' + sizes[i];
        }

        // Initialize the app when DOM is loaded
        document.addEventListener('DOMContentLoaded', initApp);
    </script>
</body>
</html>
