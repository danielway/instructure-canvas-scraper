# Instructure Canvas Scraper

This is a simple scraper for the Instructure Canvas LMS (learning management system). It is focused on downloading materials from courses like lecture slides and student assignment submissions, but could be easily modified to consume other data through Canvas's API.

## Goals

- Identify all of the student's enrolled courses, including past courses
- Download all course materials (lecture slides, accompanying materials)
- Download all submitted materials (student assignment submissions)
- Download all assignment prompts/materials
- Organize all of this into an understandable structure
- Operate incrementally, so it may be re-run and detect new materials

## Implementation

This application uses both the Canvas REST API and GraphQL API. Documentation can be found for both [here](https://canvas.instructure.com/doc/api/index.html), and an instance of GraphiQL can be accessed for any Canvas instance at `{CanvasApplicationURL}/graphiql` for exploring what data is available (almost everything in Canvas is available).

The application begins by executing a series of summary-level queries for the student's course enrollments, modules, files, assignments, and submissions. From there, a comparison is made between the summary information and the local filesystem. Any differences are queued to be downloaded and a worker begins processing them.
