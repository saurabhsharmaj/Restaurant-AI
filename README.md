# MCP Restaurant Platform – MCP Client ↔ MCP Server Demo

## Overview

This project demonstrates a complete **MCP (Model Context Protocol)** architecture using:

- **MCP Client** → AI Assistant / Chat UI / CLI Agent
- **MCP Server** → Gateway exposing restaurant tools
- **Microservices** → Multiple independent Node.js services
- **Tool Calling** → MCP tools exposed by backend services

The goal is to showcase to management how:

1. MCP Client communicates with MCP Server
2. MCP Server exposes tools dynamically
3. Multiple Node.js microservices work independently
4. AI Agent can perform restaurant operations using MCP Tools
5. Architecture is scalable and enterprise-ready

---

# High Level Architecture

```text
┌───────────────────────────────────────────────────────────────────────┐
│                           MCP CLIENT                                 │
│                                                                       │
│  ChatGPT / Claude Desktop / VSCode Agent / Custom AI Assistant        │
│                                                                       │
│  User Prompts:                                                        │
│   • Show Pizza Menu                                                   │
│   • Order Paneer Butter Masala                                        │
│   • Apply Promo Code                                                  │
│   • Track Delivery                                                    │
│                                                                       │
└───────────────────────────────┬───────────────────────────────────────┘
                                │ MCP Protocol
                                ▼
┌───────────────────────────────────────────────────────────────────────┐
│                           MCP SERVER                                  │
│                                                                       │
│  Node.js + Express + MCP SDK                                          │
│                                                                       │
│  Responsibilities:                                                     │
│   • Tool Registration                                                  │
│   • Request Routing                                                    │
│   • Tool Discovery                                                     │
│   • Authentication                                                     │
│   • Context Management                                                 │
│   • Orchestration                                                      │
│                                                                       │
│  Exposed MCP Tools:                                                    │
│   • getMenu()                                                          │
│   • placeOrder()                                                       │
│   • trackOrder()                                                       │
│   • applyPromoCode()                                                   │
│   • getRecommendations()                                               │
│   • generateBill()                                                     │
│   • submitReview()                                                     │
│                                                                       │
└───────────────────────────────┬───────────────────────────────────────┘
                                │ REST/gRPC/Event Bus
                                ▼
┌──────────────────────────────────────────────────────────────────────────────┐
│                         MICROSERVICE LAYER                                  │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  1. Catalog Service                                                          │
│     • Food Categories                                                        │
│     • Veg / Non-Veg Menu                                                     │
│     • Pricing                                                                │
│     • Availability                                                           │
│                                                                              │
│  2. Order Service                                                            │
│     • Create Orders                                                          │
│     • Update Order Status                                                    │
│     • Order History                                                          │
│                                                                              │
│  3. Kitchen Service                                                          │
│     • Cooking Queue                                                          │
│     • Chef Assignment                                                        │
│     • Preparation Tracking                                                   │
│                                                                              │
│  4. User/Customer Service                                                    │
│     • Customer Profiles                                                      │
│     • Address Management                                                     │
│     • Preferences                                                            │
│                                                                              │
│  5. Delivery/Logistics Service                                               │
│     • Delivery Partner Assignment                                            │
│     • Real-time Tracking                                                     │
│     • ETA Calculation                                                        │
│                                                                              │
│  6. Notification Service                                                     │
│     • SMS                                                                    │
│     • Email                                                                  │
│     • WhatsApp                                                               │
│     • Push Notifications                                                     │
│                                                                              │
│  7. Billing & Payment Service                                                │
│     • Bill Generation                                                        │
│     • Tax Calculation                                                        │
│     • Payment Processing                                                     │
│                                                                              │
│  8. Review & Rating Service                                                  │
│     • User Reviews                                                           │
│     • Food Ratings                                                           │
│     • Restaurant Feedback                                                    │
│                                                                              │
│  9. Search & Recommendation Service                                          │
│     • Semantic Search                                                        │
│     • Recommendation Engine                                                  │
│     • Popular Foods                                                          │
│                                                                              │
│ 10. Discount & Promo Service                                                 │
│     • Coupons                                                                │
│     • Offers                                                                 │
│     • Promo Validation                                                       │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
                                │
                                ▼
┌───────────────────────────────────────────────────────────────────────┐
│                         DATA & INFRASTRUCTURE                        │
├───────────────────────────────────────────────────────────────────────┤
│                                                                       │
│  PostgreSQL / MongoDB                                                 │
│  Redis Cache                                                          │
│  RabbitMQ / Kafka                                                     │
│  Docker Containers                                                    │
│  Kubernetes (Optional)                                                │
│  API Gateway                                                          │
│  Prometheus + Grafana                                                 │
│                                                                       │
└───────────────────────────────────────────────────────────────────────┘
```

