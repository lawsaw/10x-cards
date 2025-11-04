# Product Requirements Document (PRD) - 10xCards Flashcard Assistant

## 1. Product Overview

### 1.1 Goal
Deliver a web-based flashcard creation and review tool that lets students rapidly generate accurate question-answer cards using AI while retaining control over final content. The MVP emphasises speed, quality oversight, and seamless integration with an existing spaced repetition engine.

### 1.2 Target Users
- Primary: Students aged 18–30 studying university subjects or languages who already rely on flashcards but struggle to keep pace with manual creation.
- Secondary: Lifelong learners experimenting with spaced repetition who need an accessible on-ramp without advanced configuration.

### 1.3 Value Proposition
- Reduce time spent drafting flashcards by providing AI-generated suggestions sourced from pasted study text.
- Maintain user trust by enforcing preview, selective saving, and easy editing of AI outputs.
- Encourage sustained study habits via a built-in spaced repetition schedule leveraging a proven open-source algorithm.

### 1.4 Operating Constraints
- One developer and one designer share implementation, each ~20 hours per week, targeting launch in 3–4 weeks.
- Desktop-first responsive web experience must also perform on mobile browsers without native app support.
- AI input limited to plain text up to 2000 characters, with no rich formatting or media ingestion.

## 2. User Problem

Manual flashcard creation is slow and repetitive, deterring students from keeping decks current and limiting the effectiveness of spaced repetition learning. Learners want AI help to accelerate drafting but need assurances that generated content is accurate, editable, and saved securely. Existing tools with advanced algorithms require heavy setup or lack intuitive feedback loops, leaving students to choose between control and efficiency. The MVP addresses the friction by combining fast AI generation, streamlined editing, and automated scheduling, ensuring user ownership of final card content.

## 3. Functional Requirements

### 3.1 AI Flashcard Generation
- Provide a single plain-text input up to 2000 characters, displaying live character count and preventing overflow.
- Trigger AI generation only when the input is non-empty and within limits, with clear loading states.
- Return a list of draft question-answer cards, each labelled with source order and editable fields.
- Surface error handling for network or AI failures with retry guidance.

### 3.2 Card Review and Selection
- Present a preview screen where users can inspect each generated card before saving.
- Allow users to accept or discard cards individually and to accept all remaining cards at once.
- Support inline editing of questions and answers prior to saving, with instant field validation.
- Enable thumbs-up or thumbs-down feedback on each AI-generated card, storing the response alongside metadata.

### 3.3 Manual Card Management
- Provide inline controls to add new manual cards within the same list view as generated cards.
- Allow editing, deletion, and duplication of any saved card from the user’s library.
- Persist edits immediately to prevent data loss on navigation or session timeout.

### 3.4 Spaced Repetition Integration
- Store cards with fields compatible with the selected open-source spaced repetition algorithm (question, answer, next review timestamp, performance history).
- Generate initial review schedules using algorithm defaults and update schedules after each review outcome.
- Display daily review queue with due cards ordered by urgency and allow marking cards complete for the session.

### 3.5 Authentication and Account Management
- Support email and password registration, login, logout, and password reset workflows.
- Securely store user credentials and flashcard data with encryption at rest and in transit.
- Provide an account deletion flow that erases all associated data to achieve basic GDPR compliance.

### 3.6 Feedback and Analytics
- Instrument events for AI generation requests, acceptance actions, edits, deletions, thumbs feedback, and review completions.
- Aggregate acceptance rate and AI usage metrics to track success criteria.
- Prepare data exports or dashboards for internal monitoring (scope limited to raw event logging for MVP).

### 3.7 Non-Functional Requirements
- Ensure responsive design across desktop, tablet, and mobile browsers with loading times under two seconds for core flows on 4G connections.
- Provide accessibility basics: keyboard navigation, sufficient contrast, and descriptive labels.
- Maintain observability through basic error logging and uptime monitoring.

## 4. Product Boundaries

### 4.1 In Scope
- Web application accessible via modern browsers on desktop and mobile.
- AI-assisted generation of question-answer flashcards from user-supplied plain text.
- Manual card creation, editing, deletion, and duplication.
- Integration with an existing spaced repetition algorithm using default parameters.
- Email-password authentication with GDPR-aligned data deletion.
- Event logging for AI usage and card lifecycle actions.

### 4.2 Out of Scope
- Custom spaced repetition algorithm development beyond configuration of the existing library.
- Import of documents or media beyond the 2000-character plain-text field.
- Sharing or collaboration across user accounts.
- Integrations with external learning management systems or calendar tools.
- Native mobile or desktop applications.
- Rich feedback mechanisms such as text comments or ratings beyond thumbs-up/down.

## 5. User Stories

