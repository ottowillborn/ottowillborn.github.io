+++
title = "UVic Room Booking System"
date = "2025-08-01"
description = "Room booking service for classrooms at the University of Victoria"
repo = "https://github.com/ottowillborn/UVicBookingSystem"
demo = "https://drive.google.com/file/d/1ybOXO8bDZU2RxtvfDB9qaNETDifpW5-P/view?usp=sharing"
stack = ["typescript", "docker", "mcp", "k6"]
featured = true
+++

I was the developer in charge of the frontend for this system. We built it from square one with a set of requirements, and were encouraged to use LLMs for development.

### The Big Requirement
* **Concurrency & Atomicity:** Designed and implemented a robust scheduling logic to handle high-concurrency requests. By utilizing database transactions (ACID compliance), the system prevents race conditions, ensuring that no two users can book the same room at the same time, even when simultaneous requests are received.
* **Infrastructure:** Engineered the system to be environment-agnostic using Docker and Docker Compose. This ensures 1:1 parity between development, testing, and production environments, eliminating "it works on my machine" issues.

### The App
* **Frontend Architecture:** Developed a responsive, interactive calendar interface using TypeScript. Managed complex client-side state to handle room availability filtering, time-slot selection, and real-time feedback.
* **Integration Flow:** Created a seamless UX where the frontend communicates with the backend API to validate availability before committing a booking, ensuring the UI always reflects the current state of the database.

### MCP (Model Context Protocol) Integration
* **AI-Native Workflow:** Implemented an MCP server to bridge the gap between the booking system and Claude Desktop. This allows users to perform complex booking actions (e.g., "Find and book a room for 3 people on Tuesday at 2 PM") using natural language, significantly lowering the barrier to entry for administrative tasks.

### Testing & Documentation
* **Reliability:** Established a CI/CD-ready testing suite. Used `npm test` for unit testing critical API endpoints to ensure logic stability.
* **Performance:** Utilized **k6** to conduct load testing, simulating peak traffic hours at the university to identify potential bottlenecks in database queries and API response times.
* **Governance:** Enforced high engineering standards by documenting the RESTful API via Swagger (OpenAPI) and maintaining Architecture Decision Records (ADRs) to track the rationale behind key technical choices.

### Issues Faced
* **Handling Race Conditions:** Initially, we encountered race conditions where two users could select the same time slot simultaneously. We resolved this by implementing database-level transaction locking to ensure atomicity during the booking commit process.
* **State Synchronization:** Keeping the frontend calendar state in sync with the backend database during rapid user input required a custom event-bus implementation. We optimized this by using a standardized API response structure that triggered immediate UI re-renders.
* **Docker Networking:** During the initial setup of the microservices, we struggled with container-to-container communication. We resolved this by defining a custom virtual bridge network in our `docker-compose.yml` file, allowing services to communicate via internal DNS names.
* **MCP Protocol Complexity:** Integrating the MCP server required mapping our existing API routes to natural language intents. The primary challenge was structuring our API documentation in a way that the Claude model could interpret precisely, which we solved by iterating on our Swagger/OpenAPI schemas.