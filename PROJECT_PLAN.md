# Master Control Program: Trinity College Accidentals Website Redevelopment

-   **Project:** The Accidentals - Official Website
-   **Version:** 1.0
-   **Date:** September 29, 2025
-   **Author:** Sean Balbale

---

## 1.0 Executive Summary

This document outlines the master plan for the redevelopment of the Trinity College Accidentals' official website. The project's goal is to create a modern, high-performance, and visually engaging digital platform that serves as the group's primary hub for marketing, recruitment, and fan engagement.

The technical foundation will be a decoupled architecture utilizing **Next.js** for the frontend, **Strapi** as the headless Content Management System (CMS), and **Firebase** for hosting and serverless functions. The user interface will be built with the **shadcn/ui** component library, ensuring a clean, accessible, and fully responsive experience on both laptop and mobile devices.

---

## 2.0 Project Goals & Objectives

-   **Primary Goal:** To create a professional online presence that accurately reflects the talent and personality of the group.
-   **Objectives:**
    -   Increase booking inquiries through a streamlined and prominent booking system.
    -   Showcase the group's musical portfolio and performance history.
    -   Simplify the audition process for prospective members.
    -   Build a community through an integrated mailing list and social media links.
    -   Empower non-technical group members to manage all website content easily through the Strapi CMS.

---

## 3.0 Technical Architecture & Stack

This project will use a modern JAMstack architecture, separating the frontend presentation from the backend content management.

-   **Frontend Framework:** **Next.js 14+** (App Router)
    -   **Benefit:** Enables a mix of Server-Side Rendering (SSR) and Static Site Generation (SSG) for optimal performance and SEO.
-   **UI Component Library:** **shadcn/ui**
    -   **Benefit:** Provides beautifully designed, accessible, and composable components built on Tailwind CSS and Radix UI. This accelerates development and ensures a consistent, professional aesthetic.
-   **CMS (Backend):** **Strapi v5**
    -   **Benefit:** A flexible, open-source headless CMS. It will provide a user-friendly admin panel for managing all site content.
    -   **Hosting:** Strapi will be deployed to a dedicated service like **Render** or **DigitalOcean**, which is optimized for hosting Node.js applications.
-   **Platform & Hosting:** **Firebase**
    -   **Firebase Hosting:** The compiled Next.js frontend will be deployed here for global CDN delivery and fast load times.
    -   **Firebase Functions:** Will be used to handle dynamic actions like mailing list signups and booking form submissions, preventing reliance on a third-party service.

### Data Flow Diagram

```

[Content Manager] -\> [Strapi Admin Panel] -\> [Strapi API] -\> [Next.js Frontend (on Firebase)] -\> [Website Visitor]

[Visitor submits form] -\> [Next.js Frontend] -\> [Firebase Function] -\> [Database / Email Notification]

```

---

## 4.0 Site Structure & Page Requirements

The website will be fully responsive, with dedicated design considerations for both laptop and mobile views.

| Page              | Purpose & Key Components (using shadcn/ui)                                                                                                                              |
| :---------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Home** | First impression of the group. Features a hero section with a video or high-impact photo, snippets of recent news, featured music, and a call-to-action to book. Uses `Card` for content snippets and `Button` for CTAs. |
| **About Us** | Tells the story of the Accidentals. Includes group history, mission, and notable achievements. Will feature a timeline and testimonials.                                |
| **Members** | Showcase the current members and potentially a section for notable alumni. A grid of `Card` components, each opening a `Dialog` with a member's bio and photo.        |
| **Music** | The group's digital portfolio. A discography section with album art, tracklists, and links to Spotify/Apple Music. An embedded video gallery from YouTube.                 |
| **Events** | A list of upcoming and past performances. Upcoming events will have date, time, venue, and a link to tickets. Uses `Table` for a clear layout and `Badge` to denote event status. |
| **Booking** | The primary conversion page for generating gigs. Features a clear contact form built with `Input`, `Textarea`, and `Button`. May also include a `Calendar` to show general availability. |
| **Auditions** | A dedicated portal for recruitment. Provides information on audition dates, requirements, and what to prepare. Includes a sign-up form for an audition slot or to join an "audition info" mailing list. |
| **Press Kit (New)** | A hidden or footer-linked page for event organizers. Contains downloadable high-resolution photos, the group's logo, a one-sheet bio, and technical requirements for performances. |

---

## 5.0 Design System & User Experience (UX)

-   **Mobile-First Responsive Design:** All views will be designed for mobile first and then scaled up to tablet and laptop sizes to ensure a seamless experience on any device.
-   **Aesthetic:** Clean, modern, and minimalist, drawing inspiration from the `shadcn/ui` aesthetic. A color palette based on Trinity College's branding (navy blue, white) will be used.
-   **Interactivity:** Subtle animations and transitions using `framer-motion` will be employed to enhance the user experience. Interactive elements like modals (`Dialog`), dropdowns (`Select`), and tabs (`Tabs`) will be used to present information cleanly.
-   **Accessibility (A11Y):** Adherence to WCAG 2.1 guidelines will be a priority. This is a core strength of `shadcn/ui` and will be maintained throughout the project.

---

## 6.0 CMS (Strapi) Content Modeling

The Strapi admin panel will be configured with the following "Collection Types" to empower easy content management:

-   **Member:**
    -   Fields: `name` (Text), `voicePart` (Text), `headshot` (Media), `bio` (Rich Text), `isActive` (Boolean), `graduationYear` (Number).
-   **Album:**
    -   Fields: `title` (Text), `coverArt` (Media), `releaseDate` (Date), `spotifyLink` (Text), `appleMusicLink` (Text), `tracklist` (Component).
-   **Event:**
    -   Fields: `title` (Text), `date` (DateTime), `venue` (Text), `description` (Rich Text), `ticketLink` (Text), `isUpcoming` (Boolean).
-   **Audition Information:**
    -   A "Single Type" collection to manage content on the auditions page, like dates, requirements text, and FAQs.
-   **Page Content:**
    -   Single Type collections for managing content on the "About Us" and "Booking" pages.

---

## 7.0 Additional Features & Integrations

-   **Mailing List:**
    -   A reusable footer component with a sign-up form.
    -   The form will submit to a Firebase Function that adds the email to a **Mailchimp** audience via their API.
-   **SEO:**
    -   Next.js's metadata API will be used to generate dynamic `title` and `description` tags for each page based on content from Strapi, ensuring strong search engine visibility.
-   **Analytics:**
    -   **Vercel Analytics** or **Google Analytics 4** will be integrated to track website traffic and user engagement.
