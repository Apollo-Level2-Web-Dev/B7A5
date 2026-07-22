
# Assignment 5 - RentNest Frontend 🏠
**"Find & List Rental Properties with Ease"**

---

## Project Overview

RentNest is a modern, responsive **Next.js frontend application** for a rental property marketplace. Landlords can list properties, manage availability, and approve or reject rental requests via an intuitive dashboard. Tenants can browse listings with advanced filtering, submit rental requests, and complete secure payments. Admins oversee the entire platform through a comprehensive moderation dashboard. 

> 💡 **Note**: This is a **frontend-only** assignment. You will consume a backend API (your own from a previous assignment, a partner's, or a provided mock API).

---

## Roles & Permissions

| Role | Description | Frontend UI Expectations |
|------|-------------|-----------------|
| **Tenant** | Users looking for rental properties | Public browsing, interactive request forms, payment checkout flow, review submission, protected tenant dashboard. |
| **Landlord** | Property owners who list rentals | Protected landlord dashboard, property CRUD forms (with image upload UI), request approval/rejection toggles, tenant history views. |
| **Admin** | Platform moderators | Protected admin dashboard, user management tables (ban/unban actions), global platform statistics, content moderation UI. |

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
- **Responsive Property Grid**: Display properties with optimized images (`next/image`), price, location, and basic amenities.
- **Advanced Search & Filter**: Sidebar or top-bar filters for location, price range, property type, and amenities with real-time UI updates.
- **Property Details Page**: Comprehensive view with image gallery, description, landlord info, and a "Request to Rent" call-to-action (CTA).
- **Loading & Error States**: Skeleton loaders for data fetching and graceful `error.tsx` fallbacks.

### Tenant Features
- **Auth Flows**: Registration and login forms with Zod validation and inline error messages.
- **Rental Request Flow**: Interactive form/modal to submit a request. If approved, a clear "Proceed to Payment" CTA.
- **Payment Integration**: Seamless redirect to **Stripe Checkout** or **SSLCommerz** gateway. Dedicated `/payment/success` and `/payment/cancel` pages with clear UI feedback.
- **Tenant Dashboard**: View rental request history (with status badges: Pending, Approved, Rejected, Active), payment history table, and a form to leave reviews after completion.

### Landlord Features
- **Landlord Dashboard**: Overview of total properties, active requests, and earnings.
- **Property Management**: Forms to create, edit, and remove listings. Include UI for image URL uploads and availability toggles.
- **Request Management**: A dedicated table/list to view incoming requests with "Approve" and "Reject" action buttons (triggering toast notifications on success).

### Admin Features
- **Admin Dashboard**: Global overview of platform health (total users, properties, pending requests).
- **User Management**: Data table of all users with search, pagination, and "Ban/Unban" action buttons.
- **Content Moderation**: Views to inspect all listings and rental requests across the platform.

---

## Frontend Routes & API Integration

> ⚠️ **Note**: These are suggested Next.js App Router paths. You must map these to your backend API endpoints.

| Next.js Route | Component/Feature | Backend API Consumption |
|---------------|-------------------|-------------------------|
| `/` | Home page with featured properties | `GET /api/properties` |
| `/properties` | Browse & filter properties | `GET /api/properties`, `GET /api/categories` |
| `/properties/[id]` | Property details & request CTA | `GET /api/properties/:id` |
| `/auth/register` | Role selection & registration form | `POST /api/auth/register` |
| `/auth/login` | Login form | `POST /api/auth/login` |
| `/dashboard/tenant` | Tenant overview & request history | `GET /api/rentals`, `GET /api/payments` |
| `/dashboard/tenant/requests/[id]/pay` | Payment initiation page | `POST /api/payments/create` |
| `/payment/success` & `/payment/cancel` | Payment outcome pages | (Updates UI based on URL params/session) |
| `/dashboard/landlord` | Landlord overview & property list | `GET /api/landlord/properties` |
| `/dashboard/landlord/properties/new` | Create property form | `POST /api/landlord/properties` |
| `/dashboard/landlord/requests` | Manage incoming requests | `GET /api/landlord/requests`, `PATCH /api/landlord/requests/:id` |
| `/dashboard/admin` | Admin overview & user management | `GET /api/admin/users`, `PATCH /api/admin/users/:id` |

---

## Data Models & State Management

Instead of database tables, your frontend must define strict **TypeScript Interfaces** matching the backend schema. You must manage this data efficiently:

- **`User`**: ID, name, email, role, status (active/banned).
- **`Property`**: ID, title, description, price, location, category, amenities, landlordId, images.
- **`RentalRequest`**: ID, propertyId, tenantId, status (pending/approved/rejected/active/completed), dates.
- **`Payment`**: ID, rentalRequestId, amount, method, provider (Stripe/SSLCommerz), status (pending/completed/failed), transactionId.
- **`Review`**: ID, propertyId, tenantId, rating, comment.

> 💡 **State Management Rule**: Use **TanStack Query (React Query)** or **SWR** for all server-state data fetching (to handle caching, loading, and error states automatically). Use **Zustand** or **React Context** only for global client-side state (e.g., mobile sidebar toggle, transient UI states).

---

## Flow Diagrams & UI Considerations

### 🏠 Tenant Journey
```text
[Register/Login] → [Browse Properties] → [View Details] 
       ↓
[Submit Request Form (Zod Validation)] → [Wait for Approval UI]
       ↓
[Approved: "Pay Now" CTA] → [Stripe/SSLCommerz Redirect]
       ↓
[Payment Success Page] → [Leave Review Form]
```
> **UI Focus**: Show loading spinners during form submission. Use toast notifications for success/failure. Ensure the payment redirect flow handles network drops gracefully.

### 🏘️ Landlord Journey
```text
[Register/Login] → [Dashboard Overview] → [Create Listing Form]
       ↓
[View Incoming Requests Table] → [Click Approve/Reject]
       ↓
[Toast Notification: "Request Approved"] → [Tenant can now pay]
```
> **UI Focus**: Use optimistic UI updates or React Query invalidation to instantly reflect status changes in the table without a full page reload.

### 📊 Rental Request Status (UI Badges)
- `PENDING` → Yellow/Orange Badge
- `APPROVED` → Blue Badge (Shows "Pay Now" button)
- `REJECTED` → Red Badge
- `ACTIVE` → Green Badge (Shows "Leave Review" button)
- `COMPLETED` → Gray Badge

---

## ⚠️ Mandatory Frontend Requirements (Recap)

1. **API Integration Doc**: Provide an `API_INTEGRATION.md` mapping your frontend components to backend endpoints.
2. **UI Error Handling**: All form errors and API failures must show user-friendly feedback (Toasts, inline errors, Error Boundaries).
3. **Commits**: 20 meaningful frontend commits (e.g., `feat: add zod validation to login`, `fix: stripe redirect loop`).
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