### US-001 - Register with email and password
ID: US-001
Title: Register with email and password
Description: As a new student, I want to create an account using my email and a password so that my flashcards are stored securely.
Acceptance Criteria:
1. Given I provide a valid email and password, when I submit the form, then the system creates my account and logs me in.
2. Given I provide an invalid email format or weak password, when I submit, then I see inline validation explaining what to fix.
3. Given my email is already registered, when I submit, then I see an error instructing me to log in or reset my password.

### US-002 - Log in to existing account
ID: US-002
Title: Log in to existing account
Description: As a returning student, I want to log in with my email and password so that I can access my saved flashcards.
Acceptance Criteria:
1. Given I enter valid credentials, when I submit, then I am redirected to my dashboard with my decks loaded.
2. Given I enter incorrect credentials, when I submit, then I see an error without revealing whether the email exists.
3. Given I click forgot password, when I submit my email, then I receive reset instructions.

### US-003 - Log out securely
ID: US-003
Title: Log out securely
Description: As an authenticated user, I want to log out so that my account remains secure on shared devices.
Acceptance Criteria:
1. Given I am logged in, when I click log out, then my session ends and I return to the login page.
2. Given I log out, when I navigate back via browser controls, then I cannot access protected pages without logging in again.

### US-004 - Delete account and data
ID: US-004
Title: Delete account and data
Description: As a privacy-conscious user, I want to delete my account so that all my personal data is removed permanently.
Acceptance Criteria:
1. Given I confirm deletion, when I submit, then all flashcards, feedback, and analytics events tied to my account are removed.
2. Given my account is deleted, when I try to log in again, then the system requires new registration.
3. Given I cancel the deletion flow, when I return to the dashboard, then no data has been removed.

### US-005 - Paste study text for AI generation
ID: US-005
Title: Paste study text for AI generation
Description: As a user preparing cards, I want to paste up to 2000 characters of study text so that the AI can draft flashcards.
Acceptance Criteria:
1. Given I type or paste text, when I approach 2000 characters, then the interface shows a live counter.
2. Given I exceed 2000 characters, when I attempt to generate, then the system blocks submission and highlights the overflow.
3. Given the input is empty, when I click generate, then the button remains disabled until text is entered.

### US-006 - Generate AI flashcards
ID: US-006
Title: Generate AI flashcards
Description: As a user with study text, I want to generate draft question-answer flashcards so that I can quickly build a deck.
Acceptance Criteria:
1. Given I submit within limits, when generation starts, then I see a loading indicator and cannot trigger duplicate requests.
2. Given generation succeeds, when results return, then I see a list of draft cards with questions and answers populated.
3. Given generation fails, when an error occurs, then I see a message with retry guidance and no cards are saved automatically.

### US-007 - Preview and accept selected cards
ID: US-007
Title: Preview and accept selected cards
Description: As a user reviewing AI drafts, I want to choose which cards to save so that my deck only contains relevant content.
Acceptance Criteria:
1. Given draft cards are displayed, when I select accept on a card, then it is marked for saving and visually distinguished.
2. Given I click save selection, when cards are accepted, then only marked cards move into my saved library.
3. Given I choose accept all, when I confirm, then all current drafts are saved without re-running generation.

### US-008 - Provide AI quality feedback
ID: US-008
Title: Provide AI quality feedback
Description: As a user evaluating AI output, I want to mark cards with thumbs-up or thumbs-down so that the team can monitor quality.
Acceptance Criteria:
1. Given a draft card is shown, when I click thumbs-up or thumbs-down, then the choice is stored with the card record.
2. Given I change my mind before saving, when I toggle the feedback, then the latest value is recorded.
3. Given a card is saved, when I view it later, then the previous feedback remains associated for analytics.

### US-009 - Edit draft cards inline
ID: US-009
Title: Edit draft cards inline
Description: As a user reviewing AI drafts, I want to edit questions or answers before saving so that cards meet my standards.
Acceptance Criteria:
1. Given a draft card is visible, when I click into the question or answer, then the field becomes editable inline.
2. Given I enter changes, when I move focus away, then the edited text persists without explicit saving.
3. Given I revert my changes, when I undo or cancel, then the original AI text is restored for that card.

### US-010 - Edit saved cards inline
ID: US-010
Title: Edit saved cards inline
Description: As a user maintaining my deck, I want to adjust saved cards without leaving the list so that updates are quick.
Acceptance Criteria:
1. Given I view my saved cards, when I edit a question or answer, then the update persists immediately to storage.
2. Given I lose connectivity mid-edit, when I reconnect, then saved cards reflect only changes that were confirmed.
3. Given I edit a card, when I review it later, then the spaced repetition schedule adjusts only if content changes impact review history according to algorithm rules.

