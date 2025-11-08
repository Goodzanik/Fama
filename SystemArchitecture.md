# Fama Technical Specification Document

## Project Name: Fama

## Product Manager: [Hazeenice]

## Version: v1.0

## Document Date: November 2025

## Summary:

Fama is a digital agribusiness management and marketplace platform that connects farmers, buyers, and investors. It provides farmers with digital tools to manage their farms, list produce, access funding or insurance, and sell their goods securely. Buyers can discover verified produce listings and transact easily, while investors can track farm projects and monitor ROI.

## System Goals

Empower 5,000 small to mid-scale farmers with digital tools to manage production, inventory, and marketing in Q1

Create a transparent marketplace for agricultural produce with over 4,000 users in Q1

Enable investors to discover credible farm project

Simplify logistics, communication, and payments between parties to boost trust and scalability

Improve access to agricultural insights and government programs with the help of AI Agents

## Key User Roles

Farmer / Farm Management Team: Manages farm operations, creates listings, tracks inventory, interacts with buyers/investors

Buyer: Searches for produce, filters listings, chats with sellers, makes payments

Investor: Views verified farms, invests in projects, tracks ROI analytics

AI Agent / System Assistant: Provides recommendations, generates insights, assists users in navigating and managing data

## Functional Requirements (FR)

| ID     | Feature               | Functional Requirement Description |
|--------|-----------------------|------------------------------------|
| FR-001 | Profile Creation      | Users (Farmer, Buyer, Investor) can register and create profiles with required fields and upload documents for verification. |
| FR-002 | Language Switch       | The platform must support English and selected local languages (e.g., Yoruba, Hausa, Igbo, Pidgin) using a language selector. |
| FR-003 | Project Management    | Farmers can create and manage farm projects, track activities, and update inventory levels. |
| FR-004 | Access Funding/Insurance | Display list of available funding/insurance options integrated from government or partner APIs. |
| FR-005 | Crop Listing          | Farmers can list crops before harvesting, specify estimated dates, and set prices. |
| FR-006 | Notifications         | Notify users on key actions such as payment confirmation, new messages, and funding availability. |
| FR-007 | Privacy Control       | Farmers can set visibility (public/private) on their inventory and projects. |
| FR-008 | Chat System           | Enable secure real-time messaging between farmers, buyers, and investors. |
| FR-009 | Payments              | Integrate secure payment gateway (Paystack/Flutterwave) for transactions. |
| FR-010 | News Feed             | Display agricultural news via integrated RSS/News API. |
| FR-011 | Account Verification  | Enable users to verify identity (email, BVN, NIN, or government ID). |
| FR-012 | Filtering System      | Buyers can filter listings by crop type, price, location, and farm rating. |
| FR-013 | Logistics Selection   | Buyers can choose logistics partners integrated with Fama for delivery. |
| FR-014 | Investment Dashboard  | Investors can view analytics showing farm ROI, performance, and payout. |
| FR-015 | AI Data Assistant     | AI Agent can collect structured farm data and provide insights. |

## System Architecture

### Architecture Style
FAMA uses a **modular client-server architecture** built around a **RESTful API**.  
The backend communicates with the frontend via secure **HTTPS (SSL)** endpoints using **JSON** payloads.

**Key Design Principles**
- Scalable and modular services (microservice-ready)
- Secure authentication and role-based authorization
- Reusable frontend components with responsive design
- Cloud-hosted database and media storage

### Recommended Tech Stack:

- Frontend: React.js / Next.js (Web), React Native (Mobile)

- Backend: Node.js + Express.js (API Layer)

- Database: PostgreSQL (Relational) or MongoDB (Document-based)

- Realtime Chat: Firebase Realtime DB or Socket.io

- Payment: Paystack / Flutterwave

- Translation: Google i18n / Google Cloud Translate

- Hosting: AWS (EC2, S3, RDS) or Render

- Authentication: JWT + bcrypt for hashing

## Detailed Technical Specifications

### Frontend Components

