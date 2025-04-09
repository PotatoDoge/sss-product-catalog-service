SmartShoppingSystem-backend
===========================

A cloud-native microservices-based backend for a smart shopping experience. Built using Spring Boot, containerized with Docker, orchestrated with Kubernetes, and integrated with Kafka for event-driven communication. This system is designed for scalability, maintainability, and extensibility using modern architectural patterns like Hexagonal and Onion Architecture.

Project Structure
-----------------

SmartShoppingSystem-backend/\
├── recommendation-service/    # Handles product recommendations (Hexagonal)\
├── product-catalog-service/   # Manages products and inventory (Hexagonal)\
├── user-service/              # Manages users and preferences (Onion)\
├── kubernetes/                # Kubernetes manifests (Deployments, Services, etc.)\
├── docker/                    # Docker-related config (Docker Compose, Dockerfiles)\
└── README.md                  # This file

---

## Technologies Used

| Technology           | Purpose                                      |
|----------------------|----------------------------------------------|
| **Spring Boot**      | Microservices framework                      |
| **Kafka**            | Asynchronous event-based communication       |
| **REST APIs**        | Synchronous communication between services   |
| **Docker**           | Containerization                              |
| **Kubernetes**       | Orchestration and deployment                 |
| **PostgreSQL**       | Data persistence                             |
| **Hexagonal Arch**   | Used in Recommendation and Catalog Services  |
| **Onion Arch**       | Used in User Service                         |

---

## Microservices Overview

### 1. Recommendation Service (Hexagonal)

- **Responsibilities**:
    - Consumes user activity events via Kafka
    - Provides product recommendations through REST API
    - Clean separation of core logic from infrastructure via ports and adapters

### 2. Product Catalog Service (Hexagonal)

- **Responsibilities**:
    - Manages products, stock, and categories
    - Publishes Kafka events when products are updated
    - Exposes REST APIs for querying product data

### 3. User Service (Onion)

- **Responsibilities**:
    - Manages user accounts, preferences, and profiles
    - Sends REST requests to the Recommendation Service for personalized feeds
    - Core domain logic isolated in the inner circle

---

## Communication Patterns

### Kafka Topics:
- `user.activity`: Produced by **User Service** and consumed by **Recommendation Service**.
- `product.events`: Produced by **Product Catalog Service** and consumed by **Recommendation Service**.

### REST Endpoints:
- **User Service** → **Recommendation Service**: For fetching personalized product feeds.
- **Recommendation Service** → **Product Catalog Service**: For enriching product details.

---

## Running the System

### Local Development (Docker Compose)

1. Navigate to the `docker` directory:
    ```bash
    cd docker
    ```

2. Build and start all services:
    ```bash
    docker-compose up --build
    ```

This includes:
- All 3 microservices
- Kafka & Zookeeper
- PostgreSQL (one instance for each service)

### Kubernetes Deployment

1. Apply Kubernetes configuration to your cluster:
    ```bash
    kubectl apply -f kubernetes/
    ```

**Note**: Make sure you have a local Kubernetes cluster running (Minikube, k3d, etc.).

---

## Getting Started with Development

1. **Clone the repository**:
    ```bash
    git clone https://github.com/yourusername/SmartShoppingSystem-backend.git
    ```

2. **Navigate to the service folder** (e.g., `user-service`):
    ```bash
    cd user-service
    ```

3. **Build and run the service**:
    ```bash
    ./mvnw clean install   # For Maven-based projects
    # OR
    ./gradlew build        # For Gradle-based projects
    ```

4. Once built, you can run the service with:
    ```bash
    java -jar target/user-service.jar
    ```

---

## License

MIT License (or specify your own license).

---

## Contributors

- **Your Name**
- **Collaborators**

---

Thank you for checking out **SmartShoppingSystem-backend**!
