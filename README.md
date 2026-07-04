# Restaurant Reservation Management System

A full-stack implementation of a restaurant table reservation system featuring a dynamic React frontend and a robust Node.js Express backend. Designed to handle role-based access control and prevent capacity or scheduling double-bookings.

## Setup Instructions
1. Download and extract the source repository package.
2. Install dependencies locally by executing: `npm install`
3. Launch the environment orchestrator via: `npm start`
4. Access the web interface layout at: `http://localhost:3000`

## Core Technical Assumptions Made
- The system assumes a single operational restaurant instance.
- Tables are configured programmatically with specified seating maximum bounds.
- Bookings are divided into fixed, distinct 2-hour dining windows to simplify slot distribution.

## Reservation & Availability Logic (Conflict Handling)
- **Capacity Constraint Rule:** Before logging any slot parameters, the system references the `Table` model's capacity against the incoming user passenger count. If guests exceed table dimensions, a strict `HTTP 400 Bad Request` code rejects the validation sequence.
- **Double-Booking Prevention:** The creation route utilizes an atomic MongoDB tracking lookup query searching for existing reservation vectors on identical table IDs, matching target dates, and overlapping time windows. If found, conflicts are blocked gracefully with meaningful user warning contexts.

## Role-Based Access Control Structure
- **Customer:** Authenticated users assigned standard profiles can submit new table requests, look up their distinct individual list items, and cancel bookings belonging to their unique account IDs.
- **Administrator:** Accounts initialized with master role values bypass standard restrictions, providing complete monitoring over all active system rows, administrative cancellation triggers, and date filter selections.

## Known Limitations & Improvements
- **Current Limitation:** Database records currently depend on runtime sandbox memory layers or default instances unless customized via environmental parameters.
- **Future Improvements:** Integrating real-time state listeners (WebSockets) to dynamically lock table layouts the moment an alternate customer opens a booking canvas.

