## 🚀 Live Demo

👉 [Click here to view the live app](https://taskmanager-frontend-three.vercel.app/)

# 📋 Task Management Dashboard – Frontend

A modern and responsive task management dashboard designed for both individual productivity and team collaboration. This is the **frontend** built with modern React tooling and structured for scalability.

---

## 🚀 Features

### ✅ User Features
- **Dashboard:** View personal task metrics, deadlines, and overall progress.
- **Task Tracking:** View, filter, and manage tasks by priority, due dates, or status.
- **Automated Updates:** Task statuses update automatically based on checklist progress.
- **Attachments:** Add and access file links for each task.
- **Mobile Ready:** Seamless user experience across desktop, tablet, and mobile.

### 👨‍💼 Admin Features
- **Task Management:** Create and manage tasks, assign users, update priorities.
- **User Management:** Add, remove, and monitor user access and performance.
- **Download Reports:** Export task-related data for analysis (CSV/PDF planned).
- **Team Collaboration:** Assign tasks to multiple users and track their contributions.

---

## 🛠️ Tech Stack

- **Framework:** React (via Vite)
- **UI:** Tailwind CSS (or your preferred CSS system)
- **Routing:** React Router
- **State Management:** React Context API
- **Icons:** Heroicons / Lucide / React Icons
- **Authentication:** Custom auth logic (`useUserAuth`)

---


### 📁 Folder Structure
```bash

src/
├── assets/ # Static files like images/icons
├── components/ # Reusable UI components
│ ├── Cards/ # Task/stat cards
│ ├── Charts/ # Chart components for insights
│ ├── inputs/ # Input fields and form components
│ └── layout/ # Layout-specific components like modals, alerts
│ ├── AvatarGroup.jsx
│ ├── DeleteAlert.jsx
│ ├── Model.jsx
│ ├── Progress.jsx
│ ├── TaskListTable.jsx
│ └── TaskStatusTabs.jsx
├── context/ # Global state (e.g., user context)
│ └── userContext.jsx
├── hooks/ # Custom hooks
│ └── useUserAuth.jsx
├── pages/ # Route-based views
│ ├── Admin/
│ │ ├── CreateTask.jsx
│ │ ├── Dashboard.jsx
│ │ ├── ManageTask.jsx
│ │ └── ManageUsers.jsx
│ ├── Auth/
│ │ ├── Login.jsx
│ │ └── SignUp.jsx
│ └── User/
│ ├── MyTask.jsx
│ └── UserDashboard.jsx
└── App.jsx # Main app entry
```
---

## 📦 Getting Started

### 1. Clone the repository

````bash
git clone https://github.com/yourusername/task-dashboard-frontend.git
cd task-dashboard-frontend
````



### 2. Install dependencies

npm install
# or
yarn install


### 3. Run the app

npm run dev
# or
yarn dev


## ☁️ DevOps & Deployment

This frontend repo is part of a full GitOps deployment pipeline.

- Built by GitHub Actions in `.github/workflows/frontend-dev.yml` when code is pushed to `develop`.
- Docker image is built and pushed to Docker Hub as `trishank01/taskmanager-frontend:${{ github.sha }}`.
- Build args passed into the frontend image:
  - `VITE_API_URL`
  - `VITE_CLOUDINARY_CLOUD_NAME`
  - `VITE_CLOUDINARY_UPLOAD_PRESET`
- The workflow clones the separate manifest repo `task-manager-k8s` and updates `dev/frontend/deployment.yaml` with the new image tag.
- Argo CD watches that repo and syncs the `dev` and `prod` apps into the Kubernetes cluster.

### Docker & Kubernetes details

- `frontend/Dockerfile` uses a multi-stage build:
  - build stage with Node and Vite
  - runtime stage with `nginx:alpine`
- Final app is served by Nginx on port `80`.
- Kubernetes frontend manifest uses `containerPort: 80` and `imagePullPolicy: Always`.
- The deployed manifest path is `dev/frontend/deployment.yaml` in the manifest repo.

### Build-time secrets

- Sensitive values are injected at build time from GitHub Secrets, not hard-coded in the app.
- The frontend receives runtime configuration through Vite environment values.

### Why this matters

- The pipeline makes each deploy traceable by SHA-based image tags.
- Automatic manifest updates ensure Argo CD can deploy the exact image.
- This repo focuses on frontend build and packaging; the manifest repo owns deployment configuration.


### 📲 Responsive Design
Designed with mobile-first principles:

Fully responsive across desktop, tablet, and mobile devices

Scalable layout and typography

Touch-friendly UI for task management

### 🔐 Authentication
Basic auth system with:

Login & Signup pages (Auth/Login.jsx, Auth/SignUp.jsx)

Auth context (context/userContext.jsx)

Custom hook for auth logic (hooks/useUserAuth.jsx)

You can plug in your backend auth endpoints or Firebase integration.

### 📊 Pages Overview
Page	Path	Description
Admin Dashboard	/admin/dashboard	Overview of tasks and user metrics
Manage Tasks	/admin/manage-tasks	Create/update/delete/assign tasks
Manage Users	/admin/manage-users	View & control team members
User Dashboard	/user/dashboard	Personal view of tasks, progress, stats
My Tasks	/user/my-tasks	User’s detailed task list
Login	/login	Auth login screen
Signup	/signup	Auth registration screen

### 📥 Future Improvements
Task reminders & calendar integration

Notification system

Commenting & chat per task

Dark mode support

Drag-and-drop task reordering

### 🤝 Contributing
Pull requests are welcome. For significant changes, please open an issue first to discuss improvements or changes.
