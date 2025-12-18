# 🚀 Gogarow

> **Bridging the gap between "Homework Set" and "Homework Done."**

![Status](https://img.shields.io/badge/Status-In%20Development-orange) ![License](https://img.shields.io/badge/License-MIT-blue)

**Gogarow** is a lightweight Learning Management System (LMS) focused on student accountability and the home-school connection. It provides a seamless interface for Teachers and Parents to assign work, and a flexible "Proof of Work" engine for Students to submit assignments via file upload, screenshot, or rich text.

---

## 📖 Table of Contents
- [The Problem](#-the-problem)
- [Key Features](#-key-features)
- [System Architecture](#-system-architecture)
- [Tech Stack](#-tech-stack)
- [Database Schema](#-database-schema)
- [Getting Started](#-getting-started)
- [Roadmap](#-roadmap)

---

## 🧐 The Problem

Most homework tools focus on *setting* the task. Gogarow focuses on the **submission and verification** loop. 

Parents often struggle to track if homework is actually finished. Teachers struggle to get assignments back in a consistent format. Gogarow solves this by:
1.  **Centralized Dashboard:** Real-time status tracking (Pending, Submitted, Verified, Redo).
2.  **Flexible Submissions:** Kids can drag-and-drop files or paste screenshots directly from their clipboard (e.g., proving they finished a quiz on an external site).
3.  **Data Safety:** A robust file handling system that prevents accidental data loss.

---

## ✨ Key Features

### 👨‍👩‍👧 Roles & Permissions
* **Parents/Teachers:** Create tasks, set due dates, review submissions, and mark work as "Verified" or "Redo."
* **Students:** A distraction-free, gamified dashboard to view pending tasks and upload work.

### 📤 Hybrid Submission Engine
Students have two ways to prove their work:
1.  **File Upload:** Drag-and-drop support for PDFs, Word Docs, and Images. Handles multiple file uploads simultaneously (Batch Uploads).
2.  **The "Scratchpad":** A rich-text editor that allows students to type answers or **paste screenshots directly from their clipboard**.

### 🛡️ Smart File Handling (Safety System)
* **Reference-Based Storage:** The database stores file paths (pointers), not heavy binary blobs, keeping the app fast.
* **Soft Deletes:** When a user deletes a file, the system marks it as "archived" in the database rather than destroying the data immediately. This allows for recovery if a child accidentally deletes their homework.

---

## 🏗️ System Architecture

Gogarow separates file storage from data management to ensure performance and scalability.

1.  **File Store (The "Shelf"):** Physical files are stored in a dedicated environment (e.g., AWS S3 bucket or Local Server `uploads/` directory).
2.  **Database (The "Catalog"):** Stores metadata (File URL, Uploader ID, Task ID) and links it to the submission.
3.  **The Soft Delete Workflow:**
    * User clicks "Delete" -> Database updates `deleted_at` timestamp -> File remains in storage for 30 days before permanent cleanup.

---

## 🛠️ Tech Stack

*(Update these with your final choices)*

* **Frontend:** React.js / Vue.js
* **Backend:** Node.js (Express)
* **Database:** PostgreSQL
* **File Storage:** AWS S3 / Local Storage
* **Authentication:** JWT / Firebase Auth

---

## 💾 Database Schema Concept

**`Users`**
- `id`, `name`, `role` (parent/student/teacher), `password_hash`

**`Tasks`**
- `id`, `assigned_by`, `assigned_to`, `title`, `description`, `due_date`, `status` (pending/submitted/verified)

**`Submissions`**
- `id`, `task_id`, `student_id`, `notes` (text content), `submitted_at`

**`Attachments`**
- `id`, `submission_id`, `file_url`, `file_type`, `created_at`, `deleted_at` (for soft deletes)

---

## 🚀 Getting Started

To run this project locally:

1.  **Clone the repo**
    ```bash
    git clone [https://github.com/yourusername/gogarow.git](https://github.com/yourusername/gogarow.git)
    ```

2.  **Install Dependencies**
    ```bash
    cd gogarow
    npm install
    ```

3.  **Setup Environment Variables**
    Create a `.env` file in the root directory:
    ```env
    PORT=3000
    DB_HOST=localhost
    DB_USER=root
    DB_PASS=password
    STORAGE_BUCKET=my-gogarow-bucket
    ```

4.  **Run the App**
    ```bash
    npm run dev
    ```

---

## 🔮 Future Roadmap

- [ ] **Streak System:** Gamification to reward consistent on-time submissions.
- [ ] **Teacher Portal:** Allow teachers to bulk-assign homework via Class Code.
- [ ] **Mobile App:** Native mobile notifications for parents ("Your child just submitted homework!").

---

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
