# BambangShop Publisher App
Tutorial and Example for Advanced Programming 2024 - Faculty of Computer Science, Universitas Indonesia

---

## About this Project
In this repository, we have provided you a REST (REpresentational State Transfer) API project using Rocket web framework.

This project consists of four modules:
1.  `controller`: this module contains handler functions used to receive request and send responses.
    In Model-View-Controller (MVC) pattern, this is the Controller part.
2.  `model`: this module contains structs that serve as data containers.
    In MVC pattern, this is the Model part.
3.  `service`: this module contains structs with business logic methods.
    In MVC pattern, this is also the Model part.
4.  `repository`: this module contains structs that serve as databases and methods to access the databases.
    You can use methods of the struct to get list of objects, or operating an object (create, read, update, delete).

This repository provides a basic functionality that makes BambangShop work: ability to create, read, and delete `Product`s.
This repository already contains a functioning `Product` model, repository, service, and controllers that you can try right away.

As this is an Observer Design Pattern tutorial repository, you need to implement another feature: `Notification`.
This feature will notify creation, promotion, and deletion of a product, to external subscribers that are interested of a certain product type.
The subscribers are another Rocket instances, so the notification will be sent using HTTP POST request to each subscriber's `receive notification` address.

## API Documentations

You can download the Postman Collection JSON here: https://ristek.link/AdvProgWeek7Postman

After you download the Postman Collection, you can try the endpoints inside "BambangShop Publisher" folder.
This Postman collection also contains endpoints that you need to implement later on (the `Notification` feature).

Postman is an installable client that you can use to test web endpoints using HTTP request.
You can also make automated functional testing scripts for REST API projects using this client.
You can install Postman via this website: https://www.postman.com/downloads/

## How to Run in Development Environment
1.  Set up environment variables first by creating `.env` file.
    Here is the example of `.env` file:
    ```bash
    APP_INSTANCE_ROOT_URL="http://localhost:8000"
    ```
    Here are the details of each environment variable:
    | variable              | type   | description                                                |
    |-----------------------|--------|------------------------------------------------------------|
    | APP_INSTANCE_ROOT_URL | string | URL address where this publisher instance can be accessed. |
2.  Use `cargo run` to run this app.
    (You might want to use `cargo check` if you only need to verify your work without running the app.)

## Mandatory Checklists (Publisher)
-   [ ] Clone https://gitlab.com/ichlaffterlalu/bambangshop to a new repository.
-   **STAGE 1: Implement models and repositories**
    -   [x] Commit: `Create Subscriber model struct.`
    -   [x] Commit: `Create Notification model struct.`
    -   [x] Commit: `Create Subscriber database and Subscriber repository struct skeleton.`
    -   [x] Commit: `Implement add function in Subscriber repository.`
    -   [x] Commit: `Implement list_all function in Subscriber repository.`
    -   [x] Commit: `Implement delete function in Subscriber repository.`
    -   [x] Write answers of your learning module's "Reflection Publisher-1" questions in this README.
-   **STAGE 2: Implement services and controllers**
    -   [x] Commit: `Create Notification service struct skeleton.`
    -   [x] Commit: `Implement subscribe function in Notification service.`
    -   [x] Commit: `Implement subscribe function in Notification controller.`
    -   [x] Commit: `Implement unsubscribe function in Notification service.`
    -   [x] Commit: `Implement unsubscribe function in Notification controller.`
    -   [x] Write answers of your learning module's "Reflection Publisher-2" questions in this README.
-   **STAGE 3: Implement notification mechanism**
    -   [x] Commit: `Implement update method in Subscriber model to send notification HTTP requests.`
    -   [x] Commit: `Implement notify function in Notification service to notify each Subscriber.`
    -   [x] Commit: `Implement publish function in Program service and Program controller.`
    -   [x] Commit: `Edit Product service methods to call notify after create/delete.`
    -   [x] Write answers of your learning module's "Reflection Publisher-3" questions in this README.

## Your Reflections
This is the place for you to write reflections:

### Mandatory (Publisher) Reflections

#### Reflection Publisher-1
1. We may skip the interface for the Observer pattern if we're looking for simplicity and we're sure things won't change much. However, an interface gives us a neat flexibility for the future, making it easier to expand and swap things out.

2. Vec or DashMap?: If we're keeping a small list and don't care much about the speed of checking or updating items, a Vec might do just fine. But if our list is growing and we want quick lookups and updates, DashMap is our friend because it does all that efficiently

3. DashMap or Singleton pattern?: DashMap is built to handle multiple threads without breaking a sweat, which is super handy in Rust. Singleton could work, but it's more about limiting ourself to one instance than managing threads. So, unless we have a strong reason to restrict to a single instance, DashMap is usually the better choice in Rust for keeping things thread-safe without the extra hassle.


#### Reflection Publisher-2
1. Why separate Service and Repository from Model?: The separation is key for ensuring the code is easier to maintain, scale, and test, adhering to fundamental design principles like the Single Responsibility Principle (SRP), Separation of Concerns (SoC), and Don't Repeat Yourself (DRY). It enables a cleaner organization of code, simplifies maintenance, and better accommodates changes as the system grows more complex.

2. What if only Model is used?: Relying solely on the Model would likely bloat its responsibilities, compounding complexity and diminishing maintainability and modularity. Models would then be overburdened with both business logic and data access tasks, leading to a convoluted codebase that's tougher to expand or alter.

3. How does Postman contibute?: Postman streamlines the process of testing API endpoints. It simplifies making calls to the endpoints, allowing one to verify if the program operates as expected. The most appreciated feature of Postman is the ability to organize endpoints into collections for easy testing and even to automate these tests, enhancing efficiency.

#### Reflection Publisher-3
1. Which variation of pattern is implemented?: The implementation uses the push variation of the observer pattern. Here, the NotificationService functions as the subject, actively sending updates to its observers (Subscribers) whenever there's a change.

2. What are the benefits of using the observer pattern in this tutorial?: Opting for the pull method in the observer pattern helps simplify the system as the subject isn't required to keep track of its observers. Moreover, this approach enhances scalability because observers pull updates only when necessary, freeing the subject from the need to simultaneously push updates to all observers.

3. What are the implications of not using multi-threading?: Without multi-threading, sending notifications can become markedly slower, especially with many users accessing the application simultaneously. Additionally, the available hardware resources are not fully leveraged, potentially leading to inefficiencies.