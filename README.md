EventController Documentation
Overview
The EventController is a Laravel controller that is part of a TV dashboard web application designed to manage events. It provides features for creating, editing, deleting, restoring, and managing events, as well as handling associated media files (images and videos). This controller ensures efficient event lifecycle management while incorporating features like logging and soft deletion.

Features
Event Management
List events with pagination.
Add new events with video and image uploads.
Edit event details and associated media.
Delete events (soft deletion) with the ability to restore or permanently delete.
Media Management
Upload and manage event-related images and videos.
Resize and optimize images for consistent formatting.
Activity Logging
Logs all critical actions (event creation, updates, deletion, and restoration) for accountability.
Soft Deletion
Deleted events are moved to an "EventTrash" model, allowing recovery before permanent deletion.
User-Friendly Views
Provides data for rendering user-friendly views, ensuring seamless interaction with the application.

Controller Methods
1. getEvent()
Fetches all active events and deleted (trashed) event counts. Passes this data to the event listing view.
2. addEvent()
Displays the form for adding a new event.
3. postAddEvent(Request $req)
Handles the creation of new events:
Saves event details, including name, description, and schedule.
Validates and uploads video files.
Resizes and uploads multiple images.
Logs the event creation activity.
4. deleteEvent($id)
Soft delete an event by moving it to the EventTrash model and logs the action.
5. deletedEvent()
Displays all soft-deleted events and related statistics.
6. restoreEvent(Request $req, $id)
Restores a soft-deleted event back to the active events list and logs the restoration.
7. permanentDelete($id)
Permanently deletes an event from the EventTrash model and logs the action.
8. getEditEvent($id)
Fetches the details of a specific event for editing, including associated images and videos.
9. postEditEvent(Request $req, $id)
Updates event details, uploads new media files (if provided), and removes old media as necessary. Logs the update activity.
10. getMedia()
Lists and paginates all uploaded images, displaying them in a media management view.

Models Used
Event: Represents active events.
EventTrash: Represents soft-deleted events.
Images: Stores paths for event-related images.
Videos: Stores links to event-related videos.
Log: Records user actions for accountability.
User: Provides user information for created/updated events.

Validation Rules
Videos: They must be in one of the following formats: mp4, ogx, oga, ogg, ogv, and webm.

Logging
Logs user actions, including:
Event creation.
Updates to event details or media.
Soft deletion and restoration.
Permanent deletion.

Soft Deletion Workflow
When an event is deleted, it is moved to the EventTrash model.
Soft-deleted events can be restored to active events.
If necessary, events in EventTrash can be permanently deleted.

Media Handling
Images
Uploaded images are resized to 1300x800 pixels.
Stored in the events/ directory with a unique filename.
Videos
Uploaded videos are stored in the videos/ directory.
Supports manual entry of up to three external video links.

Views
Event Listing: Displays active events and statistics on deleted events.
Add Event Form: Provides input fields for event details and file uploads.
Edit Event Form: Allows modification of event details and associated media.
Deleted Events: Lists soft-deleted events with restoration and permanent deletion options.
Media Management: Displays uploaded images with pagination.

Usage Notes
Ensure the storage and public/events/ directories have appropriate permissions for file uploads.
Install the Image package (e.g., Intervention Image) for resizing capabilities.
Use Laravel's authentication middleware to secure the controller methods.

Example Usage
Adding an Event
Navigate to the "Add Event" page.
Fill out the form with event details, including images and videos.
Submit the form to create the event.
Editing an Event
Navigate to the "Edit Event" page for the desired event.
Modify the details or upload new media files.
Save changes.
Deleting and Restoring Events
Soft delete an event from the event listing page.
Navigate to the "Deleted Events" page to view trashed events.
Restore or permanently delete events as needed.


Conclusion
The EventController simplifies event lifecycle management, providing robust features like soft deletion, media handling, and user activity logging. It is designed for scalability and user-friendly operation in a Laravel web application.

