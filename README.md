🇪🇸 [Español](README.md) | 🇬🇧 [English](README.en.md)

# 📚 BookShop - Plataforma de Venta y Suscripción de Libros

![Laravel](https://img.shields.io/badge/Laravel-12-red)
![Vue](https://img.shields.io/badge/Vue-3-green)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-DB-blue)
![Docker](https://img.shields.io/badge/Docker-Container-blue)
![Stripe](https://img.shields.io/badge/Stripe-Payments-purple)

BookShop es una plataforma web que permite a los usuarios **comprar libros digitales, suscribirse para acceder a una biblioteca de lectura y gestionar su perfil y pedidos**.

El proyecto también incluye un **panel de administración** para gestionar libros y el catálogo de la tienda.

Desarrollado con **Laravel** + **Vue.js**, aplicando principios SOLID y siguiendo metodologías ágiles (Agile) en el desarrollo y desplegado de manera segura con **Docker** en https://booksplanet.store

---

# 🚀 Funcionalidades

## 👤 Usuarios

- Registro y autenticación de usuarios
- Gestión de perfil
- Visualización de pedidos realizados
- Compra de libros individuales
- Suscripción mensual/anual para acceso a biblioteca
- Lectura de libros disponibles mediante suscripción

---

## 📚 Tienda de Libros

- Catálogo de libros
- Página de detalle de cada libro
- Compra individual de libros
- Acceso a libros incluidos en suscripción
- Lectura online de libros mediante suscripción
- Sistema de pagos con **Stripe**

---

## 💳 Pagos

Integración con **Stripe** para:

- Pago de libros individuales
- Pago de suscripciones
- Gestión de estados de pago

---

## 📦 Gestión de Pedidos

El sistema registrará:

- Pedidos realizados por el usuario
- Historial de compras
- Estado del pedido
- Libros incluidos en cada pedido

---

## 🔑 Panel de Administración

El administrador podrá:

- Crear libros
- Editar libros
- Eliminar libros
- Gestionar catálogo
- Visualizar pedidos

### CRUD de Libros

Campos principales:

- id
- title
- slug
- description
- isbn
- language
- publisher
- published_year
- edition
- pages_count
- cover_path
- access_type (ej. subsciption, individual, etc)
- price
- status (ej draft, published, etc)
- published_at
- timestamps
- softDeletes
---

## 🏗 Arquitectura del Sistema



# 🧱 Project Architecture

The project follows a modern architecture based on:

- **Backend API:** Laravel
- **Public Frontend:** Server Side Rendering (SSR)
- **Administration Panel:** Client Side Rendering (CSR) with Vue.js
- **Database:** PostgreSQL
- **Containers:** Docker

Simplified structure:
```bash
bookshop/
│
├── book-store-backend
├── book-store-frontend
├── book-store-docker
├── docs
└── README.md
```
--- 
## ⚙️ Rendering Strategy

The platform uses a **hybrid rendering architecture** to optimize SEO, performance, and interactivity.

### Server Side Rendering (SSR)

Used in the public-facing part of the platform:

- Book catalog
- Detail pages
- Landing pages
- Indexable content

Advantages:

- Better SEO
- Faster initial rendering
- Improved search engine indexing

### Client Side Rendering (CSR)

Used in:

- Administration panel
- Interactive book reader

Examples:

- Book management (CRUD)
- Catalog management
- System administration

Advantages:

- SPA-like application experience
- Faster interactions
- Less page reloads
- SEO optimization is not critical
---

# 🛠 Technologies Used

## Backend

- Laravel 12
- PHP 8+
- Eloquent ORM
- Laravel Authentication
- Laravel Policies / Middleware
- FormRequests
- Laravel Sanctum

## Frontend

- Vue.js 3
- Inertia.js
- Server Side Rendering (SSR) (Public-facing part)
- Client Side Rendering (CSR) (Admin panel, interactive book reader)
- Vite
- HTML5
- CSS3
- Bootstrap & SCSS

## Payments

- Stripe
- Stripe Webhooks

## Infrastructure

- Docker
- Docker Compose
- Nginx
- PostgreSQL

## SEO

- Google Search Console
- Google Analytics
- HTML Optimization

## Hosting

The project is deployed at:

https://booksplanet.store

Infrastructure:

- Linux VPS
- Docker
- Nginx
- PostgreSQL

# 📋 Technical Requirements

To run the project, you need:

- Docker
- Docker Compose
- Git

Optional (if running without Docker):

- PHP 8.2+
- Composer
- Node.js 18+
- npm or pnpm
- PostgreSQL

# 🐳 Docker Installation

## 1. Clone the repository

```bash
git clone https://github.com/zhenyax14/book_shop.git
cd book_shop
```

## 2. Copy the environment file
Copy the default variables:
```bash
    cp .env.example .env
```
Edit it:
```bash
    nano .env
```
Enter your  DEV or PROD credentials:
```
    DB_DATABASE=bookshop
    DB_USERNAME=root
    DB_PASSWORD=root
    
    STRIPE_KEY=your_key
    STRIPE_SECRET=your_secret
```

## 3. Start the containers
```bash
  docker compose up -d
```
## 4. Install the dependencies
```bash
    docker compose exec app composer install
    docker compose exec app npm install
    docker compose exec app npm run dev
```

## 5. Generate application key
```bash
    docker compose exec app php artisan key:generate
```

## 6. Run migrations
```bash
    docker compose exec app php artisan migrate
```
# 📊 Data Model

![E-R Diagram](docs/img/ER/er-diagram.png)

Main system entities:

### Users

- id
- name
- email
- email_verified_at
- password
- role
- remember_token
- timestamps

### Books

- id
- title
- slug
- description
- isbn
- language
- publisher
- published_year
- edition
- pages_count
- cover_path
- access_type (e.g. subscription, individual, etc)
- price
- status (e.g. draft, published, etc)
- published_at
- timestamps
- softDeletes

### Tags

- id
- name
- slug
- color
- created_at
- updated_at

### Book Tags (Pivot Table)

- book_id
- tag_id

### Book Volumes

- id
- book_id
- number
- title
- timestamps

### Book Chapters

- id
- book_id
- volume_id
- number
- title
- slug
- reading_time_minutes
- is_published
- timestamps

### Book Pages

- id
- chapter_id
- number
- global_number
- content
- content_format
- word_count
- timestamps

### User Reading Progress

- id
- user_id
- book_id
- chapter_id
- page_id
- scroll_position
- completion_percentage
- last_read_at
- is_finished
- finished_at
- timestamps

### Bookmarks

- id
- user_id
- book_id
- page_id
- label
- color
- timestamps

### Annotations

- id
- user_id
- page_id
- start_offset
- end_offset
- selected_text
- color
- note
- timestamps

### Reading Sessions

- id
- user_id
- book_id
- start_page_id
- end_page_id
- started_at
- ended_at
- pages_read
- duration_seconds
- timestamps

### Orders

- id
- user_id
- total
- payment_status
- stripe_session_id

### Order Items

- id
- order_id
- book_id
- price

### Subscriptions

- id
- user_id
- stripe_subscription_id
- status
- expires_at

### Reading Settings

- id
- user_id
- font_size
- font_family
- line_height
- theme
- page_width
- pagination_mode
- words_per_page
- timestamps

# 🔐 Security

## Back-End

- CSRF protection
- Validation using FormRequest
- Laravel Sanctum for APIs
- Role-based route protection

## Front-End

- Live form validation
- Communication with Back-End via token

## Deployment

- Basic VPS server hardening (ufw, strong passwords, ssh)
- Correct folder permissions according to structure

# 📖 Project Roadmap

Possible future improvements:

- Book review system
- Favorites / wishlist
- Book recommendations
- Admin metrics dashboard
- AI assistant

# 🧪 Testing

Will be implemented:

- Unit tests with PHPUnit
- API integration tests
- Simulated payment tests with Stripe

# 📄 License

This project is distributed under the CC BY-NC license.

# 📖 Additional Documentation

[Stripe](https://docs.stripe.com/ )

[Laravel](https://laravel.com/docs/12.x/installation)

[Vue](https://vuejs.org/guide/introduction.html)