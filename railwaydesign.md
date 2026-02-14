# Design Document
## Project Title: AI-Based Smart Seat Selection System for Railway Booking (2D Layout)

## 1. Introduction
This document describes the design of an AI-based smart seat selection system for railway booking. The system provides a 2D coach layout interface where passengers can manually select seats and receive AI-driven seat recommendations.

The system focuses on improving comfort and safety, especially for women passengers and senior citizens.

---

## 2. System Architecture

### 2.1 High-Level Architecture
The system is divided into the following components:

1. Frontend UI Module (2D Layout Seat Selection)
2. Backend Booking Service
3. AI Recommendation Engine
4. Database Layer

---

## 3. Component Design

### 3.1 Frontend UI Module
Responsibilities:
- Display 2D coach layout with seats.
- Show booked and available seats.
- Allow user seat selection.
- Display recommended seats highlighted.
- Collect user preferences such as window, aisle, lower berth, safety mode.

UI Elements:
- Seat map grid layout
- Filter panel for preferences
- Recommended seat highlight
- Booking confirmation popup

---

### 3.2 Backend Booking Service
Responsibilities:
- Handle booking requests.
- Fetch real-time seat availability.
- Lock seat temporarily during booking.
- Confirm booking and update database.
- Communicate with AI engine for seat ranking.

APIs:
- GET /coach-layout/{train_id}/{coach_type}
- GET /seat-availability/{train_id}/{coach_id}
- POST /recommend-seats
- POST /confirm-booking

---

### 3.3 AI Recommendation Engine
The AI engine generates seat recommendations based on passenger needs and safety rules.

Inputs:
- Passenger details (age, gender)
- Seat preferences (window, aisle, berth type)
- Group size
- Available seat list
- Booked passenger distribution (female clusters, families)

Outputs:
- Ranked list of recommended seats
- Seat safety score and comfort score

---

## 4. AI Logic Design

### 4.1 Seat Scoring Method
Each available seat is assigned a score based on:

- Comfort score (window/lower berth preference)
- Safety score (female passenger nearby)
- Group adjacency score (seats together for group booking)
- Distance score (near entry, away from washroom)

Final Seat Score:
Final Score = (Comfort Score + Safety Score + Group Score + Distance Score)

The top-ranked seats are recommended to the passenger.

---

### 4.2 Women Safety Mode Logic
If Women Safety Mode is enabled:
- Identify all seats booked by female passengers.
- Check adjacent and nearby seats to female seats.
- Recommend seats that are closest to female clusters.
- Avoid isolated seats if journey time is night-based.

Safety Cluster Detection:
- Seats near 2 or more female passengers receive higher safety score.
- Seats in isolated corners receive lower safety score.

---

### 4.3 Senior Citizen Mode Logic
If passenger age >= 60:
- Prioritize lower berth seats first.
- If lower berth unavailable, recommend side lower.
- If side lower unavailable, recommend seats with minimum climbing difficulty.

This ensures elderly passengers receive comfortable travel.

---

### 4.4 Group/Family Booking Logic
For group size > 1:
- Search for adjacent seats in same bay.
- Minimize distance between group members.
- Suggest best cluster of seats available.
- If full cluster not available, recommend nearest possible distribution.

Optimization Approach:
- Greedy seat selection + adjacency check
- Ranking based on seat closeness

---

## 5. Database Design

### 5.1 Tables

#### Users Table
- user_id
- name
- phone
- email
- password_hash

#### Trains Table
- train_id
- train_name
- route_details

#### Coaches Table
- coach_id
- train_id
- coach_type
- total_seats

#### Seats Table
- seat_id
- coach_id
- seat_number
- seat_type (window/aisle/middle)
- berth_type (lower/middle/upper/side lower/side upper)

#### Bookings Table
- booking_id
- user_id
- train_id
- coach_id
- seat_id
- passenger_name
- age
- gender
- booking_status

---

## 6. Workflow Design

### 6.1 Seat Booking Workflow
1. User selects train and coach type.
2. System loads 2D coach layout.
3. User selects seat preferences.
4. AI engine recommends best seats.
5. User selects seat manually or chooses AI recommendation.
6. Backend locks seat temporarily.
7. User confirms payment.
8. Booking stored in database and seat marked as booked.

---

## 7. UI Design / Wireframe Concept
- Seat map shown in a grid format.
- Booked seats shown in red.
- Available seats shown in green.
- Recommended seats shown in blue highlight.
- Filters displayed on left panel:
  - Window
  - Aisle
  - Lower berth
  - Women safety mode
  - Senior citizen mode
  - Group booking

---

## 8. Technology Stack
Frontend:
- HTML, CSS, JavaScript / React / Flutter

Backend:
- Python (Flask/Django) or Java (Spring Boot)

Database:
- MySQL / PostgreSQL

AI Engine:
- Python-based recommendation module

Hosting:
- AWS Cloud (EC2, RDS, Lambda optional)

---

## 9. Security & Reliability Considerations
- Seat locking mechanism to prevent double booking.
- Secure authentication and encrypted storage of user data.
- Transaction-based booking confirmation.
- API rate limiting for abuse prevention.

---

## 10. Future Scope
- Voice-enabled booking for rural users.
- Multilingual interface.
- AR/3D coach visualization.
- Predictive crowd safety analysis.
- Smart pricing recommendation system.
