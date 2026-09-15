# TeaTime — Agent Build Instructions

## 1. Project Overview
TeaTime is a full-stack tea discovery, recommendation, and multi-seller marketplace platform. Users get personalized tea recommendations, browse/search teas, and buy from multiple sellers. Sellers manage their own shop and inventory. Admins manage the whole platform.

## 2. Tech Stack

### Frontend
- React
- JavaScript (no TypeScript)
- Tailwind CSS

### Backend
- Java
- Spring Boot
- Spring Web / REST API
- Spring Data JPA
- Spring Security
- JWT
- Bean Validation
- Maven

### Database
- MySQL

## 3. Architecture

```
TeaTime
   │
   ▼
React + JavaScript (Frontend)
   │
REST API
   │
   ▼
Spring Boot
   │
 ┌─────────────┼─────────────┐
 │             │             │
Spring        JWT      Business Logic
Security
 │             │             │
 └─────────────┼─────────────┘
   │
   ▼
MySQL
```

## 4. Backend Package Structure

```
com.teatime
│
├── controller
├── service
├── repository
├── model
├── dto
├── security
├── exception
└── config
```

Example controllers/services/repositories:
- TeaController / TeaService / TeaRepository
- UserController / UserService / UserRepository
- SellerController / SellerService / SellerRepository
- OrderController / OrderService / OrderRepository
- ReviewController / ReviewService / ReviewRepository
- RecommendationController / RecommendationService

## 5. Roles & Authorization

Three roles, enforced via Spring Security + JWT:

- **ROLE_CUSTOMER**: browse teas, get recommendations, favorites, cart, orders, reviews
- **ROLE_SELLER**: manage tea products, inventory, view/update orders, seller dashboard
- **ROLE_ADMIN**: manage users, sellers, products, reviews, orders, categories

JWT handles authentication. Spring Security handles authorization (role-based route protection).

## 6. Database Entities (MySQL)

users, roles, sellers, shops, teas, tea_categories, tea_flavors, tea_origins, tea_images, inventory, favorites, reviews, carts, cart_items, orders, order_items, payments, recommendations

## 7. Recommendation Engine (v1 — rule-based, no ML)

Plain Java business logic inside Spring Boot. Weighted score:

- Flavor Match — 40%
- Caffeine Match — 25%
- Mood Match — 20%
- Experience Match — 15%

Input: User Tea Preference Profile → compare against each Tea → compute Tea Match Score → return Top 5 Recommended Teas.

## 8. Feature Scope

### Authentication & Users
- Registration, Login/logout, User profile, User preferences
- Customer/Seller/Admin roles, JWT auth, role-based authorization

### Tea
- Tea database, categories, details (origin, region, elevation, harvest season, processing method, caffeine, flavor profile, aroma, strength), brewing info, images

### Discovery
- Tea Explorer, Search, Filters, Sorting, Similar teas, Trending teas

### Personalization
- Tea Preference Profile, Find My Tea Quiz, Recommendation Engine, Tea DNA, Personalized recommendations

### Marketplace
- Seller registration, seller shop, product listings, inventory, seller dashboard
- Cart, Checkout, Orders, Order tracking
- Reviews, Ratings, Favorites

### Brewing
- Brewing Guide, Brewing Calculator, Brewing Timer, Multiple infusion info

### Business
- Promotions, Discounts, Featured products, Tea subscriptions

### Advanced (later phase)
- AI Tea Assistant
- Advanced ML Recommendation System

### Admin
- Admin dashboard, user/seller/product management, review moderation, order management, categories, tea origins, platform analytics

### System
- Customer/Seller/Order/Inventory notifications

## 9. Build Order (for agents)

1. Project scaffolding: Spring Boot backend + React frontend, connect to MySQL.
2. Entity models + repositories for core tables (users, roles, teas, categories).
3. Authentication: registration, login, JWT issuing, Spring Security config, role guards.
4. Tea CRUD + Discovery (search/filter/sort).
5. Tea Preference Profile + Recommendation Engine (rule-based scoring).
6. Seller module: shop, product listing, inventory, seller dashboard.
7. Cart, Checkout, Orders, Order tracking.
8. Reviews, Ratings, Favorites.
9. Brewing Guide/Calculator/Timer.
10. Admin dashboard + management screens.
11. Notifications.
12. Business features: Promotions, Discounts, Featured products, Subscriptions.
13. Advanced (last): AI Tea Assistant, ML Recommendation System.

## 10. Notes for Agents
- Keep controllers thin; business logic in service layer.
- Use DTOs for request/response, not raw entities.
- Follow REST conventions for endpoint naming.
- Use Tailwind utility classes directly; no custom CSS unless necessary.
- Do not introduce TypeScript, PostgreSQL, or ML in v1 — out of scope for this build.