---

# Restaurant Catalog Structure

## Starter

### Drinks
- Cold Coffee
- Mojito
- Fresh Lime Soda
- Mango Shake

### Pizza
- Margherita Pizza
- Farmhouse Pizza
- Chicken Pepperoni Pizza

### Pasta
- White Sauce Pasta
- Red Sauce Pasta
- Chicken Alfredo Pasta

### Soup
- Tomato Soup
- Sweet Corn Soup
- Chicken Hot & Sour Soup

### Paneer
- Paneer Tikka
- Chilli Paneer
- Paneer 65

---

## Main Course

### Vegetable
- Veg Kolhapuri
- Kadai Paneer
- Butter Chicken
- Chicken Curry

### Roti
- Butter Naan
- Tandoori Roti
- Garlic Naan

### Chawal
- Jeera Rice
- Veg Biryani
- Chicken Biryani

---

## Desert

### Sweet
- Gulab Jamun
- Rasmalai
- Brownie

### Ice Cream
- Vanilla
- Chocolate
- Butterscotch

---

## Special Thali

### Regular Thali
- Dal
- Rice
- 2 Roti
- Sabzi
- Sweet

### Special Thali
- Paneer Dish
- Dal Makhani
- Rice
- Butter Naan
- Dessert
- Starter

---

# Suggested Tech Stack

| Layer | Technology |
|---|---|
| MCP Server | Node.js + TypeScript |
| API Framework | Express.js / Fastify |
| MCP SDK | Model Context Protocol SDK |
| Database | PostgreSQL / MongoDB |
| Cache | Redis |
| Message Broker | RabbitMQ / Kafka |
| Containerization | Docker |
| Orchestration | Kubernetes |
| API Gateway | Kong / NGINX |
| Monitoring | Grafana + Prometheus |
| Authentication | JWT / OAuth2 |

---

# MCP Tool Design

## Catalog Tools

```ts
getMenu(category)
searchFood(query)
getFoodDetails(foodId)
```

## Order Tools

```ts
placeOrder(orderPayload)
getOrder(orderId)
cancelOrder(orderId)
trackOrder(orderId)
```

## Kitchen Tools

```ts
getKitchenQueue()
updateCookingStatus(orderId)
```

## User Tools

```ts
registerUser()
getUserProfile()
updateAddress()
```

## Payment Tools

```ts
generateBill(orderId)
processPayment()
refundPayment()
```

## Review Tools

```ts
submitReview()
getRatings(foodId)
```

## Promo Tools

```ts
applyPromoCode(code)
validateCoupon(code)
```

---

# MCP Server Folder Structure

```text
restaurant-mcp-platform/
│
├── mcp-server/
│   ├── src/
│   │   ├── tools/
│   │   ├── routes/
│   │   ├── services/
│   │   ├── middleware/
│   │   └── app.ts
│   └── package.json
│
├── services/
│   ├── catalog-service/
│   ├── order-service/
│   ├── kitchen-service/
│   ├── user-service/
│   ├── delivery-service/
│   ├── notification-service/
│   ├── payment-service/
│   ├── review-service/
│   ├── recommendation-service/
│   └── promo-service/
│
├── docker-compose.yml
├── README.md
└── kubernetes/
```

---

# Example MCP Flow

## Scenario: User Orders Pizza

### Step 1 – User Prompt

```text
User: Order one Farmhouse Pizza and one Mojito
```

### Step 2 – MCP Client

MCP Client sends request to MCP Server.

### Step 3 – MCP Server Tool Selection

MCP Server invokes:

```ts
searchFood("Farmhouse Pizza")
searchFood("Mojito")
placeOrder(orderPayload)
```

### Step 4 – Order Service

Order Service creates order.

### Step 5 – Kitchen Service

Kitchen queue updated.

### Step 6 – Payment Service

Bill generated.

### Step 7 – Notification Service

Customer receives confirmation.

### Step 8 – Delivery Service

Delivery assigned.

---

# Event Driven Communication

## Recommended Async Events

```text
ORDER_CREATED
PAYMENT_SUCCESS
ORDER_PREPARING
ORDER_READY
DELIVERY_ASSIGNED
ORDER_DELIVERED
REVIEW_SUBMITTED
```

Use:

- RabbitMQ
- Apache Kafka
- NATS