| Component | Description | Key Features / Functions |
|------------|--------------|---------------------------|
| **User Registration Form** | Collects user details such as name, email, location, user type, and verification documents. | - Client-side form validation<br>- File/document upload<br>- Multi-role onboarding (Farmer, Buyer, Investor) |
| **Profile Page** | Displays user profile, farm details, and verification status. | - Editable profile info<br>- Toggle visibility (public/private)<br>- View verification badge |
| **Language Selector** | Dropdown/toggle for language change. | - Stores preference in local storage<br>- Integrates Google Translate API<br>- Updates text dynamically |
| **Farmer Dashboard** | Overview of projects, inventory, and notifications. | - Visual charts for crop yield<br>- Quick actions (Add Project, New Listing)<br>- Alerts for funding or insurance |
| **Listings Page** | Shows all available farm produce. | - Filter by crop type, price, or location<br>- Image grid view<br>- “Contact Seller” button triggers chat |
| **Chat Interface** | Enables real-time messaging between users. | - Socket.io integration<br>- Typing indicator<br>- Message timestamp and status |
| **Payment Page** | Checkout interface for buying/investing. | - Secure form linked to payment gateway<br>- Transaction reference display<br>- Post-payment confirmation |
| **Notification Panel** | Displays updates and alerts. | - Push/in-app notifications<br>- Read/unread state<br>- Timestamped messages |
| **News Feed** | Displays agricultural updates and insights. | - Scrollable feed<br>- Category filters (Funding, Market, Research)<br>- External news API integration |
| **Investor Dashboard** | Shows ROI analytics and portfolio details. | - ROI charts (bar/pie)<br>- Active investments list<br>- Payment history tracking |

### Backend Component

| Module | Description | Main Responsibilities |
|---------|--------------|-----------------------|
| **Authentication Service** | Handles registration, login, and verification. | - JWT-based authentication<br>- Role-based access control<br>- Password hashing with bcrypt |
| **User Service** | Manages user profiles and verification data. | - CRUD operations for users<br>- Profile photo & document upload (AWS S3)<br>- Verification workflows |
| **Farm Management Service** | Controls farm creation, projects, and inventory data. | - Create/update farm details<br>- Manage farm projects<br>- Store yield and production metrics |
| **Listing Service** | Manages produce listings and availability. | - CRUD for listings<br>- Track sale status<br>- Manage listing expiration |
| **Chat Service** | Provides real-time messaging. | - Socket.io / Firebase integration<br>- Store message history in DB<br>- Support one-on-one and group chats |
| **Payment Service** | Integrates payment gateway for transactions. | - Initialize/verify payments (Paystack/Flutterwave)<br>- Store transaction records<br>- Handle webhook callbacks |
| **Notification Service** | Sends updates across email, SMS, and in-app channels. | - Twilio/SendGrid API integration<br>- Store and mark notifications as read<br>- Push notification handler |
| **News Service** | Fetches and displays news articles. | - Integrate News API / RSS feeds<br>- Cache articles for faster retrieval |
| **Analytics Service** | Generates farm and investment insights. | - Query farm & investment metrics<br>- Calculate ROI, yield performance |
| **Localization Service** | Handles text translation and localization. | - Uses Google Translate API<br>- Manages translation files (.json)<br>- Detects preferred language |

## Detailed Database Schema

### Users
| Field | Type | Description |
|--------|------|-------------|
| user_id | UUID | Primary Key |
| name | String | Full name |
| email | String | Unique user email |
| password | String | Hashed password |
| role | Enum (Farmer, Buyer, Investor) | Role type |
| verified_status | Boolean | Account verification status |
| created_at | Timestamp | Registration date |

### FarmProfiles
| Field | Type | Description |
|--------|------|-------------|
| farm_id | UUID | Primary Key |
| user_id | UUID | Foreign Key (Users) |
| location | String | Farm location |
| size | Decimal | Farm size (hectares) |
| holdings | Text | List of crops/assets |
| description | Text | Farm bio |

### Projects
| Field | Type | Description |
|--------|------|-------------|
| project_id | UUID | Primary Key |
| farm_id | UUID | FK (FarmProfiles) |
| title | String | Project title |
| status | Enum (Active, Completed) | Current state |
| start_date | Date | Project start date |
| inventory_data | JSON | Crop data or yield |

