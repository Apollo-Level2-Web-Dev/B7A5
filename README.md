# Assignment 5 - Frontend Project 

## 🔍 Find Your Assignment

> 💡 Check your Student ID by clicking your **profile image** on the [Programming Hero Website](https://web.programming-hero.com/profile).

| Last Digit of Student ID | Assignment |
|:------------------------:|------------|
| **0, 1, 2, 3** | [RentNest](./1-RentNest-Frontend.md) 🏠 |
| **4, 5, 6** | [GearUp](./2-GearUp-Frontend.md) 🏋️ |
| **7, 8, 9** | [FixItNow](./3-FixItNow-Frontend.md) 🔧 |

---

## ⚠️ Mandatory Requirements

> [!CAUTION]
> **MANDATORY - READ CAREFULLY**
> 
> The following **SIX requirements are MANDATORY**:
> 1. **API Integration & Documentation** - Consume all required backend endpoints. Provide a brief `API_INTEGRATION.md` file mapping frontend components to backend endpoints.
> 2. **Consistent UI Error Handling** - All API errors and form validation errors must show user-friendly, structured UI feedback (e.g., Toast notifications, inline form errors, Error Boundaries).
> 3. **Commits** - 20 meaningful *frontend* commits with descriptive messages (e.g., `feat: add role-based dashboard layout`, `fix: resolve stripe checkout redirect loop`).
> 4. **Form Validation** - Client-side validation on all forms using **Zod + React Hook Form** (or Next.js Server Actions with Zod), with clear error messages.
> 5. **Admin Credentials** - Provide working admin email & password to test the deployed frontend application.
> 6. **Payment Integration** - Must integrate the frontend flow for **Stripe** (Checkout/Elements) or **SSLCommerz**. Simulated/fake payments (Cash on Delivery, Pay Later) are **NOT** accepted. Must handle success/cancel redirect pages.
>
> ❌ **Failure to complete any of these = 0 MARKS**

---

## 📊 Marks Distribution

| # | Category | Weight | Details |
|:-:|----------|:------:|---------|
| 1 | UI/UX Design & Responsiveness | 20% | Modern, clean UI, mobile-first responsive design, loading skeletons, toast messages, dark/light mode (optional but bonus) |
| 2 | State Management & Data Fetching | 20% | Proper use of Next.js App Router (Server/Client Components), TanStack Query (or SWR), and global state (Zustand/Context) where appropriate |
| 3 | Commit History | 10% | 20 meaningful frontend commits with conventional commit standards |
| 4 | Error Handling & Validation | 10% | Zod validation, React Hook Form, UI error boundaries, graceful 404/500 pages |
| 5 | Core Functionality | 20% | Auth flows (JWT storage, protected routes via Middleware), role-based UI rendering, full CRUD via UI |
| 6 | Payment Integration | 10% | Frontend payment flow (Stripe Checkout/SSLCommerz redirect), handling success/failure routes, updating UI post-payment |
| 7 | Video Explanation | 10% | 7-10 min frontend walkthrough video |

---

## 📅 Timeline

| Deadline | Maximum Marks |
|----------|:-------------:|
| **August 2, 2026, 11:59 PM** | 60 Marks |
| **August 3, 2026, 11:59 PM** | 50 Marks |
| **August 4 to August 24, 2026, 11:59 PM** | 30 Marks |

> **Note:** If you want to join early job placement, you must obtain at least **55 marks** within the August 2 deadline (60 Marks) or **42 marks** within the August 3 deadline (50 Marks).

---

## 📦 What to Submit

| Item | Required |
|------|:--------:|
| Frontend GitHub Repo |
| Live Frontend URL (Vercel) |
| Backend API URL (Your own or provided) |
| Demo Video (7-10 min) |
| Admin Credentials |

**Example:**
```text
Frontend Repo    : https://github.com/your-username/rentnest-frontend
Live Frontend    : https://rentnest-app.vercel.app
Backend API      : https://rentnest-api.vercel.app (or mock data setup)
Demo Video       : https://drive.google.com/file/d/xxx/view
Admin Email      : admin@rentnest.com
Admin Password   : admin123
```

---

## 🎥 Video Explanation Guide

**Language:** English or Bengali

**What to Cover:**
1. Project overview & Next.js architecture (App Router, folder structure).
2. Demonstrate all 3 roles working via the **actual UI** (Customer/Tenant, Provider/Landlord/Technician, Admin). Show how the UI adapts per role.
3. Show CRUD operations via the UI (e.g., creating an item, updating status, deleting).
4. Demonstrate form validation (show an error triggering) and error handling (e.g., network error toast).
5. Walk through the Payment Integration flow (from clicking "Pay" to the success page).
6. Briefly explain one technical challenge you solved (e.g., middleware auth, state management, payment webhook handling).

**Recording Options:**
- **Loom** - Record & share link directly.
- **OBS** - Record & upload to Google Drive (set "Anyone with link" access).

---

## 🛠️ Tech Stack

### Frontend
| Technology | Purpose |
|------------|---------|
| **Next.js** (App Router) | React Framework, Routing, Server Components |
| **TypeScript** | Type safety (Mandatory) |
| **Tailwind CSS** | Styling (Shadcn UI, DaisyUI, or custom components allowed) |
| **React Hook Form + Zod** | Form state management and schema validation |
| **Fetch**, **TanStack Query (React Query)** or **SWR** | Server state management and data fetching |
| **Auth.js** or **Custom JWT Middleware** | Authentication and protected routes |
| **Stripe.js** or **SSLCommerz JS** | Frontend payment gateway integration |

### Deployment
| Service | Purpose |
|---------|---------| 
| **Vercel/Render** | Frontend application deployment (Recommended) |

---

## 🎯 Key Rules

- **Roles**: Each project has 3 fixed roles. The UI must dynamically render navigation, dashboards, and actions based on the authenticated user's role. Use Next.js Middleware for route protection.
- **Payment**: Payment integration is **MANDATORY**. The frontend must successfully initiate the payment (e.g., redirect to Stripe Checkout or SSLCommerz gateway) and handle the return URL (success/cancel pages) gracefully, updating the UI accordingly.
- **Backend Dependency**: You may connect to your own backend from a previous assignment, a partner's backend, or a provided mock backend. If using a mock, document it clearly, but real API integration is highly preferred.
- **Performance**: Optimize images using `next/image`, implement loading states (`loading.tsx`), and handle errors gracefully (`error.tsx`).

---

## ⚠️ Important Notes

> **Plagiarism** = 0 Marks. All UI components, logic, and integrations must be your original work. Using AI to generate entire pages without understanding or customization will result in mark deduction.

**Good luck! Build a blazing-fast, beautiful, and robust Next.js frontend you're proud of.** 🚀
