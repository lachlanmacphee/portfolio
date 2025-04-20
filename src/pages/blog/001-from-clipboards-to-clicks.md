---
layout: ../../layouts/BlogPostLayout.astro
date: "2025-04-20"
title: "From Clipboards to Clicks: Digitising a Run Club"
description: "I transformed a running club from pen and paper to a realtime online experience with Pocketbase."
status: "published"
---

Since 2003, the heart of Gunn Runners South Melbourne beat to the rhythm of feet pounding the pavement around Albert Park Lake every Tuesday night. But behind the scenes, the pulse of their timekeeping was a little more analogue. Picture this: a volunteer armed with a clipboard, a pen, and a printed sheet. As runners registered, names were meticulously matched to bib numbers. Then, the real challenge began at the finish line – frantically scribbling down times as runners crossed, often in groups, hoping we got them all down on the sheet in order. It was slow, prone to errors, and incredibly stressful for the volunteers, especially on busy nights. I knew there had to be a better way.

Gunn Runners, affectionately known as "Gunnies", is more than just a run club; it's a community. We meet weekly at the Limerick Arms Hotel for a timed 3.5km or 5km run, welcoming runners of all abilities. The $5 run fee supports the club and the charities that we choose to donate to. But our 20-year-old paper timekeeping system was becoming a bottleneck. Transcribing results into our WordPress database was tedious, historical data was hard to reach, and managing waivers was a separate manual process. The need for a digital transformation was clear.

Enter the "Gunnies App" – a custom-built solution I designed specifically for the club's needs. The goal was simple: streamline the entire Tuesday night process, from registration to results, making it faster, more accurate, and less stressful for their invaluable volunteers, then add a bunch of stuff that would help us remain as Melbourne's most social running club.

### Building the Solution

I opted for a modern web application stack. The frontend, the part the runners and volunteers interact with, is built using React and Vite, styled with Tailwind CSS. This provides a responsive and user-friendly interface accessible on tablets and phones – perfect for trackside use.

For the backend, I chose Pocketbase, an open-source backend-in-a-box solution. It provides the database, real-time subscriptions, user authentication, and file storage needed, all manageable through a simple admin UI. I set up hosting for this efficiently on Fly.io.

### Key Features: Solving the Paper Pain Points

The Gunnies App tackles the old system's flaws head-on:

1.  **Digital Registration & Bib Assignment:** The clipboard is gone! Volunteers now use the app to register runners. Participants select their name (linked to their signed digital waiver) and are assigned a bib number for the run. The system prevents duplicate bibs or participant entries.
2.  **Live Time Tracking:** This is the core improvement. The app features a dedicated timing interface. As runners cross the finish line, a volunteer simply taps their bib number on the screen. The app records the precise time instantly. Handling multiple finishers simultaneously is no longer a frantic scribble-fest but a series of quick taps.
3.  **Real-time Leaderboard:** Forget waiting until the next day (or longer!) for results. As times are recorded, the leaderboard updates live within the app. Runners can see their time and position almost immediately after finishing.
4.  **Waiver Management:** Waivers are now digital. New runners sign electronically, and the system stores their acceptance, linking it to their profile. No more paper forms to file!
5.  **Historical Data & Stats:** All run data is stored digitally in Pocketbase. This allows runners to track their performance over time and enables the club to easily view past results and generate statistics. I even set up views to quickly see top performers, like the top ten female runners in the 5km event.
6.  **Beyond Timing:** The app also includes features for managing weekly volunteers, posting upcoming events, sharing club news via banners, running fun trivia quizzes, and maintaining a club wiki and FAQ section.

### Under the Hood: The Pocketbase Schema

Pocketbase stores the data in collections, similar to tables in a traditional database. Here’s a glimpse into how I structured things:

- **`waivers`**: Stores participant details and waiver acceptance status. Includes fields like `name`, `email`, `gender`, `emergency_contact`, etc.
- **`group_runs`**: Represents each Tuesday night event, holding the date and potentially weather information.
- **`participant_runs`**: This is crucial. It links a `waiver` record (the runner) to a `group_run` record (the event) and stores their `bib_number`, chosen `distance` (3.5 or 5), and recorded `time_seconds`.
- **`volunteers`**: Tracks who volunteered for which date and role.
- **`events`**, **`trivia_questions`**, **`wiki_pages`**: Collections for the additional features.

I also leveraged Pocketbase's **view** collections to create pre-defined queries for things like leaderboards:

```json
// Example: top_10_male_5k view schema snippet
{
  "id": "ib2a5ada1pdo9jk", // Unique ID for this collection definition
  "name": "top_10_male_5k", // Name of the view
  "type": "view",
  "system": false,
  "schema": [
    // Fields exposed by the view
    {
      "system": false,
      "id": "ffoxsxfk",
      "name": "name",
      "type": "text"
      // ... other field options
    },
    {
      "system": false,
      "id": "f9qgqj9q",
      "name": "time_seconds",
      "type": "number"
      // ... other field options
    }
    // ... other fields like 'id', 'created'
  ],
  "indexes": [],
  "listRule": null, // Access rules
  "viewRule": null,
  "createRule": null,
  "updateRule": null,
  "deleteRule": null,
  "options": {
    // The SQL query defining the view
    "query": "SELECT \n    (ROW_NUMBER() OVER (ORDER BY min_time)) as id,\n    name,\n    min_time as time_seconds,\n    created\nFROM (\n    SELECT \n        participant_runs.name,\n        MIN(participant_runs.time_seconds) as min_time,\n        participant_runs.created as created\n    FROM \n        participant_runs \n    JOIN \n        waivers ON participant_runs.waiver_id = waivers.id\n    WHERE \n        participant_runs.distance = 5 -- Filter for 5k distance\n        AND participant_runs.time_seconds != 0\n        AND waivers.gender = 'Male' -- Filter for Male\n    GROUP BY \n        participant_runs.name\n) as distinct_runs\nORDER BY \n    min_time \nLIMIT 10;" // Get only the top 10
  }
}
```

Similar views exist for other categories like `top_10_female_5k`, `top_10_male_3k`, and `top_10_female_3k`.

### The Transition and Benefits

Rolling out the app involved training the club's committee and regular volunteers so that there was always someone around who knew how to use the app. We ran the paper system in parallel for a couple of weeks to ensure accuracy and build confidence. Feedback was crucial – I made minor tweaks to the UI and workflow based on volunteer input. Working so closely and in-person with the team here allowed us to optimise the experience very rapidly.

The benefits were immediate and significant:

- **Speed:** Registration and timing are drastically faster.
- **Accuracy:** Transcription errors are eliminated. Times are captured precisely.
- **Reduced Volunteer Stress:** Finish line duty is no longer a high-pressure task.
- **Instant Results:** Runners love seeing their times immediately.
- **Data Accessibility:** Historical results and personal bests are easily accessible.
- **Engagement:** Features like stats, trivia, and event listings keep members more connected.
- **Efficiency:** Admin tasks like managing waivers and results are streamlined.

### Looking Ahead

The transition from pen and paper to the Gunnies App has fundamentally improved how Gunn Runners operates. It has freed up volunteer time, enhanced the runner experience, and provided valuable data insights. While built for Gunnies, [the codebase](https://github.com/lachlanmacphee/runclub) is available for other clubs to adapt. Digitising our run wasn't just about adopting new technology; it was about preserving the community spirit by making the operational side smoother, allowing everyone to focus more on the joy of the run (and the post-run chat at the pub!).
