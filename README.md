SmartShoppingSystem-backend
===========================

A cloud-native microservices-based backend for a smart shopping experience. Built using Spring Boot, containerized with Docker, orchestrated with Kubernetes, and integrated with Kafka for event-driven communication. This system is designed for scalability, maintainability, and extensibility using modern architectural patterns like Hexagonal and Onion Architecture.

Project Structure
-----------------

SmartShoppingSystem-backend/\
├── recommendation-service/    # Handles product recommendations (Hexagonal)\
├── **product-catalog-service**/   # Manages products and inventory (Hexagonal)\
├── user-service/              # Manages users and preferences (Onion)

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

# Product Catalog Service

The **Product Catalog Service** is a core component of the SmartShoppingSystem. It is responsible for managing all product-related data and exposing APIs for other services and clients to interact with the product catalog. The service is designed following the **Hexagonal Architecture**, ensuring a clean separation between domain logic and infrastructure concerns.

---

## 🧠 Responsibilities

- Manage products, inventory, and categories.
- Provide RESTful endpoints for product operations.
- Publish Kafka events when product data changes (e.g., create/update/delete).
- Integrate with a PostgreSQL database for data persistence.

---

## 🧱 Architecture Overview

The service follows **Hexagonal (Ports and Adapters) Architecture**, which includes:

- **Domain Layer**: Business logic and core models.
- **Application Layer**: Use cases and service orchestration.
- **Adapters**:
    - **Inbound**: REST controllers.
    - **Outbound**: Repositories (JPA), Kafka producers.
- **Ports**: Interfaces used by the domain to abstract infrastructure.

---

## 📡 REST Endpoints

| Method | Endpoint             | Description              |
|--------|----------------------|--------------------------|
| GET    | `/products`          | Get all products         |
| GET    | `/products/{id}`     | Get a product by ID      |
| POST   | `/products`          | Create a new product     |
| PUT    | `/products/{id}`     | Update an existing product |
| DELETE | `/products/{id}`     | Delete a product         |

---

## 🔄 Kafka Integration

- **Topic**: `product.events`
- **Event Types**:
    - `ProductCreated`
    - `ProductUpdated`
    - `ProductDeleted`

These events can be consumed by services like the **Recommendation Service** to keep product information in sync.

---

## ⚙️ How to Run Locally

1. **Navigate to the service folder**:
   ```bash
   cd product-catalog-service

1. **Build the service:r**:
   ```bash
   ./mvnw clean install

1. **Run the service:**:
   ```bash
   ./mvnw spring-boot:run


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

## Contributors

- https://github.com/PotatoDoge

---

Thank you for checking out **SmartShoppingSystem-backend**!
