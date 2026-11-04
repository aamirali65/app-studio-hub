# Trello Clone Architecture Plan

## Overview
- **App Name**: Trello Clone
- **Platform**: Flutter (Android)
- **Stack**: Flutter, Dart, Riverpod, GoRouter, SQLite (Drift/Isar), Firebase Auth, Google Mobile Ads

---

## Step 1: The Stack

| Layer               | Technology Stack                                                                 |
|----------------------|----------------------------------------------------------------------------------|
| **Web App**         | Flutter (GoRouter, Riverpod)                                                     |
| **Styling**         | Material 3, Custom Design Tokens                                                  |
| **Database**        | SQLite (Drift/Isar) for offline-first support                                     |
| **ORM**             | Drift for SQL queries and migrations                                              |
| **Auth**            | Firebase Auth (Google, Email, Apple)                                             |
| **Payments**        | Google Play Billing (for in-app purchases)                                       |
| **Ads**             | Google Mobile Ads SDK                                                             |
| **Hosting**         | Firebase Hosting or GitHub Pages                                                   |
| **Analytics**       | Firebase Analytics                                                                |

**Why**: Flutter provides cross-platform support, while SQLite (Drift/Isar) ensures offline functionality. Firebase Auth and Google Mobile Ads are widely used and reliable.

---

## Step 2: The Schema

### Database Schema (SQLite)
```sql
-- Users table
CREATE TABLE users (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  name TEXT NOT NULL,
  email TEXT NOT NULL UNIQUE,
  created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP
);

-- Boards table
CREATE TABLE boards (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  name TEXT NOT NULL,
  user_id INTEGER NOT NULL,
  created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);

-- Cards table
CREATE TABLE cards (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  board_id INTEGER NOT NULL,
  title TEXT NOT NULL,
  description TEXT,
  due_date TIMESTAMP,
  status TEXT NOT NULL DEFAULT 'To Do',
  created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (board_id) REFERENCES boards(id) ON DELETE CASCADE
);

-- Checklists table
CREATE TABLE checklists (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  card_id INTEGER NOT NULL,
  title TEXT NOT NULL,
  FOREIGN KEY (card_id) REFERENCES cards(id) ON DELETE CASCADE
);

-- Checklist Items table
CREATE TABLE checklist_items (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  checklist_id INTEGER NOT NULL,
  title TEXT NOT NULL,
  completed BOOLEAN NOT NULL DEFAULT FALSE,
  FOREIGN KEY (checklist_id) REFERENCES checklists(id) ON DELETE CASCADE
);
```

### Indexes
```sql
CREATE INDEX idx_cards_board_id ON cards(board_id);
CREATE INDEX idx_checklists_card_id ON checklists(card_id);
CREATE INDEX idx_checklist_items_checklist_id ON checklist_items(checklist_id);
```

---

## Step 3: The API

### API Routes
| Method | Path               | What It Does                          | Who Can Call It | Input                          | Output                                                                 |
|--------|--------------------|--------------------------------------|------------------|---------------------------------|--------------------------------------------------------------------------|
| POST   | /api/boards          | Create a new board                  | Authenticated    | {name}                         | {id, name, user_id}                                                   |
| GET    | /api/boards          | List all boards                     | Authenticated    | -                               | [{id, name, user_id, created_at}]                                   |
| GET    | /api/boards/{id}     | Get a specific board               | Authenticated    | -                               | {id, name, user_id, created_at, cards: [...] }                       |
| POST   | /api/cards          | Create a new card                   | Authenticated    | {board_id, title, description}   | {id, board_id, title, description, status, created_at}                |
| GET    | /api/cards          | List all cards                      | Authenticated    | {board_id}                     | [{id, board_id, title, description, status, created_at}]              |

---

## Step 4: The Parts That Bite

1. **Time Zones**: Use the `intl` package to handle time zones and daylight saving.
2. **Offline Support**: Leverage SQLite (Drift/Isar) for offline-first functionality.
3. **Idempotency**: Ensure API endpoints handle duplicate requests gracefully.
4. **Rate Limits**: Implement rate limiting for API endpoints.
5. **GDPR Compliance**: Ensure user data can be deleted and encrypted.

---

## Step 5: Build Order

1. **Vertical Slice**: Sign up → Create a board → Add a card.
   - Screens: S01 (Home), S02 (Board View), S03 (Card View).
   - Tables: `users`, `boards`, `cards`.
   - Routes: `/api/boards`, `/api/cards`.

2. **Must-Haves**:
   - Boards (S01, S02).
   - Cards (S03).
   - Planner (S04).

3. **Should-Haves**:
   - Calendar Integration.
   - Inbox (S05).

4. **Could-Haves**:
   - AI Summaries (if feasible).

---

## Next Step
Proceed to `/replica-design` to rebuild the design system: colors, typography, spacing, and components.
