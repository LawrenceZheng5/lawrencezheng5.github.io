---
layout: project
type: project
image: img/manoa-guesser/logo.jpg
title: "Manoa Guesser"
date: 2025-12-11
published: True
labels:
  - React
  - Nextjs
  - Leaflet
summary: "Designed Geo Guesser but for the UHM campus"
---

This was the final project that I made for ICS 314 - Software Engineering. You can play it [here](https://manoa-guesser.vercel.app/).

### Overview
Manoa Guesser is a gamified exploration web application designed to help UH Mānoa students become more familiar with campus locations. Each year, new students arrive on campus and often struggle to navigate the large environment. This project aims to make that process more engaging by turning real campus imagery into a location-guessing game.

The system allows users to guess where a photo was taken on an interactive Leaflet map, earn points based on accuracy, climb the leaderboard, and even contribute their own images through a submission system. Administrators can moderate submitted photos, ensuring only approved images appear in gameplay. The project also demonstrates modern full-stack development concepts, including authentication, database integration, API routing, geolocation interfaces, and CI/CD workflows.

A link to the GitHub organization can be found [here](https://github.com/manoa-guesser).

### Contributions
For this project, I primarily worked on the Submission Page and contributed significantly to the Game Page. My contributions included:

- Implementing the Leaflet map integration, enabling users to place location guesses.
- Developing the scoring system, which calculates accuracy based on map distance.
- Writing backend code to retrieve approved images for gameplay using Prisma and Next.js API routes.
- Building the submission workflow, including:
  - Image upload UI
  - Hint and location input fields
  - Integration with Supabase storage
  - Sending submissions for admin review

I also assisted in debugging authentication, coordinating environment variables, and supporting team members during feature integration.

### Learnings
This project strengthened my understanding of full-stack web development, especially how frameworks like Next.js handle routing, server components, and API endpoints. I learned how Prisma interacts with a PostgreSQL database and how environment variables affect deployment on platforms like Vercel.

Working with Supabase taught me how cloud storage integrates into a production system, while Playwright and ESLint reinforced automated testing and coding standards. On the frontend, I deepened my experience with React, Leaflet, and component-driven UI development.

Overall, I learned how various parts of a modern web application connect, from database schema design to client-side rendering to continuous integration workflows.

Documentation for the complete project can be found [here](https://manoa-guesser.github.io/).

### Screenshots

<img class='img-fluid' src="..\img/manoa-guesser/M3-Game-Page.png" alt="Game Page Screenshot">

<img class='img-fluid' src="..\img/manoa-guesser/M3-Submission.png" alt="Submission Page Screenshot">

<img class='img-fluid' src="..\img/manoa-guesser/M3-Leaderboard.png" alt="Leaderboard Screenshot">
