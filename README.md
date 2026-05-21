# 📅 Add to Calendar — Eloqua Email Generator
A lightweight, single-file HTML tool for generating Eloqua-safe "Add to Calendar" button code for email campaigns. Fill in your event details, pick a style, and copy the ready-to-paste HTML — no build step, no dependencies, no server required.

## Features

Live preview — see your button rendered on a white email background as you type
All major calendar providers — generates links for Google Calendar, Outlook.com, Apple / iCal (.ics), and Yahoo Calendar
Eloqua-safe HTML — table-based layout with MSO conditional comments for Outlook on Windows
Full email output — optionally generate a complete email template wrapper around your button
Color customization — pick button background, text color, and link color with a color picker
Three button styles — Filled, Outline, and Pill
Zero dependencies — one .html file, works offline


## Usage

Download add-to-calendar-generator.html
Open it in any modern browser
Fill in your event details on the left panel
Copy the generated HTML from the Snippet or Full Email tab
Paste into an Eloqua Custom HTML content block


## Output
### Email Snippet
A self-contained table-based button block you can drop anywhere in an existing email template:

### Full HTML Email
A complete Eloqua-ready email template with header, event details, the button block, and footer placeholder (including <!-- UNSUBSCRIBE_LINK --> comment for your Eloqua merge field).

## Calendar Provider Notes
ProviderMethodNotesGoogle CalendarURL redirectOpens Google Calendar with fields pre-filledOutlook.comURL redirectOpens Outlook.com compose viewApple / iCal.ics downloaddata:text/calendar link — works in Gmail, Apple MailYahoo CalendarURL redirectOpens Yahoo Calendar with fields pre-filled

Outlook on Windows will often intercept the email and show its own native "Add to Calendar" prompt, hiding the provider link row. This is Outlook's rendering behavior and cannot be overridden in HTML.


## Limitations

Times are converted to UTC in all generated links. Enter your event start/end in local time and the tool handles the conversion.
The data:text/calendar link for Apple / iCal may be blocked by some corporate email security gateways. In that case, host the .ics file on a CDN and replace the link with the hosted URL.
Test in Litmus or Email on Acid before sending, especially for Outlook 2016/2019.


## Built With

Vanilla HTML, CSS, and JavaScript — no frameworks
DM Sans + Fira Code + Syne via Google Fonts
