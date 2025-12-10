# GHCP-UST_Level2

Generate-a-Spring-Boot-API-with-CRUD-using-GitHub-Copilot
Overview
A step-by-step lab that shows how to generate a Spring Boot REST API with CRUD operations using GitHub Copilot inside your IDE (VS Code). The lab covers project creation, using Copilot prompts to scaffold code, implementing Entity/Repository/Service/Controller layers, running the app, testing endpoints, and pushing the project to GitHub.

Quick Plan (high-level steps)

Prepare environment and tools.
Create a new GitHub repo (or local repo).
Bootstrap a Spring Boot project using Spring Initializr.
Open project in VS Code and enable GitHub Copilot.
Use Copilot prompts to scaffold entity/repository/service/controller.
Run the app and test CRUD endpoints.
Commit and push to GitHub; optionally add CI.
Prerequisites

Java JDK 17 or later installed and JAVA_HOME set.
Maven (or use the Maven wrapper mvnw) or Gradle.
Git installed and configured (git config --global user.name and user.email).
VS Code (or IntelliJ) and GitHub Copilot extension enabled and signed in to GitHub.
A GitHub account and a repository to push to (or create one during the lab).
Optional: Postman, HTTPie, or curl for testing.
Repository layout (expected)

src/main/java/... : Spring Boot app sources
src/main/resources/application.properties
pom.xml (or build.gradle)
README.md (this file)
Detailed Step-by-step Instructions

Create the GitHub repository (or start locally)
Option A — create repo on GitHub.com:
Create a new public/private repo on github.com (e.g., spring-boot-copilot-crud).
Option B — initialize locally and push:
Open PowerShell in your working folder and run:
Bootstrap the Spring Boot project
Use Spring Initializr (https://start.spring.io/) or the Spring Initializr extension in VS Code.
Choose:
Project: Maven (or Gradle)
Language: Java
Spring Boot: 3.1.x (or compatible)
Packaging: Jar
Java: 17 (or 21 depending on your JDK)
Dependencies: Spring Web, Spring Data JPA, H2 Database (for lab), Spring Boot DevTools (optional)
Download generated project and unzip, or import directly in VS Code.
Open project in VS Code and enable Copilot
Open the project folder in VS Code.
Ensure the GitHub Copilot extension is installed and you are signed in.
Enable inline suggestions if not already enabled.
Create the domain model with Copilot
Create a package: com.example.demo.model
Create a Java class file Book.java and use Copilot to scaffold it by providing a short prompt at the top of the file, for example:
Copilot will suggest entity annotations and fields; accept or iterate as needed.
Example result to expect:
Create the repository
Create com.example.demo.repository.BookRepository.java
Prompt Copilot:
Expected skeleton:
Create the service layer
Create com.example.demo.service.BookService.java and BookServiceImpl.java
Example prompt for interface:
Example prompt for implementation:
Copilot will provide method implementations using bookRepository.
Create the REST controller
Create com.example.demo.controller.BookController.java
Prompt Copilot:
Expected endpoints:
GET /api/books — list all books
GET /api/books/{id} — get book by id
POST /api/books — create book
PUT /api/books/{id} — update book
DELETE /api/books/{id} — delete book
Add sample data (optional)
Use data.sql in src/main/resources or an ApplicationRunner bean to insert example rows at startup for quick testing.
Configure application.properties
For H2 in-memory DB and console:
Build and run the application
Using the Maven wrapper in PowerShell:
Or with Gradle wrapper:
Test the CRUD endpoints
Using curl (PowerShell): create a book
Get all books
Get a book by id
Update a book
Delete a book
Alternatively use Postman or HTTPie for easier UI.
Commit and push to GitHub
Example PowerShell commands:
(Optional) Add GitHub Actions CI
Create .github/workflows/ci.yml to build and test with Maven:
Copilot prompt examples (use directly in files or comments)

"Create a JPA entity Book with fields id Long, title String, author String, publishedDate LocalDate and Lombok annotations"
"Create a Spring Data JPA repository for Book"
"Create a service that returns List<Book> and Book by id and throws ResourceNotFoundException when not found"
"Create a REST controller for Book with typical CRUD endpoints and map to /api/books"
Best practices & tips

Ask Copilot for small, specific tasks rather than "write entire app" at once — shorter prompts produce more focused suggestions.
Review Copilot suggestions carefully for correctness and security.
Keep business logic in service layer; controller should be thin.
Add validation (@Valid, @NotNull) and exception handlers (@ControllerAdvice) after basic scaffolding.
Replace H2 with a persistent DB (Postgres/MySQL) for real projects.
Troubleshooting

If Copilot suggestions do not appear: confirm extension is installed, you are signed in, and inline suggestions are enabled in VS Code settings.
Common runtime issues:
Port already in use: change server port in application.properties (server.port=8081)
JPA errors: check spring.jpa.hibernate.ddl-auto setting and entity mapping annotations.
Appendix — Minimal controller example (what to expect from Copilot)

License and Attribution
