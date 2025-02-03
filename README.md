# Guide to Using Git Submodules for Next.js and Nest.js

Git Submodules allow you to manage multiple Git repositories within a single parent project. This is especially useful when integrating a frontend application (next-app) and a backend application (nest-app) in the same repository. Additionally, using Git Submodules makes it easier to set up CI/CD pipelines and Docker configurations.

## Table of Contents

- [Guide to Using Git Submodules for Next.js and Nest.js](#guide-to-using-git-submodules-for-nextjs-and-nestjs)
  - [Table of Contents](#table-of-contents)
  - [1. Create the Main Repository](#1-create-the-main-repository)
  - [2. Add Submodules](#2-add-submodules)
    - [Add Submodule for Next.js](#add-submodule-for-nextjs)
    - [Add Submodule for Nest.js](#add-submodule-for-nestjs)
  - [3. Clone the Project with Submodules](#3-clone-the-project-with-submodules)
  - [4. Update Submodules](#4-update-submodules)
  - [5. Remove Submodules](#5-remove-submodules)
  - [6. Example Directory Structure](#6-example-directory-structure)
  - [7. Deployment Instructions](#7-deployment-instructions)
    - [Running the Frontend Application (Next.js)](#running-the-frontend-application-nextjs)
    - [Running the Backend Application (Nest.js)](#running-the-backend-application-nestjs)
    - [Additional Submodule Commands](#additional-submodule-commands)
      - [Check Submodule Status](#check-submodule-status)
      - [Synchronize Submodules](#synchronize-submodules)
      - [Pull Changes for All Submodules](#pull-changes-for-all-submodules)
  - [8. Docker and CI/CD](#8-docker-and-cicd)
    - [Running the Docker Compose](#running-the-docker-compose)
    - [Docker Tips](#docker-tips)
  - [Conclusion](#conclusion)
  - [Star the Project ⭐](#star-the-project-)
  - [License](#license)

---

## 1. Create the Main Repository

1. Create a main repository on GitHub.
2. Clone the repository to your local machine:

   ```bash
   git clone <main-repo-url>
   cd <main-repo>
   ```

## 2. Add Submodules

### Add Submodule for Next.js

```bash
git submodule add <next-repo-url> frontend
```

### Add Submodule for Nest.js

```bash
git submodule add <nest-repo-url> backend
```

> **Note:** `frontend` and `backend` are the directories where the submodules will be cloned.

## 3. Clone the Project with Submodules

When cloning a repository with submodules, use the `--recurse-submodules` flag:

```bash
git clone --recurse-submodules <main-repo-url>
```

If you've already cloned the repository without submodules, run the following command:

```bash
git submodule update --init --recursive
```

## 4. Update Submodules

To update submodules when changes are made:

```bash
git submodule update --remote
```

## 5. Remove Submodules

1. Remove the submodule entry from `.git/config`:

   ```bash
   git submodule deinit -f frontend
   rm -rf .git/modules/frontend
   git rm -f frontend
   ```

2. Commit the changes:

   ```bash
   git commit -m "Remove submodule frontend"
   ```

## 6. Example Directory Structure

```
my-main-repo/
├── frontend/      # Next.js Submodule
├── backend/       # Nest.js Submodule
└── README.md
```

## 7. Deployment Instructions

### Running the Frontend Application (Next.js)

1. Navigate to the `frontend` directory:

   ```bash
   cd frontend
   ```

2. Install dependencies and run the application:

   ```bash
   npm install
   npm run dev
   ```

### Running the Backend Application (Nest.js)

1. Navigate to the `backend` directory:

   ```bash
   cd backend
   ```

2. Install dependencies and run the application:

   ```bash
   npm install
   npm run start:dev
   ```

### Additional Submodule Commands

#### Check Submodule Status

```bash
git submodule status
```

#### Synchronize Submodules

If the submodule structure has changed in the parent repository:

```bash
git submodule sync
```

#### Pull Changes for All Submodules

```bash
git submodule foreach git pull origin main
```

## 8. Docker and CI/CD

### Running the Docker Compose

1. Navigate to the `backend` directory.
2. Run the following command to start the services:

   ```bash
   docker-compose up --build
   ```

3. Access the Nest.js application at `http://localhost:3000`.

### Docker Tips

- To stop the containers:

  ```bash
  docker-compose down
  ```

- To clean up volumes:

  ```bash
  docker-compose down -v
  ```

- Check container logs:

  ```bash
  docker logs nest_app
  ```

## Conclusion

Git Submodules combined with Docker provide a robust solution for managing and deploying Next.js and Nest.js applications efficiently. This guide aims to help you set up and maintain your development environment seamlessly.

## Star the Project ⭐

If you find this project useful, feel free to give it a star! ⭐

Your support helps this project get more visibility and helps the community! Thank you!

## License

This project is licensed under the MIT License.
