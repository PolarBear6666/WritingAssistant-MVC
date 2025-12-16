# WritingAssistant-MVC
Desktop AI Writing Assistant built in Java Swing, showcasing the MVC pattern, advanced software design (Strategy, Singleton, Repository), and robust resiliency features like Exponential Backoff and concurrency for network stability.
AI Writing Assistant (MVC + Design Patterns)
🌟 Project Overview
This project is a desktop application developed in Java using Swing, designed to demonstrate robust software engineering principles, including the Model-View-Controller (MVC) architectural pattern and several key Gang of Four (GoF) design patterns.

The application successfully connects to the OpenAI API to generate text, dynamically changing the AI's behavior based on a selected strategy (e.g., Creative Storytelling vs. Formal Academic Report).

✨ Architectural Highlights
This application strictly adheres to the Model-View-Controller (MVC) pattern for clear separation of concerns:

Model: Contains the business logic, API communication (APIService, APIClient), and data management (StrategyRepository, Config).

View: The Swing UI (MainFrame) displays data and captures user input.

Controller: (MainController) acts as the intermediary, handling user events and updating the Model/View.

🛠️ Design Patterns Implemented
The following GoF design patterns were strategically used to enhance flexibility, maintainability, and resource management:
1. Behavioral Patterns
Pattern,Implementation,Benefit
Strategy Pattern,"(GenerationStrategy Interface, implemented by CreativeStorytellingStrategy, FormalAcademicStrategy, etc.)","Allows the application to swap AI behavior (the ""strategy"") at runtime based on the user's selection, promoting dynamic context switching."
Observer Pattern,(Implemented by the Controller notifying the View),"Ensures the UI remains responsive and is updated asynchronously. The View observes the Model's state changes (e.g., generation start, generation complete, error)."
2. Creational Patterns
Pattern,Implementation,Benefit
Singleton Pattern,(APIClient and Config classes),"Guarantees that only one instance of the critical network client and configuration loader exists throughout the application, preventing resource conflicts and ensuring a single source of truth for API settings."
Factory Method Pattern,(Implicitly used by the StrategyRepository or a dedicated Strategy Factory),Centralizes the creation and management of the different GenerationStrategy objects.
3. Structural Pattern
Pattern,Implementation,Benefit
Repository Pattern,(SessionRepository),Decouples data access and persistence logic (saving and loading user sessions) from the business logic and controllers.
Non-Functional Requirements (Resiliency)
The application is built to handle network instability and API errors robustly.

Exponential Backoff and Retries: The core API communication logic implements an Exponential Backoff mechanism. If an API call fails with a transient error, the system will retry the request up to three times (MAX_RETRIES), doubling the wait time (500ms, 1000ms, 2000ms) between each attempt.

Concurrency: API calls are executed asynchronously using CompletableFuture to ensure the Swing UI remains responsive and non-blocking during network latency.

Cancellation: The application allows the user to explicitly Stop Generation, cleanly terminating the ongoing asynchronous API request.
Getting Started
Prerequisites
Java Development Kit (JDK) 21+

Maven

An OpenAI API Key

Configuration
Locate Configuration: Find the config.properties.example file in src/main/resources.

Rename/Copy: Rename/copy this file to config.properties.

Insert API Key: Open config.properties and replace the placeholder with your actual OpenAI Secret Key:

Properties

API_KEY=sk-YOUR_SECRET_KEY_HERE
Running the Application
Build: Use Maven to compile the project:

Bash

mvn clean install
Run: Execute the main class from your IDE (IntelliJ IDEA) or the command line:

Bash

java -cp target/classes org.example.Main
📝 Usage
Select Mode: Use the dropdown menu to choose a generation strategy (e.g., Creative Storytelling, Formal Academic Report).

Enter Prompt: Type your text prompt in the Your Input Prompt area.

Generate: Click the Generate Text button.

Manage Session: Use the File menu to Save Session (to persist your current strategy, input, and output) or Load Session.