### US-011 - Add manual cards inline
ID: US-011
Title: Add manual cards inline
Description: As a user, I want to add new cards manually alongside AI drafts so that I can capture nuances the AI missed.
Acceptance Criteria:
1. Given I click add card, when a blank question and answer row appears, then I can fill it inline.
2. Given I complete both fields, when I save, then the manual card appears in the saved list with the same formatting as AI cards.
3. Given I leave required fields empty, when I attempt to save, then validation prevents submission until completed.

### US-012 - Delete cards from library
ID: US-012
Title: Delete cards from library
Description: As a user, I want to delete unwanted cards so that my deck stays relevant.
Acceptance Criteria:
1. Given I view a saved card, when I click delete, then I am asked to confirm before removal.
2. Given I confirm deletion, when the action completes, then the card is removed from my library and review queue.
3. Given I cancel deletion, when I return to the list, then the card remains unchanged.

### US-013 - Handle AI generation errors
ID: US-013
Title: Handle AI generation errors
Description: As a user, I want clear guidance when generation fails so that I know how to recover.
Acceptance Criteria:
1. Given the AI service returns an error, when it occurs, then I see a descriptive message indicating the issue.
2. Given an error occurs, when I click retry, then the system reuses my last input without losing edits.
3. Given repeated failures, when they exceed a threshold, then the interface offers manual creation as an alternative.

### US-014 - Review due cards with spaced repetition
ID: US-014
Title: Review due cards with spaced repetition
Description: As a learner, I want to review cards that are due today so that I stay on track with spaced repetition.
Acceptance Criteria:
1. Given I navigate to review mode, when due cards exist, then they appear one at a time with question-first display.
2. Given I reveal the answer, when I rate my recall, then my response feeds the algorithm to schedule the next review.
3. Given no cards are due, when I open review mode, then I see a message encouraging me to generate more cards or return later.

### US-015 - Update review schedule after feedback
ID: US-015
Title: Update review schedule after feedback
Description: As a learner, I want the system to reschedule cards automatically based on my recall rating so that effort is spaced optimally.
Acceptance Criteria:
1. Given I rate a card (eg. easy, good, hard), when I submit, then the next review date is recalculated by the algorithm.
2. Given I close review mode and reopen it, when the schedule updates, then cards show the new due dates without duplication.
3. Given I mark a card as forgotten repeatedly, when the algorithm adjusts, then future intervals shorten accordingly.

### US-016 - Track analytics events
ID: US-016
Title: Track analytics events
Description: As a product team member, I want key user actions instrumented so that we can measure AI adoption goals.
Acceptance Criteria:
1. Given a user triggers AI generation, when the request starts, then an AI_generate event records user ID and timestamp.
2. Given a user saves an AI-generated card, when it is stored, then an AI_accept event records card ID and feedback state.
3. Given a user edits or deletes a card, when the action occurs, then edit_card or delete_card events log the change with metadata.
4. Given a user completes a review session, when it ends, then a review_complete event captures counts of cards reviewed and outcomes.

### US-017 - Responsive web interface
ID: US-017
Title: Responsive web interface
Description: As a mobile browser user, I want the interface to adapt to smaller screens so that I can manage flashcards on the go.
Acceptance Criteria:
1. Given I open the app on a phone-sized viewport, when I navigate, then layouts reflow without horizontal scrolling.
2. Given I use touch input, when I interact with buttons or fields, then targets remain accessible and large enough for tapping.
3. Given I rotate the device, when orientation changes, then the interface adapts without losing state.

### US-018 - Maintain session integrity
ID: US-018
Title: Maintain session integrity
Description: As a security-conscious user, I want inactive sessions to expire so that my account is protected on shared devices.
Acceptance Criteria:
1. Given I remain inactive beyond the timeout threshold, when the threshold passes, then I am logged out and informed why.
2. Given I am logged out due to inactivity, when I log back in, then my unsaved draft cards saved locally are restored if available.
3. Given I actively interact with the app, when I perform actions, then the inactivity timer resets.

## 6. Success Metrics

### 6.1 Adoption and Quality
- 75 percent of AI-generated cards presented to users are accepted without deletion within 24 hours.
- 75 percent of all new cards in the first month are created via AI generation rather than manual entry.
- At least 60 percent of registered users complete one AI generation session and save cards in week one post-launch.

### 6.2 Engagement and Retention
- Median time from paste to first saved card is under two minutes.
- At least 50 percent of weekly active users complete a spaced repetition review session each week.
- Less than five percent of review sessions end due to system errors or instability.

### 6.3 Reliability and Satisfaction
- Uptime of 99 percent during the first quarter after launch.
- Fewer than ten percent of AI generations result in error states per week.
- Average thumbs-up ratio on AI cards exceeds 60 percent, indicating perceived usefulness.

