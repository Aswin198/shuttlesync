# Initial Database Design

This document describes the initial database tables required for ShuttleSync.

## Users

|Field          | Data Type     | Required | Description                                        |
|---|---|---|---|
|user_id        | INTEGER       | yes      | stores UNIQUE id of user, PRIMARY KEY              |
|username       | VARCHAR       | yes      | stores username of user, UNIQUE                    |
|password_hash  | VARCHAR       | yes      | stroes hashed password                             |
|is_admin       | BOOLEAN       | yes      | stores admin status (T/F)                          |
|email          | VARCHAR       | yes      | stores email to help with resetting process, UNIQUE|
|created_at     | TIMESTAMP     | yes      | stores date&time of registration                   |


## Training Sessions    

|Field          | Data Type| Required | Description |
|---|---|---|---|
|session_id     | INTEGER  | yes      | to keep track of session_id, PRIMARY KEY    |
|session_date   | DATE     | yes      | to store date of session                    |
|start_time     | TIME     | yes      | to store start time of session              |
|end_time       | TIME     | yes      | to store end time of session                | 
|location       | VARCHAR  | yes      | to store location of court                  |
|court_num      | VARCHAR  | yes      | to store court number                       |
|capacity       | INTEGER  | yes      | open to how many ppl                        |
|status         | VARCHAR  | yes      | scheduled, cancelled, completed             |
|created_by     | INTEGER  | yes      | to track who added the session, FOREIGN KEY |
|created_at     | TIMESTAMP| yes      | to track the time it was creaeted           |


## Bookings

|Field      | Data Type | Required | Description                                    |
|---|---|---|---|
|booking_id | INTEGER   | yes      | to store id of booking created, PRIMARY KEY    |
|user_id    | INTEGER   | yes      | contains user who booked, FOREIGN KEY          |
|session_id | INTEGER   | yes      | contains which session is booked, FOREIGN KEY  |
|status     | VARCHAR   | yes      | booked, cancelled, attended, absent            |


## Relationships

- One user can create many training sessions.
- One user can have many bookings.
- One training session can have many bookings.
- Each booking references one user and one training session.

## Constraints

- Usernames must be unique.
- Emails must be unique.
- Capacity must be greater than zero.
- End time must be later than start time.
- A user cannot have multiple booking records for the same session.
- Session status can only be scheduled, cancelled, or completed.
- Booking status can only be booked, cancelled, attended, or absent.