for scalable communication between microservices.

---

# Security Architecture

## Authentication

- JWT Token
- OAuth2
- API Key for MCP Client

## Authorization

- RBAC (Role Based Access)
- Admin
- Kitchen Staff
- Delivery Agent
- Customer

## Security Best Practices

- HTTPS
- Rate Limiting
- Request Validation
- Audit Logging

---

# Deployment Architecture

```text
┌──────────────────────┐
│     Load Balancer    │
└──────────┬───────────┘
           │
┌──────────▼───────────┐
│      API Gateway     │
└──────────┬───────────┘
           │
 ┌─────────▼──────────┐
 │     MCP Server     │
 └─────────┬──────────┘
           │
 ┌─────────▼─────────────────────────────────┐
 │           Kubernetes Cluster             │
 │                                           │
 │  Catalog Pods                             │
 │  Order Pods                               │
 │  Kitchen Pods                             │
 │  Delivery Pods                            │
 │  Notification Pods                        │
 │  Payment Pods                             │
 │                                           │
 └───────────────────────────────────────────┘
```

---

# Sample README.md

```md
# Restaurant MCP Platform

A scalable Restaurant Management Platform using:

- MCP Server
- MCP Client
- Node.js Microservices
- Event Driven Architecture
- Docker & Kubernetes

---

# Features

- Restaurant Catalog
- Veg & Non-Veg Menu
- Order Management
- Kitchen Workflow
- Delivery Tracking
- Billing & Payments
- Reviews & Ratings
- Search & Recommendations
- Discounts & Promo Codes

---

# Architecture

MCP Client communicates with MCP Server.

MCP Server exposes tools that orchestrate multiple backend microservices.

---

# Tech Stack

- Node.js
- TypeScript
- Express.js
- PostgreSQL
- MongoDB
- Redis
- RabbitMQ
- Docker
- Kubernetes

---

# Services

| Service | Responsibility |
|---|---|
| Catalog Service | Menu & food management |
| Order Service | Order lifecycle |
| Kitchen Service | Food preparation |
| User Service | Customer management |
| Delivery Service | Delivery tracking |
| Notification Service | SMS/Email/Push |
| Payment Service | Billing & payments |
| Review Service | Reviews & ratings |
| Recommendation Service | AI recommendations |
| Promo Service | Discounts & coupons |

---

# MCP Tools

```ts
getMenu()
placeOrder()
trackOrder()
applyPromoCode()
generateBill()
submitReview()
```

---

# Run Locally

## Install Dependencies

```bash
npm install
```

## Start Services

```bash
docker-compose up
```

## Start MCP Server

```bash
cd mcp-server
npm run dev
```

---

# Future Enhancements

- AI-based recommendation engine
- Voice ordering
- Real-time analytics
- Smart kitchen automation
- Dynamic pricing

---

# Demo Flow

1. MCP Client sends prompt
2. MCP Server selects tool
3. Tool invokes microservice
4. Services communicate asynchronously
5. Final response returned to user

---

# Author

Architecture Demo for Enterprise MCP Integration
```

---

# Recommended Demo for Manager

## Demo Storyline

### Demo 1 – Discover Menu

```text
User: Show me Veg Pizza options
```

MCP Tool:

```ts
getMenu("Pizza")
```

---

### Demo 2 – Place Order

```text
User: Order one Paneer Tikka and Butter Naan
```

MCP invokes:

```ts
searchFood()
placeOrder()
generateBill()
```

---

### Demo 3 – Apply Coupon

```text
User: Apply coupon FOOD50
```

MCP invokes:

```ts
applyPromoCode("FOOD50")
```

---

### Demo 4 – Track Delivery

```text
User: Track my order
```

MCP invokes:

```ts
trackOrder(orderId)
```

---

### Demo 5 – Recommendation

```text
User: Recommend best dessert with pizza
```

MCP invokes:

```ts
getRecommendations()
```

---

# Best Enterprise Practices

## Recommended Standards

- API Versioning
- OpenAPI / Swagger
- Centralized Logging
- Distributed Tracing
- CI/CD Pipeline
- Health Checks
- Circuit Breakers
- Retry Policies
- Idempotency

---

# Conclusion

This architecture demonstrates:

- Modern MCP ecosystem
- Enterprise microservices design
- AI-driven restaurant workflow
- Tool orchestration
- Event-driven communication
- Scalable backend systems

The design is suitable for:

- Restaurant Chains
- Food Delivery Platforms
- AI Ordering Assistants
- Smart Hospitality Systems

