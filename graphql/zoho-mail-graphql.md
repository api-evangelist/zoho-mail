# Zoho Mail GraphQL Schema

This document describes the conceptual GraphQL schema for the Zoho Mail API. Zoho Mail provides a comprehensive REST API for managing email accounts, folders, messages, contacts, calendars, tasks, and organizational settings. This schema represents a GraphQL interface over those capabilities.

## Overview

Zoho Mail is an ad-free, privacy-first email and collaboration platform. Its REST API exposes 15 modules: Organization, Domains, Groups, Users, Mail Policy, Accounts, Folders, Labels, Email Messages, Signatures, Threads, Tasks, Bookmarks, Notes, and Logs. Authentication uses OAuth 2.0 and responses are region-specific.

**Source Documentation:** https://www.zoho.com/mail/help/api/

## Schema Source

This GraphQL schema is a conceptual representation derived from the Zoho Mail REST API documentation. It models the resource types, relationships, and operations available through the Zoho Mail API surface.

## Types

The schema includes 60 named types covering all major Zoho Mail API domains:

### Account and Identity
- `Account` — top-level account container
- `EmailAccount` — individual email account within an organization
- `AccountDetails` — extended metadata for an email account
- `Alias` — email address alias for an account
- `SignatureInfo` — email signature configuration
- `APIKey` — API key credential
- `OAuthToken` — OAuth 2.0 token representation

### Folder Management
- `Folder` — generic mail folder
- `FolderType` — enumeration of folder types
- `InboxFolder` — inbox system folder
- `SentFolder` — sent items folder
- `TrashFolder` — trash/deleted items folder
- `SpamFolder` — spam/junk folder
- `CustomFolder` — user-created folder

### Email and Messaging
- `Email` — core email message
- `EmailDetails` — full email metadata and content
- `EmailBody` — email body content (plain text and HTML)
- `EmailHeader` — raw and parsed email headers
- `Sender` — message sender address
- `Recipient` — message recipient (To field)
- `CCField` — CC recipient
- `BCCField` — BCC recipient
- `ReplyTo` — reply-to address
- `Attachment` — email attachment metadata
- `AttachmentFile` — binary attachment file data
- `Draft` — unsent draft message
- `Thread` — email conversation thread
- `ThreadMessage` — individual message within a thread

### Labels and Organization
- `Label` — user-defined label
- `LabelTag` — label tag association

### Search and Filtering
- `SearchResult` — search result container
- `SearchCriteria` — search query parameters
- `Filter` — mail filter rule
- `FilterRule` — individual filter condition
- `FilterAction` — action taken when filter matches
- `ForwardRule` — email forwarding rule
- `AutoResponder` — automatic reply configuration
- `AutoReplySettings` — auto-reply schedule and content

### Contacts
- `Contact` — address book contact
- `ContactDetails` — extended contact information
- `ContactEmail` — email address for a contact
- `ContactPhone` — phone number for a contact
- `ContactGroup` — contact group/distribution list

### Calendar and Tasks
- `Calendar` — calendar container
- `CalendarEvent` — individual calendar event
- `CalendarReminder` — event reminder settings
- `Task` — task item
- `TaskList` — list of tasks

### Notes and Files
- `Note` — note item
- `FileAttachment` — file attachment metadata
- `StorageInfo` — storage quota and usage

### Domain and Organization Administration
- `DomainSettings` — email domain configuration
- `Organization` — organization-level container
- `OrganizationUser` — user within an organization

### Notifications
- `Webhook` — webhook subscription for event notifications

## Queries

- `account(accountId: ID!)` — fetch an email account by ID
- `accounts` — list all accessible email accounts
- `folder(accountId: ID!, folderId: ID!)` — fetch a folder
- `folders(accountId: ID!)` — list folders for an account
- `email(accountId: ID!, messageId: ID!)` — fetch a single email message
- `emails(accountId: ID!, folderId: ID!)` — list emails in a folder
- `thread(accountId: ID!, threadId: ID!)` — fetch a conversation thread
- `drafts(accountId: ID!)` — list draft messages
- `labels(accountId: ID!)` — list labels for an account
- `searchEmails(accountId: ID!, criteria: SearchCriteriaInput!)` — search emails
- `contacts(accountId: ID!)` — list contacts
- `contact(accountId: ID!, contactId: ID!)` — fetch a contact
- `calendar(accountId: ID!, calendarId: ID!)` — fetch a calendar
- `calendarEvents(accountId: ID!, calendarId: ID!)` — list calendar events
- `tasks(accountId: ID!)` — list tasks
- `notes(accountId: ID!)` — list notes
- `organization` — fetch organization settings
- `organizationUsers` — list organization users
- `domainSettings(domain: String!)` — fetch domain configuration
- `storageInfo(accountId: ID!)` — fetch storage quota info
- `filters(accountId: ID!)` — list mail filters
- `webhooks` — list webhook subscriptions

## Mutations

- `createEmail(accountId: ID!, input: EmailInput!)` — send an email
- `createDraft(accountId: ID!, input: DraftInput!)` — create a draft
- `updateDraft(accountId: ID!, draftId: ID!, input: DraftInput!)` — update a draft
- `deleteDraft(accountId: ID!, draftId: ID!)` — delete a draft
- `moveEmail(accountId: ID!, messageId: ID!, folderId: ID!)` — move email to folder
- `deleteEmail(accountId: ID!, messageId: ID!)` — delete an email
- `createFolder(accountId: ID!, input: FolderInput!)` — create a folder
- `updateFolder(accountId: ID!, folderId: ID!, input: FolderInput!)` — update a folder
- `deleteFolder(accountId: ID!, folderId: ID!)` — delete a folder
- `createLabel(accountId: ID!, input: LabelInput!)` — create a label
- `addLabelToEmail(accountId: ID!, messageId: ID!, labelId: ID!)` — apply label
- `createContact(accountId: ID!, input: ContactInput!)` — create a contact
- `updateContact(accountId: ID!, contactId: ID!, input: ContactInput!)` — update a contact
- `deleteContact(accountId: ID!, contactId: ID!)` — delete a contact
- `createCalendarEvent(accountId: ID!, calendarId: ID!, input: CalendarEventInput!)` — create event
- `updateCalendarEvent(accountId: ID!, eventId: ID!, input: CalendarEventInput!)` — update event
- `deleteCalendarEvent(accountId: ID!, eventId: ID!)` — delete event
- `createTask(accountId: ID!, input: TaskInput!)` — create a task
- `updateTask(accountId: ID!, taskId: ID!, input: TaskInput!)` — update a task
- `createNote(accountId: ID!, input: NoteInput!)` — create a note
- `createFilter(accountId: ID!, input: FilterInput!)` — create a mail filter
- `createWebhook(input: WebhookInput!)` — register a webhook
- `deleteWebhook(webhookId: ID!)` — delete a webhook
- `updateSignature(accountId: ID!, input: SignatureInput!)` — update signature
- `createAlias(accountId: ID!, input: AliasInput!)` — create an email alias
