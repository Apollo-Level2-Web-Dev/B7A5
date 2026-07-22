
# Assignment 5 - FixItNow Frontend 🔧
**"Your Trusted Home Service Platform"**

---

## Project Overview

FixItNow is a modern, responsive **Next.js frontend application** for a home services marketplace. Customers can browse available services, view technician profiles, and book qualified professionals for specific time slots. Technicians can build their service profiles, manage their availability via an interactive scheduler, and handle job bookings. Admins oversee the entire platform through a comprehensive moderation dashboard.

> 💡 **Note**: This is a **frontend-only** assignment. You will consume a backend API (your own from a previous assignment, a partner's, or a provided mock API).

---

## Roles & Permissions

| Role | Description | Frontend UI Expectations |
|------|-------------|-----------------|
| **Customer** | Users who book home services | Public browsing, interactive time-slot selection for bookings, payment checkout flow, booking tracking dashboard, review submission. |
| **Technician** | Service professionals | Protected technician dashboard, profile/services setup forms, interactive availability calendar/scheduler UI, booking management table (accept/decline/complete actions). |
| **Admin** | Platform moderators | Protected admin dashboard, user management tables (ban/unban actions), global platform statistics, service category management UI. |

> 💡 **Note**: Users select their role during registration. The UI must dynamically adapt based on the authenticated user's role, and routes must be protected using **Next.js Middleware**.

---

## 🛠️ Tech Stack

| Technology | Purpose |
|------------|---------|
| **Next.js** (App Router) | React Framework, Routing, Server/Client Components |
| **TypeScript** | Type safety (Mandatory interfaces for all data models) |
| **Tailwind CSS** | Styling (Shadcn UI, DaisyUI, or custom components allowed) |
| **React Hook Form + Zod** | Form state management and client-side schema validation |
| **TanStack Query (React Query)** or **SWR** | Server state management, caching, and data fetching |
| **NextAuth.js** or **Custom JWT + Middleware** | Authentication state and protected route enforcement |
| **Stripe.js** or **SSLCommerz JS** | Frontend payment gateway integration |

---

## Features & UI/UX Requirements

### Public Features
- **Responsive Service Grid**: Display services and top-rated technicians with optimized images (`next/image`), ratings, and starting prices.
- **Advanced Search & Filter**: Sidebar or top-bar filters for service type, location, rating, and price range with real-time UI updates.
- **Technician Profile Page**: Comprehensive view with technician bio, skills, past reviews, and an interactive "Book Now" section (with date/time pickers).
- **Loading & Error States**: Skeleton loaders for data fetching and graceful `error.tsx` fallbacks.

### Customer Features
- **Auth Flows**: Registration and login forms with Zod validation and inline error messages.
- **Booking Flow**: Interactive UI to select a service, choose a technician, and pick an available time slot. 
- **Payment Integration**: Seamless redirect to **Stripe Checkout** or **SSLCommerz** gateway after the technician accepts the booking. Dedicated `/payment/success` and `/payment/cancel` pages.
- **Customer Dashboard**: View booking history (with status badges and a "Cancel" button for eligible bookings), payment history table, and a form to leave reviews after job completion.

### Technician Features
- **Technician Dashboard**: Overview of upcoming jobs, total earnings, and pending requests.
- **Profile & Services Management**: Forms to update skills, experience, pricing, and profile picture.
- **Availability Scheduler**: An interactive calendar or time-slot picker UI to set working hours and block out unavailable times.
- **Booking Management**: A dedicated table to view incoming requests with action buttons ("Accept", "Decline", "Mark In-Progress", "Mark Completed").

### Admin Features
- **Admin Dashboard**: Global overview of platform health (total users, active bookings, revenue).
- **User Management**: Data table of all users with search, pagination, and "Ban/Unban" action buttons.
- **Category Management**: UI to view, create, and manage service categories.

---

## Frontend Routes & API Integration

> ⚠️ **Note**: These are suggested Next.js App Router paths. You must map these to your backend API endpoints.

| Next.js Route | Component/Feature | Backend API Consumption |
|---------------|-------------------|-------------------------|
| `/` | Home page with featured services | `GET /api/services` |
| `/services` | Browse & filter services/technicians | `GET /api/services`, `GET /api/technicians`, `GET /api/categories` |
| `/technicians/[id]` | Technician profile & booking CTA | `GET /api/technicians/:id` |
| `/auth/register` | Role selection & registration form | `POST /api/auth/register` |
| `/auth/login` | Login form | `POST /api/auth/login` |
| `/dashboard/customer` | Customer overview & booking history | `GET /api/bookings`, `GET /api/payments` |
| `/dashboard/customer/bookings/[id]/pay` | Payment initiation page | `POST /api/payments/create` |
| `/payment/success` & `/payment/cancel` | Payment outcome pages | (Updates UI based on URL params/session) |
| `/dashboard/technician` | Technician overview & availability | `GET /api/technician/profile`, `GET /api/technician/availability` |
| `/dashboard/technician/bookings` | Manage incoming bookings | `GET /api/technician/bookings`, `PATCH /api/technician/bookings/:id` |
| `/dashboard/admin` | Admin overview & user management | `GET /api/admin/users`, `GET /api/admin/bookings` |
| `/dashboard/admin/categories` | Manage service categories | `GET /api/admin/categories`, `POST /api/admin/categories` |

---

## Data Models & State Management

Instead of database tables, your frontend must define strict **TypeScript Interfaces** matching the backend schema. You must manage this data efficiently:

- **`User`**: ID, name, email, role, status (active/banned).
- **`TechnicianProfile`**: ID, userId, bio, skills, experience, hourlyRate, rating, profileImage.
- **`Service`**: ID, name, description, basePrice, categoryId.
- **`Booking`**: ID, customerId, technicianId, serviceId, scheduledTime, status (requested/accepted/declined/paid/in_progress/completed/cancelled).
- **`Payment`**: ID, bookingId, amount, method, provider (Stripe/SSLCommerz), status (pending/completed/failed), transactionId.
- **`Review`**: ID, bookingId, technicianId, customerId, rating, comment.

> 💡 **State Management Rule**: Use **TanStack Query (React Query)** or **SWR** for all server-state data fetching (to handle caching, loading, and error states automatically). Use **Zustand** or **React Context** only for global client-side state (e.g., multi-step booking form state, mobile sidebar toggle).

---

## Flow Diagrams & UI Considerations

### 🔧 Customer Journey
```text
[Register/Login] → [Browse Services] → [View Technician Profile] 
       ↓
[Select Service & Time Slot] → [Submit Booking Request]
       ↓
[Wait for Technician Acceptance] → [Stripe/SSLCommerz Redirect]
       ↓
[Payment Success Page] → [Track Booking Status] → [Leave Review]
```
> **UI Focus**: The time-slot picker must clearly show available vs. booked slots. Use toast notifications for booking status changes. Ensure the "Cancel Booking" button is only visible/enabled when the status allows it (before `IN_PROGRESS`).

### 🛠️ Technician Journey
```text
[Register/Login] → [Setup Profile & Services] → [Set Availability Calendar]
       ↓
[View Incoming Booking Requests] → [Click Accept/Decline]
       ↓
[Customer Pays] → [Mark "In-Progress"] → [Mark "Completed"]
```
> **UI Focus**: The availability scheduler should be intuitive (e.g., clicking a day to add time blocks). Use optimistic UI updates or React Query invalidation to instantly reflect booking status changes without a full page reload.

### 📊 Booking Status (UI Badges)
- `REQUESTED` → Yellow/Orange Badge (Technician sees Accept/Decline buttons)
- `ACCEPTED` → Blue Badge (Customer sees "Pay Now" button)
- `DECLINED` → Red Badge
- `PAID` → Purple Badge (Technician sees "Start Job" button)
- `IN_PROGRESS` → Green Badge (Technician sees "Complete Job" button; Customer cannot cancel)
- `COMPLETED` → Gray Badge (Customer sees "Leave Review" button)
- `CANCELLED` → Dark Red Badge

---

## ⚠️ Mandatory Frontend Requirements (Recap)

1. **API Integration Doc**: Provide an `API_INTEGRATION.md` mapping your frontend components to backend endpoints.
2. **UI Error Handling**: All form errors and API failures must show user-friendly feedback (Toasts, inline errors, Error Boundaries).
3. **Commits**: 20 meaningful frontend commits (e.g., `feat: add availability calendar for technicians`, `fix: prevent booking past time slots`).
4. **Form Validation**: **Zod + React Hook Form** is mandatory for all inputs.
5. **Admin Credentials**: Provide working admin credentials for testing.
6. **Payment UI**: Real Stripe/SSLCommerz frontend flow (redirect to gateway, handle success/cancel routes). Fake "Cash on Delivery" UI is **NOT** accepted.

---

## 📦 Submission Checklist

- [ ] Frontend GitHub Repo (with at least 20 meaningful commits)
- [ ] Live Frontend URL (Deployed on Vercel)
- [ ] Backend API URL (Documented in README)
- [ ] Demo Video (3-5 mins, covering all 3 roles, validation, and payment flow)
- [ ] Admin Credentials (Listed in README)

**Good luck! Build a blazing-fast, accessible, and beautiful Next.js frontend you're proud of.** 🚀
