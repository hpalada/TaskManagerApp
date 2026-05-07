# TaskMate — Android Task Manager

Android productivity app built in Java with SQLite — manage daily tasks, urgent tasks, and a personal journal, all with per-user data isolation through session management.

## Tech Stack

| Component | Technology |
|---|---|
| Language | Java |
| Platform | Android (API 26+) |
| Database | SQLite (via SQLiteOpenHelper) |
| UI | Material Design, RecyclerView, NavigationDrawer |
| Build | Gradle (Kotlin DSL) |

## Features

- **User authentication** — register, login, and persistent session management
- **Daily tasks** — create, update, and delete recurring daily tasks
- **Urgent tasks** — separate list for high-priority tasks with quick access
- **Journal / Notes** — personal diary entries tied to the logged-in user
- **Per-user data** — all records are scoped to the authenticated user via foreign keys
- **Navigation Drawer** — slide-out menu for moving between app sections
- **RecyclerView lists** — smooth scrolling task and note lists with adapters

## Database Schema

```sql
usuarios  (id, usuario, clave, correo)
tareas    (id, titulo, descripcion, tipo, usuario_id → usuarios.id)
diarias   (id, titulo, descripcion, usuario_id → usuarios.id)
journal   (id, titulo, descripcion, usuario_id → usuarios.id)
```

Foreign keys enforce that all tasks and notes belong to a valid user.

## Project Structure

```
app/
├── main/
│   ├── java/com/example/taskmateprueba/
│   │   ├── MainActivity.java        # Home screen with task list
│   │   ├── Login.java               # Authentication screen
│   │   ├── SesionManager.java       # Session persistence (SharedPreferences)
│   │   ├── AdminSQLiteOpen.java     # SQLite helper — schema + CRUD
│   │   ├── TaskModel.java           # Task data model
│   │   ├── AdaptadorTareas.java     # RecyclerView adapter for tasks
│   │   ├── NoteAdapter.java         # RecyclerView adapter for notes
│   │   ├── AgregarTarea.java        # Add task screen
│   │   ├── ActualizarTarea.java     # Edit task screen
│   │   ├── TareasDiarias.java       # Daily tasks screen
│   │   ├── TareasUrgentes.java      # Urgent tasks screen
│   │   ├── AgregarNota.java         # Add journal entry
│   │   ├── ActualizarNota.java      # Edit journal entry
│   │   └── Diario.java              # Journal screen
│   └── res/                         # Layouts, drawables, icons
└── build.gradle.kts
```

## Setup

1. Clone the repo and open in **Android Studio**
2. Let Gradle sync dependencies
3. Run on an emulator or physical device (API 26+)

No external dependencies or API keys required — fully self-contained with SQLite.

## Highlights

- Designed and implemented a normalized SQLite schema with foreign key constraints for data integrity
- Built user authentication and session persistence from scratch using SharedPreferences
- Implemented RecyclerView adapters with CRUD support for tasks and journal entries
- Used Material Design NavigationDrawer for intuitive section-based navigation
