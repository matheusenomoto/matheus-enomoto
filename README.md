# Matheus Enomoto

## Portfolio Projects

Here are some of the projects I've developed, showcasing my experience across different domains and the use of software engineering best practices.

### 1. Authentication System with Design Patterns

![Python](https://img.shields.io/badge/Python-3.9%2B-blue?style=for-the-badge&logo=python&logoColor=white)

This project is a Python implementation of a flexible authentication system, designed to be scalable and easy to use. It serves as a practical demonstration of how to apply design patterns to create clean, decoupled, and maintainable code.

- **Repository:** [Authentication System](https://github.com/matheusenomoto/authentication-system)

#### Key Features:

* **Multiple Authentication Methods:** Supports local authentication (username/password), Google Sign-In, and GitHub Sign-In.
* **Simplified Interface:** The **Facade** pattern hides the complexity of the underlying authentication logic, offering a cohesive interface to the client.
* **Extensible:** The **Strategy** pattern allows new authentication methods (e.g., Facebook) to be added without modifying the existing core structure.
* **Single Control Point:** The **Singleton** pattern ensures a single instance of the authentication manager across the entire application, managing global access.

#### Technologies and Concepts:

* **Language:** Python  
* **Dependencies:** `requests`, `python-dotenv`  
* **Design Patterns:** Facade, Strategy, Singleton (demonstrated in `src/auth_facade.py` and `src/strategies/`)  
* **Database (Mock):** `src/mock_user_db.py`

#### Next Steps & AWS Integration (Solutions Architect Perspective):

This project is a strong foundation that can evolve into a cloud-native solution on AWS:

* **Amazon Cognito:** Would replace the current mock system, providing native user management and identity federation (Google, GitHub).
* **AWS Lambda & API Gateway:** The `AuthenticationFacade` logic could be deployed as a serverless Lambda function and exposed via API Gateway (`POST /auth`), creating a scalable microservice with no server management.
* **AWS Secrets Manager:** Third-party credentials (like Google/GitHub API keys) would be securely stored in Secrets Manager, avoiding hardcoding and improving security posture.
* **IAM Roles:** After successful authentication (especially via Cognito), the system could grant users temporary credentials with limited privileges via IAM Roles, allowing secure access to other AWS resources (S3, DynamoDB) without exposing long-term access keys.

---

### 2. Tax Calculator with Strategy Pattern

![Python](https://img.shields.io/badge/Python-3.9%2B-blue?style=for-the-badge&logo=python&logoColor=white)

This project demonstrates the practical application of the **Strategy** design pattern to build a flexible and scalable tax calculator. It supports dynamic switching of tax calculation algorithms, following clean code practices and the Open/Closed Principle from S.O.L.I.D.

- **Repository:** [Tax Calculator](https://github.com/matheusenomoto/tax_calculator)

#### Key Features:

* **Dynamic Calculations:** Allows the client to choose the tax type (e.g., ICMS, IRPF) at runtime, without complex `if/else` statements.
* **Easy Extensibility:** The **Strategy** pattern enables adding new tax types (ISS, IPI) simply by creating new strategy classes—no changes to the core calculator logic.
* **Decoupled Logic:** Each tax rule is encapsulated in its own class, isolating responsibilities and simplifying testing and maintenance.
* **Single Context Interface:** The client only interacts with the `TaxCalculator` class (Context), which manages the execution of the appropriate strategy.

#### Technologies and Concepts:

* **Language:** Python  
* **Design Pattern:** Strategy (demonstrated in `src/tax_calculator.py` and `src/strategies/`)  
* **S.O.L.I.D. Principles:** Applies the **Open/Closed Principle**  
* **Clean Code:** Focused on small, single-responsibility classes

#### Next Steps & AWS Integration (Solutions Architect Perspective):

This project serves as a great proof of concept for a cloud-native tax calculation microservice:

* **AWS Lambda & API Gateway:** The `TaxCalculator` logic can be deployed as a serverless function. A REST API (`POST /calculate`) would receive inputs (`{ "budget": 10000, "tax_type": "IRPF" }`) and return the result. This model is scalable and cost-efficient (pay-per-use).
* **Amazon DynamoDB:** Tax rules and brackets can be stored in DynamoDB. The Lambda function would query it to get the latest rules, enabling updates without code deployments.
* **AWS Step Functions:** For more complex calculations involving multiple steps, Step Functions can orchestrate a series of Lambda calls with proper sequencing and error handling.
* **AWS Systems Manager Parameter Store:** Global settings like default taxes or feature flags could be stored and easily accessed by the Lambda function.

---

### 3. To-Do List with MVC Architecture

![Python](https://img.shields.io/badge/Python-3.9%2B-blue?style=for-the-badge&logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-2.3%2B-black?style=for-the-badge&logo=flask&logoColor=white)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)

A simple task management app built in Python with Flask, demonstrating the implementation of the Model-View-Controller (MVC) architecture. This project focuses on separating responsibilities to ensure code organization, maintainability, and scalability.

- **Repository:** [To-Do List](https://github.com/matheusenomoto/to-do-list-mvc)

#### Key Features:

* **Task Management:** Add, complete, and delete tasks efficiently.
* **Intuitive Interface:** A clean and functional UI for interacting with the task list.
* **Separation of Concerns (MVC):**
    * **Model (`models/todo_list_model.py`):** Handles business logic and data interactions (a mock JSON file `tasks.json`). It is unaware of the UI.
    * **View (`templates/index.html`):** Handles UI rendering only. It receives data from the controller and does not contain business logic.
    * **Controller (`controllers/todo_controller.py`):** Intermediary that receives user requests, calls the model, and selects the appropriate view to display.

#### Technologies and Concepts:

* **Language:** Python  
* **Web Framework:** Flask  
* **Front-end:** HTML, CSS  
* **Data:** `tasks.json` (mock JSON file)

---
### 4. Network Routing Simulator

![Python](https://img.shields.io/badge/Python-3.9%2B-blue?style=for-the-badge&logo=python&logoColor=white)

This project serves as a compelling demonstration of applying fundamental software design patterns to solve a practical problem: simulating network routing. It highlights my ability to craft clean, modular, and extensible codebases.

- **Repository:** [Netork Routing Simulator](https://github.com/matheusenomoto/network-routing-simulator)

#### Architectural Principles & Design Patterns Demonstrated:

1.  **Strategy Pattern:**
    *   **Application:** Implemented via `RoutingStrategy` and `DijkstraStrategy`. The `Router` class is configured with a specific routing strategy at runtime, decoupling the routing logic from the router's core responsibilities.
    *   **Benefit:** Enables dynamic algorithm swapping (e.g., easily switching from Dijkstra to Bellman-Ford or a custom algorithm) without modifying existing code, adhering to the Open/Closed Principle.
2.  **Factory Method Pattern:**
    *   **Application:** The `RouterFactory` class centralizes the creation of `Router` objects.
    *   **Benefit:** Provides a single point of control for object instantiation, making it easy to introduce new router types (e.g., specialized routers with different capabilities) without affecting the `Network` class, which simply consumes routers from the factory.
3.  **Facade Pattern:**
    *   **Application:** The `NetworkSimulator` class acts as a simplified interface to the complex network subsystem.
    *   **Benefit:** Drastically reduces client-side complexity (`main.py`), abstracting away the intricate details of network topology building, routing table calculations, and packet simulation into a cohesive, easy-to-use API.
4.  **Layered/Modular Architecture:**
    *   **Application:** Code is organized into `core/`, `patterns/`, `facade.py`, and `main.py` directories.
    *   **Benefit:** Enforces a strong separation of concerns, leading to a highly maintainable, testable, and scalable codebase. Each layer has a distinct responsibility, improving code clarity and reducing interdependencies.

#### Key Learnings:

*   **Clean Code & Maintainability:** Focused on creating small, single-responsibility classes and modules, making the system easy to understand, debug, and extend.
*   **Extensibility:** Designed the system to easily accommodate new routing algorithms or future router types with minimal impact on the existing codebase.
*   **System Design:** Practiced architectural thinking by structuring the application to handle complexity gracefully and provide clear interfaces.
*   **Algorithmic Implementation:** Implemented Dijkstra's shortest path algorithm efficiently, handling graph traversals and path reconstruction.

### 5. NetGuardian - Network Monitor

![Python](https://img.shields.io/badge/Python-3.9%2B-blue?style=for-the-badge&logo=python&logoColor=white)

NetGuardian is an network traffic monitor, developed in Python, that exemplifies the application of **Clean Architecture** and modern design patterns. This project was designed to provide a robust, clear, extensible, and testable foundation for network analysis, demonstrating the ability to build systems with high maintainability and flexibility.

- **Repository:** [NetGuardian](https://github.com/matheusenomoto/netguardian)

#### Architecture and Applied Design Principles:

This project strictly adheres to the principles of **Clean Architecture**, promoting a separation of concerns that ensures decoupled and easily evolving code. The structure is divided into well-defined layers, with the **Dependency Rule** as the central pillar: source code dependencies always point inward, ensuring that the domain (the business core) remains untouched by implementation details:

*   **Domain Layer**: This is the innermost and most independent layer. It contains the essential business logic and the system's core entities, such as the representation of a `Packet`. It is completely free of frameworks or infrastructure details, focusing solely on the "what" of the problem to be solved.
*   **Application Layer**: Positioned just above the domain, this layer orchestrates the domain's operations to execute specific use cases. The `MonitorTrafficUseCase`, for example, resides here, defining how traffic monitoring should be performed, relying on domain abstractions to interact with packet capture and notify observers.
*   **Infrastructure Layer**: The outermost layer, which encapsulates all implementation details and external dependencies, such as I/O libraries, file access, configurations, and specific frameworks (e.g., `scapy` for packet capture). It implements the interfaces (abstractions) defined in the inner layers, ensuring that the application's core is not affected by technological changes.

### Beyond Clean Architecture, NetGuardian effectively illustrates the application of several design patterns:

1.  **Observer Pattern**: Used for a highly extensible event notification system. The central `Observable` notifies multiple "observers" (`PacketObserver`) each time a new packet is captured. This allows for adding new analysis or presentation functionalities (like `ConsolePresenter`, `FileLogger`, `TrafficAnalyzer`) without modifying the central packet capture logic. This follows the Open/Closed Principle of S.O.L.I.D.
2.  **Dependency Inversion Principle (DIP)**: This principle is fundamental in NetGuardian. The `MonitorTrafficUseCase` (in the application layer) does not depend on concrete packet capture implementations (like `ScapyPacketCapture`), but rather on an abstraction (`PacketCapture`). The concrete implementations are "injected" into the use case at the **Composition Root**, located in `main.py`. This inversion ensures that the application's core is independent of the underlying technology used to capture packets, facilitating testing and future replacements.
3.  **Composition Root**: The `main.py` file acts as the application's composition root. This is where all concrete classes are instantiated and "wired" together. This approach centralizes the system's configuration, making it more understandable and manageable, and is a key aspect of implementing Dependency Inversion.

#### Key Features:

*   **Real-Time Packet Capture**: The system can monitor live network traffic, processing packets as they are detected.
*   **Highly Configurable**: Allows the user to easily define the network interface to monitor and logging preferences (such as enabling or disabling file logging and specifying the log file name) through a `config.ini` file.
*   **Extensible Observer Modules**: Thanks to the Observer pattern, different modules can react to captured packets:
    *   `ConsolePresenter`: Displays detailed information for each captured packet directly in the console, in real-time.
    *   `FileLogger`: Logs all packet data to a CSV file, allowing for offline analysis and auditing.
    *   `TrafficAnalyzer`: Performs a basic traffic analysis, summarizing data volume by source IP address and presenting a concise report at the end of the monitoring session.
*   **High Testability**: The architecture and use of abstractions make each system component isolated and easily testable. The `tests/` directory contains examples of unit tests using `pytest`, ensuring code robustness.
*   **Graceful Shutdown**: The system safely manages interruptions (e.g., via `Ctrl+C`), ensuring that resources are released correctly (like closing the log file) and that a final report is generated by the `TrafficAnalyzer` before exiting.

#### Technologies and Concepts:

*   **Language:** Python
*   **Packet Capture Library:** `scapy` (used for the infrastructure capture interface)
*   **Testing Framework:** `pytest`
*   **Architectural Pattern:** Clean Architecture
*   **Design Patterns:** Observer, Dependency Inversion

#### Configuration and Execution:

To operate NetGuardian, it must be run with root/administrator privileges, as packet capture requires special access to the network interface. The project includes clear instructions for cloning the repository, creating an isolated virtual environment, installing dependencies via `requirements.txt`, and configuring the `config.ini`.

## My Personal Blog

<!-- Backend -->
![Node.js](https://img.shields.io/badge/Node.js-43853D?style=for-the-badge&logo=node.js&logoColor=white)
![Express.js](https://img.shields.io/badge/Express.js-000000?style=for-the-badge&logo=express&logoColor=white)

<!-- Database -->
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white)

<!-- Template Engine -->
![EJS](https://img.shields.io/badge/EJS-A91F26?style=for-the-badge)

<!-- Content Management -->
![Amazon S3](https://img.shields.io/badge/Amazon_S3-569A31?style=for-the-badge&logo=amazon-s3&logoColor=white)

<!-- Authentication -->
![JWT](https://img.shields.io/badge/JWT-000000?style=for-the-badge&logo=json-web-tokens&logoColor=white)
![bcrypt](https://img.shields.io/badge/bcrypt-black?style=for-the-badge)

<!-- Misc -->
![Lucide](https://img.shields.io/badge/Lucide-2E8B57?style=for-the-badge)

<!-- AWS Infra -->
![AWS](https://img.shields.io/badge/AWS-232F3E?style=for-the-badge&logo=amazon-aws&logoColor=white)
![Amazon EC2](https://img.shields.io/badge/Amazon_EC2-FF9900?style=for-the-badge&logo=amazon-ec2&logoColor=white)
![Amazon VPC](https://img.shields.io/badge/Amazon_VPC-FF9900?style=for-the-badge&logo=amazon-vpc&logoColor=white)
![Amazon Route 53](https://img.shields.io/badge/Amazon_Route_53-FF9900?style=for-the-badge&logo=amazon-route53&logoColor=white)
![ALB](https://img.shields.io/badge/ALB-FF9900?style=for-the-badge)

I maintain a blog where I share my studies, thoughts, and experiments in the tech world. It’s a space to document my learning journey and share insights on topics like Full Stack development, solution architecture, cloud computing, and FTTx networks.

- **Visit the Blog:** [Blog](https://www.matheusenomoto.com)

#### Built With:

Although the source code repository is private, the blog is built using the following technologies:

* **Backend:** Node.js, Express.js  
* **Database:** PostgreSQL  
* **Template Engine:** EJS  
* **Content Management:** Article storage in AWS S3  
* **Authentication:** JWT, bcrypt, cookie-parser  
* **Others:** `cors`, `env-var`, `lucide`, `uuid`  
* **AWS Infrastructure:** IAM, VPC, Route 53, ACM, ALB, S3, EC2

---

## Connect With Me

I'm always open to tech discussions. Feel free to connect:

* **LinkedIn:** [https://www.linkedin.com/in/matheus-lopes-enomoto](https://www.linkedin.com/in/matheus-lopes-enomoto)  
* **Email:** matheusenomoto@gmail.com  
* **Phone:** +55 41 99929 3255 (Feel free to reach out!)

