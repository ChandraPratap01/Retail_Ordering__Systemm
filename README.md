# 🍕 Retail Ordering Platform

> A full-stack retail ordering system for Pizza, Cold Drinks & Breads.
> Customers can browse, cart, order and track. Admins can manage products, inventory and orders — all in one platform.

![Status](https://img.shields.io/badge/Status-Complete-brightgreen)
![Java](https://img.shields.io/badge/Java-17-orange)
![SpringBoot](https://img.shields.io/badge/Spring%20Boot-3.3.x-6DB33F)
![React](https://img.shields.io/badge/React-18-61DAFB)
![Vite](https://img.shields.io/badge/Vite-5.x-646CFF)
![MySQL](https://img.shields.io/badge/MySQL-8.x-4479A1)
![License](https://img.shields.io/badge/Classification-Internal-lightgrey)

---

## 📌 Table of Contents

- [Project Overview](#-project-overview)
- [Tech Stack](#-tech-stack)
- [Features](#-features)
- [Project Structure](#-project-structure)
  - [Backend Structure](#backend-structure-ordering)
  - [Frontend Structure](#frontend-structure-retailfrontend)
- [Getting Started](#-getting-started)
  - [Prerequisites](#prerequisites)
  - [Database Setup](#database-setup)
  - [Backend Setup](#backend-setup)
  - [Frontend Setup](#frontend-setup)
- [Configuration](#-configuration)
- [Frontend Routes](#-frontend-routes)
- [API Reference](#-api-reference)
  - [Auth APIs](#auth-apis)
  - [Category APIs](#category-apis)
  - [Product APIs](#product-apis)
  - [Cart APIs](#cart-apis)
  - [Order APIs](#order-apis)
  - [Inventory APIs](#inventory-apis)
- [Database Schema](#-database-schema)
- [Core Business Flow](#-core-business-flow)
- [Security](#-security)
- [MVP Scope](#-mvp-scope)
- [Author](#-author)

---

## 📖 Project Overview

The **Retail Ordering Platform** is a complete full-stack web application where:

- **Customers** can register, log in, browse the menu by category (Pizza / Cold Drinks / Breads), add items to cart, place orders, and track their order status in real time.
- **Admins** can manage products, categories, inventory stock levels, and update order statuses through a dedicated dashboard.

The backend is a REST API built with **Spring Boot + MySQL**, and the frontend is a **React + Vite** SPA. Both are fully connected and running.

---

## 🛠 Tech Stack

### Backend

| Layer | Technology |
|---|---|
| Framework | Spring Boot 3.3.x |
| Language | Java 17 |
| Database | MySQL 8.x |
| ORM | Spring Data JPA / Hibernate |
| Build Tool | Maven |
| Validation | Spring Validation (`@Valid`, `@NotBlank`, `@Min`) |
| Boilerplate | Lombok (`@Data`, `@Builder`, `@RequiredArgsConstructor`) |
| API Docs | Springdoc OpenAPI / Swagger UI 2.5.0 |
| Auth (ready) | JWT + Spring Security *(disabled for demo — see Security section)* |

### Frontend

| Layer | Technology |
|---|---|
| Framework | React 18 |
| Build Tool | Vite 5.x |
| HTTP Client | Axios |
| Routing | React Router DOM |
| State Management | React Context API (`AuthContext`) |
| Notifications | Toast Notifications |
| Styling | CSS (`App.css`, `index.css`) |

---

## ✨ Features

### Customer Features
- 🔐 Register and Login with session management via `AuthContext`
- 🍕 Browse full product menu with **category filter** (Pizza / Cold Drinks / Breads)
- 🛒 Full cart management — add, update quantity, remove items
- ✅ Place orders with **automatic stock validation**
- 📦 View order confirmation with full item breakdown
- 📋 Order history with status tracking
- 🔍 View individual order details

### Admin Features
- 📊 Admin Dashboard — overview of platform activity
- 🗂 Manage Categories — create, edit, delete
- 📦 Manage Products — add, update, soft-delete products
- 🏭 Inventory Management — view and update stock levels per product
- 🚚 Order Management — view all orders, update order statuses

### Platform Features
- 🔔 Toast notifications for all user actions (success, error, info)
- ⚡ Fast SPA experience with Vite
- 📄 Swagger UI for API exploration and testing
- 🔄 Auto inventory deduction on order confirmation
- 💾 Price snapshot on order items (prevents price drift on historical orders)

---

## 📁 Project Structure

### Backend Structure (`ordering/`)

```
ordering/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/retail/ordering/
│   │   │       │
│   │   │       ├── config/                          ← Security & API config
│   │   │       │   ├── JwtFilter.java               ← JWT request filter (disabled)
│   │   │       │   ├── JwtUtil.java                 ← JWT generate & validate (disabled)
│   │   │       │   ├── SecurityConfig.java          ← Spring Security config (disabled)
│   │   │       │   └── SwaggerConfig.java           ← OpenAPI / Swagger setup
│   │   │       │
│   │   │       ├── controller/                      ← REST Controllers
│   │   │       │   ├── AdminInventoryController.java
│   │   │       │   ├── AuthController.java
│   │   │       │   ├── CartController.java
│   │   │       │   ├── CategoryController.java
│   │   │       │   ├── OrderController.java
│   │   │       │   └── ProductController.java
│   │   │       │
│   │   │       ├── dto/
│   │   │       │   ├── request/                     ← Incoming request bodies
│   │   │       │   │   ├── CartRequestDto.java
│   │   │       │   │   ├── CategoryRequestDto.java
│   │   │       │   │   ├── InventoryRequestDto.java
│   │   │       │   │   ├── LoginRequestDto.java
│   │   │       │   │   ├── ProductRequestDto.java
│   │   │       │   │   └── RegisterRequestDto.java
│   │   │       │   │
│   │   │       │   └── response/                    ← Outgoing response bodies
│   │   │       │       ├── ApiResponseDto.java
│   │   │       │       ├── AuthResponseDto.java
│   │   │       │       ├── CartItemResponseDto.java
│   │   │       │       ├── CartResponseDto.java
│   │   │       │       ├── CategoryResponseDto.java
│   │   │       │       ├── InventoryResponseDto.java
│   │   │       │       ├── OrderItemResponseDto.java
│   │   │       │       ├── OrderResponseDto.java
│   │   │       │       └── ProductResponseDto.java
│   │   │       │
│   │   │       ├── entity/                          ← JPA Entities
│   │   │       │   ├── Cart.java
│   │   │       │   ├── CartItem.java
│   │   │       │   ├── Category.java
│   │   │       │   ├── Inventory.java
│   │   │       │   ├── Order.java
│   │   │       │   ├── OrderItem.java
│   │   │       │   ├── Product.java
│   │   │       │   └── User.java
│   │   │       │
│   │   │       ├── exception/                       ← Error handling
│   │   │       │   ├── BadRequestException.java
│   │   │       │   ├── GlobalExceptionHandler.java
│   │   │       │   └── ResourceNotFoundException.java
│   │   │       │
│   │   │       ├── repository/                      ← JPA Repositories
│   │   │       │   ├── CartItemRepository.java
│   │   │       │   ├── CartRepository.java
│   │   │       │   ├── CategoryRepository.java
│   │   │       │   ├── InventoryRepository.java
│   │   │       │   ├── OrderRepository.java
│   │   │       │   ├── ProductRepository.java
│   │   │       │   └── UserRepository.java
│   │   │       │
│   │   │       ├── service/                         ← Business Logic
│   │   │       │   ├── AuthService.java
│   │   │       │   ├── CartService.java
│   │   │       │   ├── CategoryService.java
│   │   │       │   ├── InventoryService.java
│   │   │       │   ├── OrderService.java
│   │   │       │   └── ProductService.java
│   │   │       │
│   │   │       └── OrderingApplication.java         ← Entry point
│   │   │
│   │   └── resources/
│   │       ├── static/
│   │       │   ├── app.js
│   │       │   ├── index.html
│   │       │   └── styles.css
│   │       ├── templates/
│   │       └── application.properties
│   │
│   └── test/
│
├── target/
├── .gitattributes
├── .gitignore
├── HELP.md
├── mvnw
├── mvnw.cmd
└── pom.xml
```

---

### Frontend Structure (`retailfrontend/`)

```
retailfrontend/
├── public/
├── src/
│   ├── api/
│   │   └── axios.js                  ← Axios instance (base URL + headers)
│   │
│   ├── assets/                       ← Static assets (images, icons)
│   │
│   ├── context/
│   │   └── AuthContext.jsx           ← Global auth state (user, login, logout)
│   │
│   ├── pages/
│   │   ├── Login.jsx                 ← Login page
│   │   ├── Register.jsx              ← Register page
│   │   ├── Menu.jsx                  ← Product listing with category filter
│   │   ├── Cart.jsx                  ← Cart management page
│   │   ├── Orders.jsx                ← Order history listing
│   │   ├── OrderDetail.jsx           ← Individual order details + tracking
│   │   ├── AdminDashboard.jsx        ← Admin overview dashboard
│   │   ├── AdminCategories.jsx       ← Admin: manage categories
│   │   ├── AdminProducts.jsx         ← Admin: manage products
│   │   ├── AdminInventory.jsx        ← Admin: manage stock levels
│   │   └── AdminOrders.jsx           ← Admin: manage + update order statuses
│   │
│   ├── App.jsx                       ← Route definitions
│   ├── App.css                       ← Global component styles
│   ├── main.jsx                      ← React entry point
│   └── index.css                     ← Base/reset styles
│
├── index.html
├── eslint.config.js
├── .gitignore
└── vite.config.js
```

---

## 🚀 Getting Started

### Prerequisites

Ensure the following are installed:

```bash
java -version        # Java 17+
mvn -version         # Maven 3.6+
mysql --version      # MySQL 8.x
node -v              # Node.js 18+
npm -v               # npm 9+
git --version        # Git
```

---

### Database Setup

Open MySQL terminal or Workbench and run:

```sql
CREATE DATABASE retail_ordering;
```

> All tables are **auto-created** by Hibernate on first run via `ddl-auto=update`.
> No manual SQL scripts needed.

---

### Backend Setup

```bash
# 1. Navigate to backend folder
cd ordering

# 2. Set your MySQL password in:
#    src/main/resources/application.properties
#    → spring.datasource.password=YOUR_PASSWORD

# 3. Clean and build
mvn clean install

# 4. Run the application
mvn spring-boot:run
```

| | URL |
|---|---|
| Backend | `http://localhost:8080` |
| Swagger UI | `http://localhost:8080/swagger-ui.html` |
| API Docs JSON | `http://localhost:8080/api-docs` |

---

### Frontend Setup

```bash
# 1. Navigate to frontend folder
cd retailfrontend

# 2. Install dependencies
npm install

# 3. Start the dev server
npm run dev
```

| | URL |
|---|---|
| Frontend | `http://localhost:5173` |

> ⚠️ Make sure the backend is running on port `8080` before starting the frontend.

---

## ⚙️ Configuration

### `src/main/resources/application.properties`

```properties
# ─── SERVER ───
server.port=8080

# ─── DATABASE ───
spring.datasource.url=jdbc:mysql://localhost:3306/retail_ordering?createDatabaseIfNotExist=true&useSSL=false&serverTimezone=UTC
spring.datasource.username=root
spring.datasource.password=yourpassword
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

# ─── JPA / HIBERNATE ───
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQLDialect

# ─── SWAGGER ───
springdoc.api-docs.path=/api-docs
springdoc.swagger-ui.path=/swagger-ui.html
springdoc.swagger-ui.enabled=true

# ─── APP ───
spring.application.name=retail-ordering
```

### `src/api/axios.js`

```javascript
import axios from 'axios';

const instance = axios.create({
  baseURL: 'http://localhost:8080/api',
  headers: {
    'Content-Type': 'application/json'
  }
});

export default instance;
```

---

## 🗺 Frontend Routes

| Route | Page | Description |
|---|---|---|
| `/login` | `Login.jsx` | User login |
| `/register` | `Register.jsx` | New customer registration |
| `/menu` | `Menu.jsx` | Browse products with category filter |
| `/cart` | `Cart.jsx` | View and manage cart |
| `/orders` | `Orders.jsx` | Order history |
| `/orders/:id` | `OrderDetail.jsx` | Individual order details + status |
| `/admin` | `AdminDashboard.jsx` | Admin overview |
| `/admin/categories` | `AdminCategories.jsx` | Manage categories |
| `/admin/products` | `AdminProducts.jsx` | Manage products |
| `/admin/inventory` | `AdminInventory.jsx` | Manage stock |
| `/admin/orders` | `AdminOrders.jsx` | Manage and update orders |

---

## 📡 API Reference

> All APIs return a standard response envelope:
> ```json
> {
>   "success": true | false,
>   "message": "Human readable message",
>   "data": { }
> }
> ```

**Base URL:** `http://localhost:8080`
**Swagger UI:** `http://localhost:8080/swagger-ui.html`

---

### Auth APIs

> ⚠️ Currently **disabled** for demo. See [Security](#-security) to enable.

| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/api/auth/register` | Register new customer |
| `POST` | `/api/auth/login` | Login and receive JWT token |

**POST `/api/auth/register` — Sample Request**
```json
{
  "name": "Gopal",
  "email": "gopal@example.com",
  "password": "Password@123",
  "phone": "9876543210",
  "address": "PSIT, Kanpur"
}
```

**POST `/api/auth/login` — Sample Request**
```json
{
  "email": "gopal@example.com",
  "password": "Password@123"
}
```

**Login — Sample Response**
```json
{
  "success": true,
  "message": "Login successful",
  "data": {
    "token": "eyJhbGciOiJIUzI1NiJ9...",
    "userId": 1,
    "name": "Gopal",
    "role": "CUSTOMER"
  }
}
```

---

### Category APIs

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/categories` | Get all categories |
| `GET` | `/api/categories/{id}` | Get category by ID |
| `POST` | `/api/categories` | Create new category |
| `PUT` | `/api/categories/{id}` | Update category |
| `DELETE` | `/api/categories/{id}` | Delete category |

**POST `/api/categories` — Sample Request**
```json
{
  "name": "Pizza",
  "brand": "Dominos",
  "packagingType": "Box"
}
```

**Sample Response**
```json
{
  "success": true,
  "message": "Category created",
  "data": {
    "id": 1,
    "name": "Pizza",
    "brand": "Dominos",
    "packagingType": "Box"
  }
}
```

---

### Product APIs

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/products` | Get all active products |
| `GET` | `/api/products/{id}` | Get product by ID |
| `GET` | `/api/products/category/{categoryId}` | Filter by category |
| `POST` | `/api/products` | Create new product |
| `PUT` | `/api/products/{id}` | Update product |
| `DELETE` | `/api/products/{id}` | Soft-delete product |

**POST `/api/products` — Sample Request**
```json
{
  "name": "Margherita Pizza",
  "description": "Classic cheese and tomato pizza",
  "price": 299.00,
  "categoryId": 1,
  "imageUrl": "https://example.com/margherita.jpg",
  "stockQuantity": 50
}
```

---

### Cart APIs

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/cart/{userId}` | View user's cart |
| `POST` | `/api/cart/add` | Add item to cart |
| `PUT` | `/api/cart/update/{cartItemId}` | Update item quantity |
| `DELETE` | `/api/cart/remove/{cartItemId}` | Remove item from cart |
| `DELETE` | `/api/cart/clear/{userId}` | Clear entire cart |

**POST `/api/cart/add` — Sample Request**
```json
{
  "userId": 1,
  "productId": 3,
  "quantity": 2
}
```

---

### Order APIs

| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/api/orders/place/{userId}` | Place order from cart |
| `GET` | `/api/orders/user/{userId}` | Get user's order history |
| `GET` | `/api/orders/{orderId}` | Get order details |
| `GET` | `/api/admin/orders` | Get all orders (Admin) |
| `PUT` | `/api/admin/orders/{orderId}/status` | Update order status (Admin) |

**Order Status Flow:**
```
PENDING  →  CONFIRMED  →  PREPARING  →  OUT_FOR_DELIVERY  →  DELIVERED
```

**POST `/api/orders/place/{userId}` — Sample Response**
```json
{
  "success": true,
  "message": "Order placed successfully!",
  "data": {
    "orderId": 1,
    "status": "CONFIRMED",
    "totalAmount": 598.00,
    "orderDate": "2026-04-18T10:30:00",
    "deliveryAddress": "123, MG Road, Kanpur",
    "items": [
      {
        "productName": "Margherita Pizza",
        "quantity": 2,
        "priceAtTime": 299.00,
        "subtotal": 598.00
      }
    ]
  }
}
```

---

### Inventory APIs

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/admin/inventory` | View all stock levels |
| `PUT` | `/api/admin/inventory/{productId}` | Manually update stock |

**PUT `/api/admin/inventory/{productId}` — Sample Request**
```json
{
  "availableStock": 100
}
```

---

## 🗄 Database Schema

All 8 tables are auto-created by Hibernate on first run:

```
users
  id               BIGINT        PK  AUTO_INCREMENT
  name             VARCHAR(100)  NOT NULL
  email            VARCHAR(150)  NOT NULL  UNIQUE
  password         VARCHAR(255)  NOT NULL  (BCrypt hashed)
  role             ENUM(CUSTOMER, ADMIN)
  phone            VARCHAR(15)
  address          TEXT
  created_at       TIMESTAMP

categories
  id               BIGINT        PK  AUTO_INCREMENT
  name             VARCHAR(100)  NOT NULL
  brand            VARCHAR(100)
  packaging_type   VARCHAR(100)

products
  id               BIGINT        PK  AUTO_INCREMENT
  name             VARCHAR(200)  NOT NULL
  description      TEXT
  price            DECIMAL(10,2) NOT NULL
  category_id      BIGINT        FK → categories.id
  image_url        VARCHAR(500)
  stock_quantity   INT           NOT NULL
  active           BOOLEAN       DEFAULT true

inventory
  id               BIGINT        PK  AUTO_INCREMENT
  product_id       BIGINT        FK  UNIQUE → products.id
  available_stock  INT           NOT NULL
  last_updated     TIMESTAMP

cart
  id               BIGINT        PK  AUTO_INCREMENT
  user_id          BIGINT        FK  UNIQUE → users.id
  created_at       TIMESTAMP

cart_items
  id               BIGINT        PK  AUTO_INCREMENT
  cart_id          BIGINT        FK → cart.id
  product_id       BIGINT        FK → products.id
  quantity         INT           NOT NULL
  subtotal         DECIMAL(10,2) NOT NULL

orders
  id               BIGINT        PK  AUTO_INCREMENT
  user_id          BIGINT        FK → users.id
  status           ENUM(PENDING, CONFIRMED, PREPARING, OUT_FOR_DELIVERY, DELIVERED)
  total_amount     DECIMAL(10,2) NOT NULL
  order_date       TIMESTAMP
  delivery_address TEXT

order_items
  id               BIGINT        PK  AUTO_INCREMENT
  order_id         BIGINT        FK → orders.id
  product_id       BIGINT        FK → products.id
  quantity         INT           NOT NULL
  price_at_time    DECIMAL(10,2) NOT NULL  (price snapshot)
  subtotal         DECIMAL(10,2) NOT NULL
```

### Entity Relationships

```
User       ──<  Orders        one user      → many orders
User       ──   Cart          one user      → one cart
Cart       ──<  CartItems     one cart      → many items
CartItem   >──  Product       many items    → one product
Order      ──<  OrderItems    one order     → many items
OrderItem  >──  Product       many items    → one product
Product    >──  Category      many products → one category
Product    ──   Inventory     one product   → one inventory record
```

---

## 🔄 Core Business Flow

### Order Placement

```
1.  Customer clicks Place Order on Cart page
2.  POST /api/orders/place/{userId} is triggered
3.  Backend fetches all CartItems for the user
4.  For each CartItem:
      Inventory.availableStock >= requestedQty ?
      NO  → return HTTP 400, frontend shows error toast
5.  All stock OK:
      Create Order  (status = CONFIRMED)
      Create OrderItem per CartItem (snapshot priceAtTime)
      Deduct inventory per item
      Clear user cart
6.  Return confirmation payload
7.  Frontend shows success toast + navigates to OrderDetail page
```

### Admin Order Status Update

```
1.  Admin opens AdminOrders page
2.  Selects new status from dropdown
3.  PUT /api/admin/orders/{orderId}/status
4.  Order status updated in DB
5.  Customer sees updated status on Orders / OrderDetail page
```

---

## 🔐 Security

> Auth is currently **disabled** for demo — all endpoints are publicly accessible.
> `JwtFilter`, `JwtUtil`, and `SecurityConfig` are present in `config/` but inactive.

### To Enable JWT Auth

**Step 1** — Uncomment Security + JWT in `pom.xml`:
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt-api</artifactId>
    <version>0.11.5</version>
</dependency>
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt-impl</artifactId>
    <version>0.11.5</version>
    <scope>runtime</scope>
</dependency>
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt-jackson</artifactId>
    <version>0.11.5</version>
    <scope>runtime</scope>
</dependency>
```

**Step 2** — Activate the existing classes in `config/`:
```
JwtFilter.java        → uncomment filter chain registration
JwtUtil.java          → uncomment bean and signing key
SecurityConfig.java   → uncomment http security rules
```

**Step 3** — Add to `application.properties`:
```properties
jwt.secret=your-256-bit-secret-key-here
jwt.expiration=86400000
```

**Step 4** — Update `axios.js` to attach token on every request:
```javascript
instance.interceptors.request.use(config => {
  const token = localStorage.getItem('token');
  if (token) config.headers.Authorization = `Bearer ${token}`;
  return config;
});
```

### Access Matrix (when enabled)

| Endpoint | Public | Customer | Admin |
|---|---|---|---|
| `/api/auth/**` | ✅ | — | — |
| `GET /api/products` | ✅ | ✅ | ✅ |
| `GET /api/categories` | ✅ | ✅ | ✅ |
| `/api/cart/**` | — | ✅ | — |
| `/api/orders/place/**` | — | ✅ | — |
| `/api/orders/user/**` | — | ✅ | — |
| `/api/admin/**` | — | — | ✅ |
| `/swagger-ui/**` | ✅ | ✅ | ✅ |

---

## ✅ MVP Scope

| Feature | Status |
|---|---|
| User registration and login | ✅ Complete |
| Browse products with category filter | ✅ Complete |
| Product CRUD (admin) | ✅ Complete |
| Category CRUD (admin) | ✅ Complete |
| Cart — add, update, remove, clear | ✅ Complete |
| Order placement with stock validation | ✅ Complete |
| Automatic inventory deduction on order | ✅ Complete |
| Order status tracking (5 stages) | ✅ Complete |
| Order history and order detail page | ✅ Complete |
| Admin dashboard | ✅ Complete |
| Admin — manage orders and update status | ✅ Complete |
| Admin — inventory management | ✅ Complete |
| Toast notifications | ✅ Complete |
| Swagger / OpenAPI documentation | ✅ Complete |
| JWT Auth + Spring Security | ⏳ Ready — disabled for demo |
| Email order confirmation | ❌ Stretch |
| Coupons / loyalty points | ❌ Stretch |
| Cloud DB deployment | ❌ Phase 2 |

---

## 👨‍💻 Author

**Gopal**
Final Year B.Tech — Computer Science
Pranveer Singh Institute of Technology (PSIT), Kanpur | CGPA: 8.0

---

## 📄 License

Built for educational and internal hackathon purposes.
**Classification: Internal**

---

> 💡 **Quick Start:**
> Backend → `http://localhost:8080` |
> Frontend → `http://localhost:5173` |
> Swagger → `http://localhost:8080/swagger-ui.html`
