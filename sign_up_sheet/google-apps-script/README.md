# Google Sheets backend for the potluck sign-up sheet

This folder contains the Google Apps Script backend for `../sign_up_sheet.html`.

## Setup

1. Create a new Google Sheet.
1. In the sheet, choose **Extensions > Apps Script**.
1. Replace the default `Code.gs` content with the contents of `Code.gs` from this folder.
1. In Apps Script, select the `setup` function and run it once.
1. Approve the permissions prompt.
1. Confirm the Google Sheet now has these tabs:
   - `Settings`
   - `Categories`
   - `Signups`
1. In Apps Script, choose **Deploy > New deployment**.
1. Select **Web app**.
1. Use these deployment settings:
   - **Execute as:** Me
   - **Who has access:** Anyone
1. Copy the Web app URL ending in `/exec`.
1. Open `../sign_up_sheet.html` and paste that URL into:

   ```js
   const SHARED_BACKEND_URL = "PASTE_YOUR_APPS_SCRIPT_WEB_APP_EXEC_URL_HERE";
   ```

1. Publish/upload the updated `sign_up_sheet.html` to GitHub Pages.

## How customization works in shared mode

When `SHARED_BACKEND_URL` is set, the page loads shared data from the Google Sheet.

Edit the Google Sheet directly:

- `Settings` tab controls title, note, date, location, organizer email, and optional hero image URL.
- `Categories` tab controls category ID, display name, needed count, icon, and whether the category is active.
- `Signups` tab stores submitted sign-ups, including private email and phone details.

The public page intentionally displays only name and item. Email and phone stay private in the Google Sheet.

## Category limits

The Apps Script uses `LockService` before saving a signup. That means if two people submit at nearly the same time for the last slot, only one should get the slot and the other will receive a full-category message.
