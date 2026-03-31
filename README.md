# Sirius E-Commerce

A full-stack e-commerce application built with the MERN stack (MongoDB, Express, React, Node.js). Features a complete shopping experience with product browsing, cart management, order processing, PayPal payment integration, and an admin dashboard for managing the store.

## Demo

![Sirius E-Commerce Demo](demo/demo.gif)

## Tech Stack

**Frontend:** React 18, Redux Toolkit (RTK Query), React Router 6, Tailwind CSS, Vite
**Backend:** Node.js, Express.js, MongoDB (Mongoose), JWT Authentication
**Payments:** PayPal
**Image Storage:** Cloudinary
**Charts:** ApexCharts (Admin Dashboard)

## Features

### Customer
- Browse products with filtering by category and price range
- Product search and pagination
- Product reviews and ratings
- Favorites / wishlist (persisted in localStorage)
- Shopping cart with quantity management
- Checkout flow with shipping address and payment
- PayPal payment integration
- Order history and order tracking
- User profile management

### Admin
- Dashboard with sales analytics and charts
- User management (view, update roles, delete)
- Product management (CRUD with image upload via Cloudinary)
- Category management
- Order management (view all, mark as delivered)

## Project Structure

```
sirius_ecommerce/
  backend/
    config/          # Database connection and Cloudinary config
    controllers/     # Route handlers
    middlewares/      # Auth and admin middleware
    models/          # Mongoose schemas (User, Product, Category, Order)
    routes/          # API route definitions
    utils/           # JWT token helper
    index.js         # Express server entry point
  frontend/
    src/
      components/  # Reusable UI components
      pages/       # Page components (Auth, Admin, Products, Orders)
      redux/       # Store, slices, RTK Query API definitions
    vercel.json      # Vercel SPA rewrite config
    vite.config.js   # Vite config with dev proxy
  package.json         # Root package (backend deps and dev scripts)
  .env                 # Environment variables (not committed)
```

## Prerequisites

- Node.js 18+
- MongoDB (local or MongoDB Atlas)
- Cloudinary account (free tier available)
- PayPal Developer account (optional, for payments)

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/sirius-ecommerce.git
cd sirius-ecommerce
```

### 2. Install dependencies

```bash
# Install backend dependencies (from root)
npm install

# Install frontend dependencies
npm install --prefix frontend
```

### 3. Set up environment variables

Create a `.env` file in the project root:

```env
PORT=5000
MONGO_URI=mongodb://127.0.0.1:27017/siriusStore
JWT_SECRET=your_jwt_secret_here
NODE_ENV=development
PAYPAL_CLIENT_ID=your_paypal_client_id
FRONTEND_URL=http://localhost:5173
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret
```

### 4. Run the application

```bash
# Run both frontend and backend concurrently
npm run dev

# Or run them separately:
npm run backend    # Backend on http://localhost:5000
npm run frontend   # Frontend on http://localhost:5173
```

## API Endpoints

### Auth and Users - `/api/users`
| Method | Endpoint | Access | Description |
|--------|----------|--------|-------------|
| POST | `/` | Public | Register |
| POST | `/auth` | Public | Login |
| POST | `/logout` | Public | Logout |
| GET | `/profile` | User | Get profile |
| PUT | `/profile` | User | Update profile |
| GET | `/` | Admin | Get all users |
| GET | `/:id` | Admin | Get user by ID |
| PUT | `/:id` | Admin | Update user |
| DELETE | `/:id` | Admin | Delete user |

### Products - `/api/products`
| Method | Endpoint | Access | Description |
|--------|----------|--------|-------------|
| GET | `/` | Public | Get products (paginated) |
| GET | `/allproducts` | Public | Get all products |
| GET | `/top` | Public | Top rated products |
| GET | `/new` | Public | Newest products |
| GET | `/:id` | Public | Get product by ID |
| POST | `/` | Admin | Create product |
| PUT | `/:id` | Admin | Update product |
| DELETE | `/:id` | Admin | Delete product |
| POST | `/:id/reviews` | User | Add review |
| POST | `/filtered-products` | Public | Filter products |

### Orders - `/api/orders`
| Method | Endpoint | Access | Description |
|--------|----------|--------|-------------|
| POST | `/` | User | Create order |
| GET | `/mine` | User | Get my orders |
| GET | `/:id` | User | Get order by ID |
| PUT | `/:id/pay` | User | Mark as paid |
| GET | `/` | Admin | Get all orders |
| PUT | `/:id/deliver` | Admin | Mark as delivered |
| GET | `/total-orders` | Admin | Total order count |
| GET | `/total-sales` | Admin | Total sales amount |
| GET | `/total-sales-by-date` | Admin | Sales by date |

### Categories - `/api/category`
Full CRUD (Admin only)

### Uploads - `/api/upload`
| Method | Endpoint | Access | Description |
|--------|----------|--------|-------------|
| POST | `/` | Admin | Upload product image (Cloudinary) |

## Deployment

This project is configured for split deployment:

- **Frontend** on Vercel (root directory: frontend)
- **Backend** on Render (start command: node backend/index.js)

### Environment Variables for Production

**Render (Backend):**
| Variable | Value |
|----------|-------|
| PORT | 5000 |
| NODE_ENV | production |
| MONGO_URI | Your MongoDB Atlas connection string |
| JWT_SECRET | A strong random secret |
| FRONTEND_URL | Your Vercel deployment URL |
| PAYPAL_CLIENT_ID | Your PayPal client ID |
| CLOUDINARY_CLOUD_NAME | Your Cloudinary cloud name |
| CLOUDINARY_API_KEY | Your Cloudinary API key |
| CLOUDINARY_API_SECRET | Your Cloudinary API secret |

**Vercel (Frontend):**
| Variable | Value |
|----------|-------|
| VITE_API_URL | Your Render deployment URL |

## License

ISC
