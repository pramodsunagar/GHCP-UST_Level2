# GHCP-UST_Level2

Here's the README.md content for the lab. At the top I list clear, actionable steps, then detailed instructions, Copilot prompt examples, test commands, and troubleshooting notes. Copy this into `README.md` and upload to GitHub.

# Generate-a-Spring-Boot-API-with-CRUD-using-GitHub-Copilot

Overview
A step-by-step lab that shows how to generate a Spring Boot REST API with CRUD operations using GitHub Copilot inside your IDE (VS Code). The lab covers project creation, using Copilot prompts to scaffold code, implementing Entity/Repository/Service/Controller layers, running the app, testing endpoints, and pushing the project to GitHub.

Quick Plan (high-level steps)
1. Prepare environment and tools.
2. Create a new GitHub repo (or local repo).
3. Bootstrap a Spring Boot project using Spring Initializr.
4. Open project in VS Code and enable GitHub Copilot.
5. Use Copilot prompts to scaffold entity/repository/service/controller.
6. Run the app and test CRUD endpoints.
7. Commit and push to GitHub; optionally add CI.

Prerequisites
- Java JDK 17 or later installed and `JAVA_HOME` set.
- Maven (or use the Maven wrapper `mvnw`) or Gradle.
- Git installed and configured (`git config --global user.name` and `user.email`).
- VS Code (or IntelliJ) and GitHub Copilot extension enabled and signed in to GitHub.
- A GitHub account and a repository to push to (or create one during the lab).
- Optional: Postman, HTTPie, or curl for testing.

Repository layout (expected)
- `src/main/java/...` : Spring Boot app sources
- `src/main/resources/application.properties`
- `pom.xml` (or `build.gradle`)
- `README.md` (this file)

Detailed Step-by-step Instructions

1) Create the GitHub repository (or start locally)
- Option A — create repo on GitHub.com:
  - Create a new public/private repo on `github.com` (e.g., `spring-boot-copilot-crud`).
- Option B — initialize locally and push:
  - Open PowerShell in your working folder and run:
```powershell
git init
git remote add origin https://github.com/<your-username>/spring-boot-copilot-crud.git
```

2) Bootstrap the Spring Boot project
- Use Spring Initializr (https://start.spring.io/) or the Spring Initializr extension in VS Code.
- Choose:
  - Project: `Maven` (or `Gradle`)
  - Language: `Java`
  - Spring Boot: `3.1.x` (or compatible)
  - Packaging: `Jar`
  - Java: `17` (or 21 depending on your JDK)
  - Dependencies: `Spring Web`, `Spring Data JPA`, `H2 Database` (for lab), `Spring Boot DevTools` (optional)
- Download generated project and unzip, or import directly in VS Code.

3) Open project in VS Code and enable Copilot
- Open the project folder in VS Code.
- Ensure the GitHub Copilot extension is installed and you are signed in.
- Enable inline suggestions if not already enabled.

4) Create the domain model with Copilot
- Create a package: `com.example.demo.model`
- Create a Java class file `Book.java` and use Copilot to scaffold it by providing a short prompt at the top of the file, for example:
```java
// Create a JPA entity Book with fields id Long, title String, author String, publishedDate LocalDate
```
- Copilot will suggest entity annotations and fields; accept or iterate as needed.
- Example result to expect:
```java
@Entity
@Table(name = "books")
public class Book {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String title;
    private String author;
    private LocalDate publishedDate;
    // getters and setters
}
```

5) Create the repository
- Create `com.example.demo.repository.BookRepository.java`
- Prompt Copilot:
```java
// Create a Spring Data JPA repository for Book entity
```
- Expected skeleton:
```java
public interface BookRepository extends JpaRepository<Book, Long> { }
```

6) Create the service layer
- Create `com.example.demo.service.BookService.java` and `BookServiceImpl.java`
- Example prompt for interface:
```java
// Define a BookService interface with methods: List<Book> findAll(), Book findById(Long id), Book save(Book book), Book update(Long id, Book book), void delete(Long id)
```
- Example prompt for implementation:
```java
// Implement BookService using BookRepository and throw a ResourceNotFoundException when id not found
```
- Copilot will provide method implementations using `bookRepository`.

7) Create the REST controller
- Create `com.example.demo.controller.BookController.java`
- Prompt Copilot:
```java
// Create a REST controller for Book with endpoints: GET /api/books, GET /api/books/{id}, POST /api/books, PUT /api/books/{id}, DELETE /api/books/{id}
```
- Expected endpoints:
  - `GET /api/books` — list all books
  - `GET /api/books/{id}` — get book by id
  - `POST /api/books` — create book
  - `PUT /api/books/{id}` — update book
  - `DELETE /api/books/{id}` — delete book

