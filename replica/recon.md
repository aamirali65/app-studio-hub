# Trello Recon Map

## Overview
- **App Name**: Trello
- **Platform**: Android (Google Play Store)
- **URL**: [https://play.google.com/store/apps/details?id=com.trello](https://play.google.com/store/apps/details?id=com.trello)

## Sources
| Source                     | What It Gives You                                                                 |
|------------------------------|-------------------------------------------------------------------------------------|
| App Store Listing            | Screenshots, app description, and key features.                                    |
| Help Center / Docs           | Detailed feature list and settings.                                               |
| Pricing Page                | Which features are premium (e.g., AI summaries, automation).                      |
| Public Walkthrough Videos    | Real user flows (e.g., creating a board, adding tasks).                            |
| User's Own Account          | Personal boards, tasks, and workflows (if accessible).                             |

## Screen Inventory
| ID  | Screen               | Route / How to Get There       | Purpose                                                                 | Key Components                                                                 | States Seen                                                                 |
|-----|----------------------|-------------------------------|-------------------------------------------------------------------------|-----------------------------------------------------------------------------|-----------------------------------------------------------------------------|
| S01 | Home Screen          | App launch                          | Main dashboard with boards and tasks.                                           | Board list, quick add button, notifications.                                    | Empty, loading, filled, error.                                                |
| S02 | Board View           | Tap on a board from home screen. | Displays tasks in lists (e.g., To Do, In Progress).                             | Lists, cards, add card button, filters.                                       | Empty, loading, filled, error.                                                |
| S03 | Card View            | Tap on a card from a board.      | Detailed task view with checklists, comments, and attachments.                | Title, description, checklist, comments, attachments.                           | Empty, loading, filled, error.                                                |
| S04 | Planner              | Tap on "Planner" tab.            | Daily schedule with tasks and calendar integration.                             | Calendar view, task list, focus time.                                          | Empty, loading, filled, error.                                                |
| S05 | Inbox                | Tap on "Inbox" tab.              | Captured tasks from emails, messages, and other apps.                          | Inbox list, save button, forward button.                                      | Empty, loading, filled, error.                                                |

## User Flows
1. **Create a Board**
   - S01 (Home Screen) → S02 (Board View)
   - Edge Cases: No internet, duplicate board name.

2. **Add a Task**
   - S02 (Board View) → S03 (Card View)
   - Edge Cases: Empty task name, invalid due date.

3. **Schedule a Task**
   - S03 (Card View) → S04 (Planner)
   - Edge Cases: Calendar sync failure, conflicting time slots.

## Components
- **Buttons**: Add card, save, forward, quick add.
- **Inputs**: Card title, description, checklist items.
- **Modals**: Add board, add task, due date picker.
- **Tables**: Board lists, task checklists.

## Inferred Data Model
```
Board  id, name, created_at, user_id
       evidence: S01 (Home Screen), S02 (Board View)
       confidence: high

Card   id, board_id, title, description, due_date, status (To Do | In Progress | Done)
       evidence: S02 (Board View), S03 (Card View)
       confidence: high

User   id, email, name
       evidence: S01 (Home Screen)
       confidence: high
```

## Feature Matrix
| Feature               | Area          | Priority | Original | Clone | Notes                                                                 |
|-----------------------|---------------|----------|----------|-------|-----------------------------------------------------------------------|
| Boards                | Core          | Must     | Yes      | No    |                                                                       |
| Cards                 | Core          | Must     | Yes      | No    |                                                                       |
| Planner               | Core          | Should   | Yes      | No    |                                                                       |
| Inbox                 | Core          | Could    | Yes      | No    |                                                                       |
| Calendar Integration | Integration   | Should   | Yes      | No    |                                                                       |
| AI Summaries          | AI            | Could    | Yes      | No    | Requires paid subscription.                                            |

## Out-of-Scope Items
| Item                     | Reason                                                                 |
|--------------------------|-----------------------------------------------------------------------|
| Licensed Content        | Trello's catalog of templates and backgrounds.                          |
| Network and Users       | Trello's social features (e.g., sharing boards with others).            |

## Size Estimation
- **Screens**: 5 (S01-S05)
- **Flows**: 3 (Create a Board, Add a Task, Schedule a Task)
- **Entities**: 3 (Board, Card, User)
- **Hard Parts**: Calendar integration, AI summaries (requires paid subscription).
- **Size**: M (2-4 weeks)

## Next Step
- Proceed to `/replica-architect` to plan the stack and database schema.
