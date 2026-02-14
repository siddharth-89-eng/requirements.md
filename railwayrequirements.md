# Requirements Document
## Project Title: AI-Based Smart Seat Selection System for Railway Booking (2D Layout)

## 1. Overview
The current railway booking system allocates seats automatically and does not allow passengers to visually select their seats. This leads to passenger dissatisfaction, confusion, and safety concerns, especially for women and elderly passengers.

This project proposes an AI-based seat selection system that provides a 2D coach layout where passengers can manually select seats and also receive AI-based seat recommendations based on safety and comfort preferences.

---

## 2. Goals
- Provide passengers with a clear 2D coach layout for seat selection.
- Allow manual seat selection similar to airline booking systems.
- Provide AI recommendations for best seat selection.
- Ensure women safety by recommending seats near female passengers.
- Ensure senior citizen comfort by prioritizing lower berth allocation.
- Support family/group booking seat optimization.

---

## 3. Functional Requirements

### 3.1 User Authentication
- The system shall allow users to login/register.
- The system shall allow users to book tickets using passenger details.

### 3.2 Coach Layout Display
- The system shall display a 2D coach layout during seat selection.
- The system shall show available seats and booked seats in different colors.
- The system shall support multiple coach types (Sleeper, 3AC, 2AC, etc.).

### 3.3 Manual Seat Selection
- The system shall allow passengers to select seats by clicking on the 2D seat layout.
- The system shall prevent selection of already booked seats.
- The system shall allow users to deselect and reselect seats.

### 3.4 Seat Preference Selection
The system shall allow passengers to select preferences such as:
- Window seat preference
- Aisle seat preference
- Lower berth preference
- Seats away from washroom
- Seats near entry/exit

### 3.5 Women Safety Mode
- The system shall provide an option called "Women Safety Mode".
- If enabled, the AI shall recommend seats near already booked female passengers.
- The system shall prioritize seats in clusters of female passengers.
- If no nearby female seat is available, the system shall recommend the safest alternative.

### 3.6 Senior Citizen Mode
- The system shall detect senior citizen passengers based on age.
- If age >= 60, the system shall prioritize lower berth allocation.
- If lower berth is unavailable, the system shall suggest the nearest comfortable alternative (Side Lower or closest berth).

### 3.7 Group/Family Booking Optimization
- The system shall allow group booking for multiple passengers.
- The AI shall recommend seats that keep the group together.
- The system shall reduce seat separation between group members.

### 3.8 AI Recommendation Engine
- The system shall generate seat recommendations based on:
  - passenger preferences
  - seat availability
  - group size
  - safety rules
  - berth priority rules
- The AI shall rank available seats and highlight top recommended seats.

### 3.9 Booking Confirmation
- The system shall allow passengers to confirm selected seats.
- The system shall generate a booking summary before final confirmation.
- The system shall store confirmed booking details in the database.

---

## 4. Non-Functional Requirements

### 4.1 Performance
- The system should load coach layout within 2 seconds.
- The recommendation engine should respond within 1 second.

### 4.2 Scalability
- The system should support high traffic during peak booking hours.
- The system should handle multiple concurrent booking requests.

### 4.3 Security
- The system must securely store passenger data.
- The system must ensure seat booking transactions are consistent.

### 4.4 Usability
- The UI must be simple and mobile-friendly.
- The coach layout must be clearly understandable for all users.

### 4.5 Reliability
- The system must prevent double booking of the same seat.
- The system should ensure seat locking during booking confirmation.

---

## 5. Assumptions
- Passenger gender and age details are collected during booking.
- Real-time seat availability data is accessible through a database or API.
- Coach seat layout data is predefined for each coach type.

---

## 6. Constraints
- The system must be lightweight and work efficiently on low-end devices.
- The system should use 2D layout instead of heavy 3D visualization to reduce cost and complexity.

---

## 7. Future Enhancements
- Voice-based seat selection (regional language support).
- 3D coach visualization.
- AR-based coach preview.
- Predictive crowd safety recommendation.
- Dynamic pricing optimization.