8) Add sample data (optional)
- Use `data.sql` in `src/main/resources` or an `ApplicationRunner` bean to insert example rows at startup for quick testing.

9) Configure `application.properties`
- For H2 in-memory DB and console:
```properties
spring.datasource.url=jdbc:h2:mem:demo;DB_CLOSE_DELAY=-1;DB_CLOSE_ON_EXIT=FALSE
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=
spring.jpa.hibernate.ddl-auto=update
spring.h2.console.enabled=true
spring.h2.console.path=/h2-console
```

10) Build and run the application
- Using the Maven wrapper in PowerShell:
```powershell
.\mvnw.cmd clean package
.\mvnw.cmd spring-boot:run
```
- Or with Gradle wrapper:
```powershell
.\gradlew.bat bootRun
```

11) Test the CRUD endpoints
- Using `curl` (PowerShell): create a book
```powershell
curl -H "Content-Type: application/json" -d '{"title":"Clean Code","author":"Robert C. Martin","publishedDate":"2008-08-01"}' http://localhost:8080/api/books -Method Post
```
- Get all books
```powershell
curl http://localhost:8080/api/books
```
- Get a book by id
```powershell
curl http://localhost:8080/api/books/1
```
- Update a book
```powershell
curl -H "Content-Type: application/json" -d '{"title":"Clean Code - Updated","author":"Robert C. Martin","publishedDate":"2008-08-01"}' http://localhost:8080/api/books/1 -Method Put
```
- Delete a book
```powershell
curl http://localhost:8080/api/books/1 -Method Delete
```
- Alternatively use Postman or HTTPie for easier UI.

12) Commit and push to GitHub
- Example PowerShell commands:
```powershell
git add .
git commit -m "feat: scaffold Spring Boot CRUD API using GitHub Copilot"
git branch -M main
git remote add origin https://github.com/<your-username>/spring-boot-copilot-crud.git
git push -u origin main
```

13) (Optional) Add GitHub Actions CI
- Create `.github/workflows/ci.yml` to build and test with Maven:
```yaml
name: Java CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Set up JDK 17
        uses: actions/setup-java@v4
        with:
          java-version: '17'
          distribution: temurin
      - name: Build with Maven
        run: mvn -B -DskipTests clean package
```

Copilot prompt examples (use directly in files or comments)
- "Create a JPA entity Book with fields id Long, title String, author String, publishedDate LocalDate and Lombok annotations"
- "Create a Spring Data JPA repository for Book"
- "Create a service that returns List<Book> and Book by id and throws ResourceNotFoundException when not found"
- "Create a REST controller for Book with typical CRUD endpoints and map to /api/books"

Best practices & tips
- Ask Copilot for small, specific tasks rather than "write entire app" at once — shorter prompts produce more focused suggestions.
- Review Copilot suggestions carefully for correctness and security.
- Keep business logic in service layer; controller should be thin.
- Add validation (`@Valid`, `@NotNull`) and exception handlers (`@ControllerAdvice`) after basic scaffolding.
- Replace H2 with a persistent DB (Postgres/MySQL) for real projects.

Troubleshooting
- If Copilot suggestions do not appear: confirm extension is installed, you are signed in, and inline suggestions are enabled in VS Code settings.
- Common runtime issues:
  - Port already in use: change server port in `application.properties` (`server.port=8081`)
  - JPA errors: check `spring.jpa.hibernate.ddl-auto` setting and entity mapping annotations.

Appendix — Minimal controller example (what to expect from Copilot)
```java
@RestController
@RequestMapping("/api/books")
public class BookController {

  private final BookService bookService;

  public BookController(BookService bookService) {
    this.bookService = bookService;
  }

  @GetMapping
  public List<Book> getAll() {
    return bookService.findAll();
  }

  @GetMapping("/{id}")
  public ResponseEntity<Book> getById(@PathVariable Long id) {
    return ResponseEntity.ok(bookService.findById(id));
  }

  @PostMapping
  public ResponseEntity<Book> create(@RequestBody @Valid Book book) {
    Book saved = bookService.save(book);
    return ResponseEntity.status(HttpStatus.CREATED).body(saved);
  }

  @PutMapping("/{id}")
  public ResponseEntity<Book> update(@PathVariable Long id, @RequestBody @Valid Book book) {
    return ResponseEntity.ok(bookService.update(id, book));
  }

  @DeleteMapping("/{id}")
  public ResponseEntity<Void> delete(@PathVariable Long id) {
    bookService.delete(id);
    return ResponseEntity.noContent().build();
  }
}
```

License and Attribution
- This lab doc is for teaching and demo purposes. Adapt code and dependencies to your project’s license and security requirements.
- When using Copilot-generated code in public repos, follow GitHub Copilot licensing and disclosure recommendations.

