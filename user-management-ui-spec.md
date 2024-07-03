# User Management Screen UI Specification

## Overview
This document outlines the user interface specifications for the User Management screen intended for administrative users to manage system access.

## Features
- Add, edit, and view users
- Filter out disabled users
- Filter and sort users by any column shown in the user list

## UI Components
### Header
- **Description:** Contains a new user button, an option to hide disabled users, and a save action button for the edit form.
- **Specifications:** Blue new user button with a plus icon, a checkbox for hiding disabled users, aligned to the left. Blue save user button aligned to the right; the button is only enabled if the open form is valid and not saved.

### User Table
- **Description:** Displays user information in columns: ID, User Name, Email, Enabled
- **Interactions:** On each column header, clickable arrow icons for sorting, clickable filter icon for filtering. Each row is clickable.
- **Specifications:**
- - **Columns:** There are a total of four columns: ID, User Name, Email, and Enabled, which are mapped respectively to the user fields ID, Display Name, Email, and Enabled.
- - **Headers:** Blue background, white foreground color. For each column, the header contains the column name, sort button as arrows, and a filter button. If the table is sorted, only the arrow indicating the sort direction is shown; otherwise, both up and down arrows are shown.
- - **Rows:** White background, black foreground color. Focused row's background is light blue. For each column, the field only contains the value of that field as text. On click,

### User Form
- **Description:** Displays the user form for adding a new user or updating an existing user.
- **Interactions:** Each form field has an interactive area to edit the value.
- **Specifications:** The form contains a title at the top which is either "New User" to indicate adding a new user or "Edit User" to indicate updating an existing user. If the form is opened by editing the user, each field should be pre-filled by the existing user's data. There are 6 rows in the form, each indicating only one field of the user. A row contains the field name and the editable value field. Both field names and values on each row are vertically aligned, and the field name texts are aligned to the left. The save/submit functionality is done with the save button in the header. On each user interaction, the save button's enabled status should be updated according to the form's validity. The form should contain these fields:
- - **Username:** One line text editing field. Mandatory.
- - **Display Name:** One line text editing field. Mandatory.
- - **Phone:** One line text editing field with a phone number formatter. Mandatory, a valid phone string is required.
- - **Email:** One line text editing field. Mandatory, a valid email string is required.
- - **User Roles:** Select/dropdown field that supports multiple selections. Available values are "Guest", "Admin," and "SuperAdmin." At least one selection is required.
- - **Enabled:** Simple checkbox field, the user is enabled if checked.

## Behavior and Interactivity
### Header
#### New User Button
- **Action:** Clears all fields in the form to enter new user details. If the current form has unsaved changes, a confirmation dialog is shown.

#### Hide Disabled User Checkbox
- **Action:** Toggles between 2 states; true and false. Updates the user table on value changed. If the new value is true, only show the enabled users; otherwise, show all users.

#### Save User Button
- **Action:** If enabled, creates a new user or updates the existing user's details according to the user form when clicked. If disabled, shows a message that indicates why the button is disabled (form is not valid/nothing changed).
- **Interactivity Status:** Enabled only if the form is valid and something has changed.

### User Table
#### Sort Button on Header
- **Action:** Toggles between 3 states; asc, desc, and not sorted. Updates the user table on value changed. If the new state is asc, sorts the user list in ascending order of that field; if desc, sorts the user list in descending order of that field; if not sorted, doesn't sort the user on that field.

#### Filter Button on Header
- **Action:** Opens a filter dialog to apply a filter on the user table.

#### Each Row on Table
- **Action:** Similar to the new user button, but fills the form with the selected user's details. Also, the form title is changed to edit user, and the save user button now updates this user's details.

### User Form
#### All Fields
- **Action:** On each update, updates the save user button's interactivity according to the form's validity.

## Initial State
- **Default Values:** Hide disabled user checkbox is checked. The default order of the user table is ordered by ascending ID. The form is initially a New User form with all fields empty. The Save User button is disabled.
- **On Load:** The user table is populated with data fetched from the server on each update, displayed with a spinner during loading.

## Error Handling
- **API Failure:** Displays an error message for each API call error. The error message is received from the API call response.