Gregory Hamilton
Project 4 – Student Task Tracker Architecture
Section 1: Description of Our Container
1.1 Application Overview
Student Task Tracker is a cloud-based application designed to help college students organize their assignments, manage coursework, and track assignment completion. Students can add, edit, delete, and organize assignments by course. The application also allows students to monitor their progress and identify assignments that still need to be completed.

The application will use cloud-based software architecture so users can access their information through the internet.

1.2 What Is Cloud-Based Software?
Cloud-based software is software that runs on servers accessed through the internet instead of relying entirely on a user's personal computer. Users can access the application from different devices as long as they have an internet connection.

Student Task Tracker will use a shared cloud-based database to store user accounts, courses, and assignments. This allows application information to be available to authorized users when they access the application.

1.3 What Is Docker?
Docker is a platform that allows developers to package applications and their required dependencies into containers. It makes applications easier to deploy and run in different environments.

1.4 What Is a Container?
A container is an isolated environment that includes the application and the files, libraries, and dependencies needed to run it.

Student Task Tracker will use a Docker container to package the application's backend and its runtime environment.

1.5 What Is a Docker Image?
A Docker image is a read-only template used to create Docker containers. It contains the application code, dependencies, and instructions needed to run the application.

1.6 What Is a Docker Daemon?
The Docker daemon is a background service that manages Docker objects. It handles tasks such as creating, running, and stopping containers and managing images.

1.7 What Will Be Inside Our Container?
The Student Task Tracker application container will contain:

Application source code.
Backend application files.
Required runtime environment.
Application dependencies and libraries.
Configuration files.
API and server functionality.
Database connection settings.
The shared database will be hosted separately from the application container. This allows the application to communicate with the database without storing the main database inside the container.

Section 2: Components and Necessary Files
Student Task Tracker will be organized into several major components. Each component will perform a specific responsibility and communicate with the other components when necessary.

2.1 Frontend Component
Purpose:

The frontend component provides the interface students use to interact with Student Task Tracker. It allows students to view assignments, enter assignment information, and organize their coursework.

Sub-components:

Assignment display.
Assignment input forms.
Course selection interface.
Progress display.
Necessary Files:

index.html – Provides the main application page.
style.css – Controls the appearance and layout.
script.js – Handles frontend interactions.
2.2 Assignment Management Component
Purpose:

This component allows students to create, edit, delete, and manage assignments.

Sub-components:

Add assignment.
Edit assignment.
Delete assignment.
View assignment details.
Necessary Files:

assignments.py – Handles assignment operations.
assignment_service.py – Contains assignment management logic.
assignment_routes.py – Handles assignment-related requests.
Database Usage:

This component uses the Assignments table to store and retrieve assignment information. It also references the Courses table to associate assignments with courses.

2.3 Assignment Completion Component
Purpose:

This component allows students to track their assignment completion progress. Students can mark assignments as completed or incomplete.

Sub-components:

Mark assignment as completed.
Update assignment status.
View completed assignments.
Track outstanding assignments.
Necessary Files:

completion.py – Handles assignment completion operations.
completion_service.py – Processes completion status changes.
progress.py – Calculates assignment progress.
Database Usage:

This component uses the Assignments table. It updates and retrieves the completion status of assignments.

2.4 Course Organization Component
Purpose:

This component allows students to organize assignments according to their courses. Students can filter and view assignments associated with specific courses.

Sub-components:

Add courses.
View courses.
Associate assignments with courses.
Filter assignments by course.
Necessary Files:

courses.py – Handles course information.
course_service.py – Contains course-related operations.
course_routes.py – Handles course requests.
Database Usage:

This component uses the Courses table and references the Assignments table to organize assignments by course.

2.5 Database Component
Purpose:

The database component manages the storage and retrieval of information used throughout the application.

Sub-components:

Database connection.
User data management.
Course data management.
Assignment data management.
Necessary Files:

database.py – Establishes database connections.
models.py – Defines database models.
schema.sql – Defines the database tables.
Database Usage:

The application will use a shared cloud-hosted relational database. The frontend and backend components will access information through the backend rather than connecting directly to the database.

Section 3: Structure of Related Tables in the Database
3.1 Database Overview
Student Task Tracker will use a shared relational database hosted in the cloud.

The database will store information about users, courses, and assignments. The database will allow the application components to access consistent information.

The database will contain three major tables:

Users
Courses
Assignments
3.2 Users Table
Purpose: Stores information about students who use the application.


Column	Data Type	Description
user_id	INT	Primary key identifying each user
first_name	VARCHAR(50)	Student's first name
last_name	VARCHAR(50)	Student's last name
email	VARCHAR(100)	Student's email address
password_hash	VARCHAR(255)	Securely stored password hash
created_at	TIMESTAMP	Date the account was created
3.3 Courses Table
Purpose: Stores course information belonging to students.


Column	Data Type	Description
course_id	INT	Primary key identifying each course
user_id	INT	Foreign key referencing Users
course_name	VARCHAR(100)	Name of the course
course_code	VARCHAR(20)	Course identification code
created_at	TIMESTAMP	Date the course was created
3.4 Assignments Table
Purpose: Stores assignment information and tracks completion status.


Column	Data Type	Description
assignment_id	INT	Primary key identifying each assignment
user_id	INT	Foreign key referencing Users
course_id	INT	Foreign key referencing Courses
title	VARCHAR(150)	Assignment title
description	TEXT	Assignment details
due_date	DATE	Assignment due date
is_completed	BOOLEAN	Indicates whether the assignment is completed
created_at	TIMESTAMP	Date the assignment was created
3.5 Database Relationships
The database tables will be connected using primary keys and foreign keys.

Each user can have multiple courses.
Each user can have multiple assignments.
Each course can have multiple assignments.
Each assignment belongs to a user and can be associated with a course.
The relationships help keep information organized and prevent assignments from being associated with the wrong users or courses.

3.6 Shared Database Explanation
Student Task Tracker will use a shared cloud-hosted database rather than a separate local database for each application component.

The database will be accessed through the backend application. This approach allows the assignment management, completion tracking, and course organization components to work with the same information.

Access to the database will be controlled through the backend to help protect student information.

Conclusion
The architecture of Student Task Tracker will organize the application into separate components that work together to help college students manage their coursework.

The application will use Docker containers to package the application and its dependencies. A shared cloud-hosted relational database will store users, courses, and assignments.

This architecture will make the application easier to maintain, organize, and deploy while allowing students to manage assignments and track their academic progress.