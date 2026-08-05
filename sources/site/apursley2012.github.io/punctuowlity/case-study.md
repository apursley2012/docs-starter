# Source: https://apursley2012.github.io/punctuowlity/case-study.html

![PunctuOwlity Event Tracking](https://apursley2012.github.io/punctuowlity/assets/punctuowlity-logo.png)

Case Study

# Building PunctuOwlity into a Complete Responsive Event Tracker

PunctuOwlity is an event-tracking application designed to make upcoming dates, times, and reminders easy to review at a glance. I originally built the project as an Android application, then adapted the same interface and workflow into a static web application that can run on GitHub Pages.

## Project Overview

The application supports account creation, login, SMS preference selection, event creation, event editing, event deletion, search, category filters, and reminder status. Its visual identity uses a light blue background, coral toolbar and action buttons, teal date banner, navy text, decorative type, and a custom owl logo that combines a calendar and clock.

My goal was not to redesign the app during the web conversion. I wanted the browser version to preserve the Android layout and personality while scaling cleanly beyond the original phone-sized screen.

## The Problem

The Android project depended on activities, XML layouts, Material components, vector drawables, SQLite, and device permissions. None of those pieces transfer directly to a static website. I needed to reproduce the interface in HTML and CSS, replace Android navigation with webpage navigation, and rebuild the application logic in JavaScript without introducing a server requirement.

The conversion also had to preserve the original two-column event grid. A typical desktop redesign would spread cards across additional columns, but that would change the composition. Instead, the web layout keeps the same two-column structure and scales the complete interface proportionally.

## Core Requirements

- Open on the login page, matching the Android launcher activity.
- Create and store user accounts locally.
- Allow login with either a username or email address.
- Preserve the SMS approval step while remaining usable as a static site.
- Add, edit, display, search, filter, and delete events.
- Calculate the weekday and two-digit day from each saved date.
- Store reminder status and display the correct alarm icon.
- Match the supplied screenshots, colors, typography, logo, icons, spacing, and card arrangement.
- Remain responsive without turning the interface into a different design.

## Design and Interface

I treated the Android XML and completed screenshots as the source of truth. The main screen keeps the coral toolbar, centered logo, “Upcoming Events” heading, outlined search field, teal month banner, dotted dividers, evenly distributed category tabs, dark event-grid frame, white cards, and coral floating add button.

The event cards preserve the original information hierarchy. The weekday and reminder state appear first, followed by the large date number, event title, and time. Edit and delete controls remain in the upper-right corner so each card works the same way as the Android version.

## From SQLite to Browser Storage

The Android application stored users and events in SQLite. A static GitHub Pages site cannot run that database, so I rebuilt the data layer with browser storage. User accounts, SMS preferences, and event records remain available between visits without requiring a backend.

I also added normalization for older or incomplete event records. If a stored record contains a raw date such as `2026-07-18`, the app calculates and displays `SAT` and `18`. Raw 24-hour times are converted to the compact 12-hour format used by the original cards. This prevents database-shaped values from appearing directly in the interface.

## Authentication and Account Creation

The sign-up page records first name, last name, email address, optional phone number, username, password, and password confirmation. Duplicate usernames and email addresses are rejected. The login page accepts either the saved username or email address with the matching password.

This is local application authentication rather than a production identity service. It is appropriate for a self-contained static demonstration, but a deployed application handling real accounts would need a secure backend, password hashing, protected sessions, recovery tools, and server-side validation.

## Reminders and SMS

The Android source requested permission to send SMS messages but did not include a complete SMS delivery or scheduling system. A static webpage also cannot safely contain credentials for an SMS provider. I preserved the permission-choice screen, saved the user’s preference, and used browser notifications as the available static-site reminder option.

The event form stores whether a reminder is enabled, and the event card reflects that choice with the supplied alarm-on or alarm-off vector icon.

## Responsive Behavior

The responsive work focuses on scaling rather than rearranging. The event grid remains two columns across supported phone, tablet, and desktop widths. Text, controls, spacing, and imagery grow with the available space. Only extremely narrow screens fall back to a single column to prevent clipped content and unusable controls.

Form fields remain large enough to use by touch, buttons include accessible labels, decorative images have alternative text, and status messages are announced through appropriate live regions.

## Challenges and Corrections

The most difficult part was preserving fidelity while translating fixed Android constraints into responsive CSS. Small changes to maximum widths, card ratios, icon paths, or breakpoints could make the browser version look like a new dashboard instead of the original app. I corrected that by comparing the rendered page against the supplied screenshots and returning to the measurements and hierarchy defined in the XML.

Another issue involved raw saved values. Events initially displayed full ISO dates and missing weekdays because the browser data did not match the Android model’s helper methods. Adding a normalization layer restored the intended presentation without forcing users to recreate their events.

## Result

The completed web version preserves PunctuOwlity’s original identity and core workflow while removing its dependency on Android, SQLite, and device-only components. It runs as a static HTML, CSS, and JavaScript project, supports persistent local interaction, and can be hosted directly on GitHub Pages.

This project reinforced an important distinction for me: responsive conversion is not the same thing as redesign. The successful approach was to protect the existing visual relationships first, then make those relationships flexible enough to work across screen sizes.