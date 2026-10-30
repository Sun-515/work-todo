# Work Todo

A local-first task manager built with plain HTML, CSS, and JavaScript. No sign-in, backend database, API keys, or third-party runtime dependencies are required. The application interface is currently in Chinese, with a responsive layout for desktop and mobile browsers.

## Features

- Quickly add, edit, complete, and organize tasks.
- Set priorities, due dates, categories, notes, and stars.
- Break tasks into checkable subtasks.
- Filter by All, Pending, or Completed status.
- Browse tasks due today, due in the next seven days, overdue, or starred.
- Search task titles, notes, and categories.
- Sort by creation time, due date, priority, or title.
- View global task counts and completion progress.
- Select multiple tasks to complete, move to the recycle bin, or restore.
- Restore deleted tasks and undo the most recent supported action.
- Export and import JSON backups, or export a CSV spreadsheet.
- Switch between light and dark themes.
- Use keyboard shortcuts: **N** to create a task, **/** to search, and **Esc** to cancel editing.
- Synchronize changes between tabs on the same browser and site.
- Load task records created by the original version of this project.

## Run locally

Install Python 3, then run this command from the project root:

```sh
python3 -m http.server 5173 --bind 127.0.0.1 --directory dist
```

Open [http://127.0.0.1:5173](http://127.0.0.1:5173) in your browser.

Serve the project over HTTP rather than opening the HTML file directly, because the application uses JavaScript modules.

## Checks and tests

Node.js 20 or later is required. No dependency installation is needed.

```sh
npm run check
npm test
```

The regression tests cover legacy task compatibility, filtering, global statistics, date boundaries, sorting, backup merging, and CSV escaping. GitHub Actions runs syntax checks and regression tests on pushes and pull requests.

## Data storage and privacy

Tasks are stored in your browser's localStorage for the current site origin. The application does not send task records to a server and contains no analytics or OpenAI API calls.

Different domains, browsers, and devices have separate task records. Clearing browser data removes those records. Before changing domains or devices, export a JSON backup and import it at the new location.

### Backups

- **JSON** includes all task fields, subtasks, and recycle-bin records. Use it for complete backups.
- **CSV** includes active tasks and their main fields, but does not include subtasks or recycle-bin records.
- Importing a JSON backup merges tasks into existing data. Existing task IDs are skipped rather than overwritten.
- Import supports files up to 10 MB and up to 10,000 tasks per backup.

### Task rules

- Deleting a task moves it to the recycle bin; it can be restored.
- Pending counts and completion progress always use all tasks outside the recycle bin, regardless of the current filters.
- Today and overdue views use the device's local date.
- The next-seven-days view excludes today and includes the following seven calendar days.
- Completing subtasks does not automatically complete the parent task.

## Deploy

Publish the contents of the **dist/** directory to a static hosting service with HTTPS support. There is no build step and no server-side configuration or secret required.

Storing the project on GitHub does not automatically enable GitHub Pages or deploy the application.

## Project structure

| Path | Purpose |
| --- | --- |
| dist/index.html | Page structure and task editor |
| dist/styles.css | Responsive layout and themes |
| dist/app.mjs | User interactions, local storage, and file import/export |
| dist/core.mjs | Data validation, filtering, statistics, merging, and CSV export |
| tests/core.test.mjs | Regression tests |
| .github/workflows/check.yml | GitHub Actions checks |
| package.json | Run and test commands |

## Limitations

This project is intended for personal task management and learning. It does not provide account-based cross-device sync, team permissions, or background notifications.
