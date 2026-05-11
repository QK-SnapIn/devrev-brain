---
title: "DevRev Computer Client – Critical User Journeys"
type: flow
status: draft
sources: [raw/exports/DevRev Computer Client – Critical User Journeys.md, https://support.devrev.ai/en-US/devrev/directories]
related: ["features/identity", "features/conversations", "features/chats"]
last_updated: 2026-05-11
support_articles: [ART-23982]
---

# DevRev Computer Client – Critical User Journeys

## Goal
Validate the 6 core user journeys of the DevRev desktop/web client across all supported platforms (Windows, macOS, browser, mobile), ensuring stability, performance, and cross-platform consistency.

## Preconditions
- DevRev desktop client installed on target platform (Windows/macOS) or browser access available
- Valid user credentials with workspace access
- Network connectivity to DevRev services
- [gap] Minimum supported OS versions not specified

## Core Journeys

| Flow | Journey |
| --- | --- |
| Application Startup | Launch client |
| Authentication Flow | Login > Validate user > Load modules |
| Messaging Workflow | Start conversation > Send message > Receive message |
| Notification Flow | Event triggered > Desktop notification delivered |
| Client Stability | Continuous usage without crash |
| Session Management | Logout > Login > Resume session |

## Test Scenarios (15)

### 1. Application Launch Across Platforms
- **Description:** User launches the DevRev computer client on Windows/macOS/Browser/Mobile
- **Modules:** Desktop Client, System Integration
- **Severity:** Critical
- **Expected Result:** Application should launch successfully on all supported platforms without crashes or delays

### 2. User Login & Workspace Access
- **Description:** User logs into DevRev computer client and accesses workspace
- **Modules:** Authentication, Desktop Client
- **Severity:** Critical
- **Expected Result:** User should authenticate successfully and workspace should load with correct permissions

### 3. Workspace Navigation
- **Description:** User navigates between modules (tickets, conversations, analytics)
- **Modules:** Navigation, UI Framework
- **Severity:** High
- **Expected Result:** Navigation should be smooth and UI should render correctly across platforms

### 4. Start New Conversation
- **Description:** User initiates a new chat or support conversation
- **Modules:** Messaging / Chat
- **Severity:** Critical
- **Expected Result:** Conversation should start instantly and appear in conversation list

### 5. Send & Receive Messages
- **Description:** User sends and receives messages in a conversation
- **Modules:** Messaging / Chat
- **Severity:** Critical
- **Expected Result:** Messages should deliver in real time and sync correctly

### 6. Open Existing Conversation
- **Description:** User opens previously created conversations
- **Modules:** Messaging / Chat
- **Severity:** High
- **Expected Result:** Conversation history should load accurately

### 7. Chat History Retrieval
- **Description:** User scrolls and views older messages
- **Modules:** Messaging / Chat
- **Severity:** High
- **Expected Result:** Messages should load correctly with proper timestamps

### 8. Notification Handling
- **Description:** Desktop client receives notifications for messages, tickets, or incidents
- **Modules:** Notifications
- **Severity:** Critical
- **Expected Result:** Notifications should trigger correctly across operating systems

### 9. Integration Interaction
- **Description:** Desktop client interacts with integrated services (Slack, Jira, etc.)
- **Modules:** Integrations
- **Severity:** High
- **Expected Result:** Integration events should sync correctly without failures

### 10. Keyboard Shortcuts Execution
- **Description:** User performs actions through configured shortcuts
- **Modules:** Desktop Client, Settings
- **Severity:** Medium
- **Expected Result:** Shortcuts should work consistently across platforms

### 11. Cache Management
- **Description:** User clears application cache for troubleshooting
- **Modules:** Desktop Client, System Settings
- **Severity:** Medium
- **Expected Result:** Cache should clear without impacting application stability

### 12. Session Persistence
- **Description:** User logs out and logs back in or resumes previous session
- **Modules:** Authentication, Session Management
- **Severity:** High
- **Expected Result:** User session should restore correctly

### 13. Client Stability During Operations
- **Description:** Client remains stable during heavy usage or multitasking
- **Modules:** Desktop Client, Performance
- **Severity:** Critical
- **Expected Result:** No crashes, freezes, or data loss

### 14. Cross-Platform UI Consistency
- **Description:** UI layout behaves consistently across Windows/macOS
- **Modules:** UI Framework
- **Severity:** High
- **Expected Result:** UI components should render correctly on all supported platforms

### 15. Application Update & Restart
- **Description:** Client updates and restarts without data loss
- **Modules:** Desktop Client, Updater
- **Severity:** High
- **Expected Result:** Update process should complete successfully

## Success criteria
All 15 scenarios pass on every supported platform without crashes, data loss, or UI rendering issues.

## Failure modes
- Application fails to launch on a specific platform
- Authentication hangs or returns incorrect permissions
- Messages fail to deliver or arrive out of order
- Notifications do not trigger on certain OS versions
- Client crashes under heavy usage or multitasking
- Session state lost after logout/login cycle
- UI elements misaligned or unreadable on specific platforms

## Locators touched
[gap] No locator pages exist yet for the desktop client UI.

## API calls involved
[gap] API endpoints for authentication, messaging, and notifications not yet documented.

## Support documentation

Referenced DevRev support articles synchronized from [support.devrev.ai](https://support.devrev.ai/en-US/devrev/directories):

- [[support-articles/computer-by-devrev/computer|Computer]] (ART-23982) — [external](https://support.devrev.ai/en-US/devrev/article/dI2w0Ngb)