### Listings
| Field | Type | Description |
|--------|------|-------------|
| listing_id | UUID | Primary Key |
| farm_id | UUID | FK (FarmProfiles) |
| crop_type | String | Crop name |
| quantity | Integer | Available units |
| price | Decimal | Unit price |
| harvest_date | Date | Expected harvest date |
| status | Enum (Available, Sold) | Listing status |

### Messages
| Field | Type | Description |
|--------|------|-------------|
| message_id | UUID | Primary Key |
| sender_id | UUID | FK (Users) |
| receiver_id | UUID | FK (Users) |
| content | Text | Message text |
| timestamp | Timestamp | Message time |
| read_status | Boolean | True if read |

### Payments
| Field | Type | Description |
|--------|------|-------------|
| payment_id | UUID | Primary Key |
| payer_id | UUID | FK (Users) |
| payee_id | UUID | FK (Users) |
| amount | Decimal | Transaction amount |
| currency | String | e.g. NGN |
| status | Enum (Pending, Success, Failed) | Payment state |
| reference | String | Payment reference from gateway |
| created_at | Timestamp | Transaction time |

### Investments
| Field | Type | Description |
|--------|------|-------------|
| investment_id | UUID | Primary Key |
| investor_id | UUID | FK (Users) |
| farm_id | UUID | FK (FarmProfiles) |
| amount | Decimal | Investment amount |
| roi | Decimal | Return on Investment |
| status | Enum (Active, Completed) | Investment status |
| created_at | Timestamp | Date of investment |

### Notifications
| Field | Type | Description |
|--------|------|-------------|
| notification_id | UUID | Primary Key |
| user_id | UUID | FK (Users) |
| type | Enum (Payment, Message, Update) | Notification category |
| content | Text | Notification message |
| is_read | Boolean | Read status |
| created_at | Timestamp | Notification time |

## API Endpoints

| Purpose | Endpoint | Method | Description |
|----------|-----------|---------|-------------|
| User Registration | `/api/users/register` | POST | Create new user |
| Login | `/api/users/login` | POST | Authenticate user |
| Verify Account | `/api/users/verify` | POST | Update verification status |
| Create Farm | `/api/farms` | POST | Add farm profile |
| Get Farm Info | `/api/farms/:id` | GET | Retrieve farm details |
| Add Project | `/api/projects` | POST | Create new project |
| Get Projects | `/api/projects/:farmId` | GET | View all farm projects |
| List Crop | `/api/listings` | POST | Create new listing |
| Get Listings | `/api/listings` | GET | Fetch available listings |
| Chat | `/api/messages` | POST/GET | Send or retrieve messages |
| Make Payment | `/api/payments/initiate` | POST | Start transaction |
| Verify Payment | `/api/payments/verify` | POST | Confirm payment |
| Get News | `/api/news` | GET | Retrieve agricultural updates |

## Third-Party Integrations

| Service | Use Case | Integration Method |
|----------|-----------|--------------------|
| Paystack / Flutterwave | Payment gateway | REST API |
| Firebase / Socket.io | Real-time chat | WebSocket |
| Google Maps | Farm location | Map Embed + Geocoding API |
| Twilio / SendGrid | Notifications | SMS/Email API |
| Google Translate API | Localization | Translation API |
| News API | News feed | REST API |

## Technical Feasibility & Constraints
### Feasibility: All features can be implemented using existing tools/APIs.

### Scalability: Microservice-ready architecture for future scaling.

### Security:
- Use HTTPS across all communications.

- Apply JWT for session management.

- Sanitize inputs to prevent SQL Injection/XSS.

### Constraints:

- Internet connectivity dependency for farmers in rural areas.

- Initial language support may be limited to top 3 local languages.

## Future Enhancements
- AI-powered farm analytics and yield prediction.

- IoT sensor integration for precision farming.

- Offline-first mobile experience.

- Blockchain for transparent transaction and traceability.



