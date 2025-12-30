# 🤝 Manfaa – B2B Service Exchange Platform  

## Overview  
**Manfaa** is a B2B service exchange platform that enables companies to trade professional services in Saudi Arabia.  
It facilitates matching service providers with service requesters through two exchange mechanisms: **Token-based payments** or **Barter (service-for-service)**.  

The platform manages the complete lifecycle from posting requests, competitive bidding, secure contract management with **token escrow**, to building trust through reviews.  

---

## Features  

### Company  
- Sign up / Login.  
- Create comprehensive company profile (name, industry, team size, description).  
- Manage company skills portfolio (assign/remove from 10+ skills).  
- **Service Requests**:
  - Create requests with **Token**, **Barter**, or **Either** exchange type.
  - Specify deliverables (50-500 chars), timeline, and budget.
  - Update or delete **OPEN** requests.
  - Browse all available service requests.
  - Filter by category (10 categories), status, exchange type.
  - Filter by token range (min/max budget).
  - Filter by date range (start/end dates).
  - Sort by token amount (ASC/DESC).
  - View request with all submitted bids.
- **Bidding**:
  - Submit competitive bids with detailed proposal (50-500 chars).
  - Include pricing, timeline, and deliverables.
  - Update or delete **PENDING** bids.
  - View all submitted bids.
  - Accept or reject received bids (as requester).
  - Receive email notifications on acceptance/rejection.
- **Contracts**:
  - Create contracts from accepted bids.
  - Bilateral approval required (both parties must accept).
  - Track contract status: **PENDING → ACTIVE → COMPLETED**.
  - Mark delivery complete with proof.
  - Extend contract time once (50% of original duration).
  - Reject contracts (releases tokens, reopens request).
  - Delete pending contracts.
  - **Token Escrow**: Tokens held safely until completion.
- **Credits**:
  - View token balance, total earned, total spent.
  - View transaction history (all incoming/outgoing).
  - Track transaction status: PENDING → ACCEPTED/CANCELLED.
  - Purchase tokens via payment gateway.
  - Secure three-state escrow: Hold → Release/Transfer.
- **Reviews**:
  - Rate completed contracts (1-5 stars, decimals allowed).
  - Write detailed review descriptions (min 10 chars).
  - View received reviews (reputation building).
  - View written reviews (feedback tracking).
  - Update or delete own reviews.
  - Search reviews by keyword.
  - Filter reviews by exchange type (TOKENS/BARTER).
  - Sort company reviews best to worst.
  - One review per contract (prevents duplicates).
- **Subscriptions**:
  - Subscribe monthly (120 SAR/month) or yearly (1,200 SAR/year).
  - Benefits: Priority search, higher support priority, premium badge.
  - View subscription status and renewal dates.
  - Cancel active subscriptions (active until period end).
- **Support Tickets**:
  - Create tickets for: CONTRACT, SUBSCRIPTION, PLATFORM, SUGGESTION.
  - Auto priority: CONTRACT=HIGH, Subscribers get higher priority.
  - Update ticket details (only when OPEN).
  - Delete open tickets.
  - Track status: OPEN → RESOLVED → CLOSED.
  - Receive email notifications on resolution.
- Automated email notifications for:
  - Bid acceptance/rejection with notes.
  - Contract approval, activation, completion, cancellation.
  - Review reminders after completion.
  - Token refund confirmations.
  - Ticket resolution updates.

### Admin  
- View all users.  
- Add new admins.  
- Update user details.  
- Delete users and company profiles.  
- **Categories** (10 categories):
  - Web Development, Mobile Development, Digital Marketing.
  - Graphic Design, Content Writing, Video Production.
  - Data Analysis, IT Consulting, Cloud Services, Cybersecurity.
  - Add, update, delete categories.
- **Skills** (10+ skills):
  - React.js, Node.js, Python, Java, Flutter.
  - AWS, Docker, PostgreSQL, MongoDB, Machine Learning.
  - Add, update, delete skills.
  - View skills by company.
  - Search skills by keyword.
- **Monitoring**:
  - View all reviews (search, filter, sort).
  - View all support tickets by priority.
  - Resolve support tickets.
  - View all credit transactions.
  - View all subscriptions.
  - View all company credits.
- **Operations**:
  - Process credit refunds for disputed contracts.
  - Add credits to companies manually.
  - Handle contract rejections and automatic refunds.
  - Create pending reviews for completed contracts.
  - Access system-wide reports and analytics.

---

## Tech Stack  
- **Backend:** Spring Boot 3, Spring Security, Hibernate/JPA  
- **Database:** MySQL  
- **Email Service:** JavaMailSender (SMTP)  
- **Payment Gateway:** Integration ready (Moyasar/Stripe compatible)  
- **Authentication:** JWT (JSON Web Tokens) with HTTP-only cookies  
- **Password Encryption:** BCrypt  
- **Authorization:** Role-based (`COMPANY`, `ADMIN`)  
- **Build Tool:** Maven  

---

## Roles & Example Endpoints  

### Public  
- `POST /api/v1/company/register` → Register a company.  
- `POST /api/v1/auth/login` → User login.  

### Company  
- `GET /api/v1/service-request/get-all` → Get all service requests.  
- `POST /api/v1/service-request/token/{companyId}` → Create token-based request.  
- `POST /api/v1/bid/create/{companyId}/{requestId}` → Submit a bid.  
- `POST /api/v1/bid/accept/{bidId}/{userId}` → Accept a bid.  
- `POST /api/v1/contract/create` → Create contract from accepted bid.  
- `POST /api/v1/contract/complete/{contractId}` → Mark delivery complete.  
- `POST /api/v1/reviews/add/{reviewedCompanyId}/{contractId}` → Add review.  
- `POST /api/v1/subscription/monthly/{companyProfileId}` → Subscribe monthly (120 SAR).  

### Admin  
- `GET /api/v1/user/get-all` → Get all users.  
- `DELETE /api/v1/user/delete/{userId}` → Delete a user.  
- `POST /api/v1/category/add` → Add service category.  
- `POST /api/v1/skills/add` → Add skill to library.  
- `POST /api/v1/transaction/refund/{contractId}` → Process credit refund.  
- `POST /api/v1/reviews/handle-rejection/{contractAgreementId}` → Handle rejection & refund.  

---

## Diagrams

### ER Diagram
![ER Diagram](link-to-your-er-diagram.png)

> This ER Diagram shows all main entities in Manfaa, including **Users, CompanyProfiles, CompanyCredits, ServiceRequests, ServiceBids, ContractAgreements, Reviews, CreditTransactions, Subscriptions, Tickets, Categories, and Skills**, along with their relationships.  
> It visualizes one-to-one, one-to-many, and many-to-many relations clearly.  

### Use Case Diagram
![Use Case Diagram](link-to-your-usecase-diagram.png)

> The Use Case Diagram illustrates interactions between **Companies and Admins** with the Manfaa system.  
> It highlights key functionalities like **service requests, bidding, contract management with escrow, reviews, credit operations, and subscription handling**.  

---

### Links

- [🎨 Figma Design](link-to-figma)
- [📬 Postman Documentation](link-to-postman)  
- [📊 Presentation (Canva)](link-to-presentation)

---

## Enhancements & Creative Improvements
- **Token Escrow System**: Secure three-state token lifecycle (HOLD → RELEASE/TRANSFER) ensures transaction integrity and payment safety.  
- **Dual Exchange Types**: Flexible payment options (Tokens, Barter, or Either) for diverse B2B business needs.  
- **Bilateral Contract Approval**: Both requester and provider must approve contracts before activation for trust and transparency.  
- **Email Automation**: Automated notifications at every step (bids, contracts, reviews, refunds) keep all parties informed.  
- **Advanced Review System**: Transparent feedback with search, filtering by exchange type, and sorting capabilities.  
- **Subscription Model**: Monthly (120 SAR) and yearly (1,200 SAR) plans with priority features and premium badge.  
- **Smart Ticket Prioritization**: Automatic priority assignment based on category and subscriber status.  
- **Comprehensive Search**: Filter by category, exchange type, token range, date range, and sort by price.  

---

## Summary
Manfaa is designed to be a **full-featured backend solution** for B2B service exchange in Saudi Arabia.  
It balances **service requester convenience, provider opportunities, and admin control**, while integrating **secure token escrow, bilateral contract approval, and comprehensive dispute resolution**.  
With clear data modeling, automated email notifications at every lifecycle stage, and robust review system, Manfaa provides a complete ecosystem for B2B service operations.  

---

# API Endpoints Summary

| Controller | Count |
|---|---:|
| AuthController | 2 |
| UserController | 4 |
| CompanyProfileController | 7 |
| CategoryController | 4 |
| SkillsController | 8 |
| CompanyCreditController | 1 |
| ServiceRequestController | 13 |
| ServiceBidController | 6 |
| ContractAgreementController | 6 |
| ReviewController | 14 |
| CreditTransactionController | 5 |
| SubscriptionController | 4 |
| TicketController | 4 |
| **Total** | **78** |

---

## AuthController (`/api/v1/auth`)
| Method | Path | Description | Name |
|---|---|---|---|
| POST | `/login` | User login (returns JWT token with HTTP-only cookie) | muath |
| POST | `/logout` | User logout (clears JWT cookie) | muath |

---

## UserController (`/api/v1/user`)
| Method | Path | Description | Name |
|---|---|---|---|
| GET | `/get-all` | Get all users (Admin) | muteb |
| POST | `/add` | Add new user/admin (Admin) | muteb |
| PUT | `/update/{userId}` | Update user details (Admin) | muteb |
| DELETE | `/delete/{userId}` | Delete user (Admin) | muteb |

---

## CompanyProfileController (`/api/v1/company`)
| Method | Path | Description | Name |
|---|---|---|---|
| GET | `/get-all` | Get all company profiles | hassan |
| POST | `/register` | Register new company (username, password, email, company details) | hassan |
| PUT | `/update` | Update company profile (current user) | hassan |
| DELETE | `/delete` | Delete company profile (current user) | hassan |
| GET | `/get-companies-full` | Get all companies with full details (skills, reviews, ratings) | hassan |
| GET | `/get-company-full` | Get current company full details | hassan |
| GET | `/get-company-id-full/{companyId}` | Get company by ID with full details | hassan |

---

## CategoryController (`/api/v1/category`)
| Method | Path | Description | Name |
|---|---|---|---|
| GET | `/get` | Get all categories (10 categories) | muteb |
| POST | `/add` | Add category (Admin) | muteb |
| PUT | `/update/{categoryId}` | Update category (Admin) | muteb |
| DELETE | `/delete/{categoryId}` | Delete category (Admin) | muteb |

---

## SkillsController (`/api/v1/skills`)
| Method | Path | Description | Name |
|---|---|---|---|
| GET | `/get-all` | Get all skills (10+ skills available) | muteb |
| POST | `/add` | Add skill to library (Admin) | muteb |
| PUT | `/update/{skillsId}` | Update skill (Admin) | muteb |
| DELETE | `/delete/{skillsId}` | Delete skill (Admin) | muteb |
| POST | `/assign/{userId}/{skillId}` | Assign skill to company profile | muteb |
| DELETE | `/remove/{userId}/{skillId}` | Remove skill from company profile | muteb |
| GET | `/company/{companyId}` | Get all skills for a company | muteb |
| GET | `/search/{keyword}` | Search skills by keyword | muteb |

---

## CompanyCreditController (`/api/v1/credit`)
| Method | Path | Description | Name |
|---|---|---|---|
| GET | `/get-all` | Get all company credits (balance, earned, spent) | muteb |

---

## ServiceRequestController (`/api/v1/service-request`)
| Method | Path | Description | Name |
|---|---|---|---|
| GET | `/get-all` | Get all service requests | hassan |
| POST | `/token/{companyId}` | Create token-based request (requires sufficient balance) | hassan |
| POST | `/barter/{companyId}` | Create barter request (specify desired category) | hassan |
| POST | `/either/{companyId}` | Create either-type request (accepts both payment types) | hassan |
| PUT | `/update/{id}/{requestId}` | Update service request (only OPEN status) | hassan |
| DELETE | `/delete/{requestId}/{id}` | Delete service request (only OPEN status) | hassan |
| GET | `/category/{categoryId}` | Get requests by category | hassan |
| GET | `/status/{status}` | Get requests by status (OPEN/CLOSED/CANCELLED) | hassan |
| GET | `/exchange/{exchangeType}` | Get requests by exchange type (TOKENS/BARTER/EITHER) | hassan |
| GET | `/date-range` | Filter by date range (start & end params, YYYY-MM-DD) | hassan |
| GET | `/token-range` | Filter by token amount range (min & max params) | hassan |
| GET | `/sort/{order}` | Sort by token amount (ASC/DESC) | hassan |
| GET | `/company/{companyId}/request-with-bids/{requestId}` | Get request with all submitted bids | hassan |

---

## ServiceBidController (`/api/v1/bid`)
| Method | Path | Description | Name |
|---|---|---|---|
| GET | `/get-all` | Get all bids | muath |
| POST | `/create/{companyId}/{requestId}` | Submit bid (description, deliverables, hours, dates, price) | muath |
| PUT | `/update/{id}/{bidId}` | Update bid (only PENDING status) | muath |
| DELETE | `/delete/{id}/{bidId}` | Delete bid (only PENDING status) | muath |
| POST | `/accept/{bidId}/{userId}` | Accept bid (closes request, sends email) | muath |
| POST | `/reject/{bidId}/{userId}` | Reject bid with notes (sends email to provider) | muath |

---

## ContractAgreementController (`/api/v1/contract`)
| Method | Path | Description | Name |
|---|---|---|---|
| GET | `/get-all` | Get all contracts | muath |
| POST | `/create` | Create contract (holds tokens in escrow, sends approval email) | muath |
| DELETE | `/delete/{contractId}` | Delete pending contract (releases tokens) | muath |
| POST | `/accept/{contractId}` | Approve contract (both parties must accept to activate) | muath |
| POST | `/reject/{contractId}` | Reject contract (status CANCELLED, tokens released, request reopens) | muath |
| POST | `/complete/{contractId}` | Mark delivery complete (both parties must confirm, tokens transferred) | muath |

---

## ReviewController (`/api/v1/reviews`)
| Method | Path | Description | Name |
|---|---|---|---|
| GET | `/get-all` | Get all reviews (Admin) | hassan |
| GET | `/get/{reviewId}` | Get review by ID | hassan |
| POST | `/add/{reviewedCompanyId}/{contractId}` | Add review (1-5 stars, min 10 chars description) | hassan |
| PUT | `/update/{reviewId}` | Update review (only own reviews) | hassan |
| DELETE | `/delete/{reviewId}` | Delete review (only own reviews) | hassan |
| GET | `/company/{companyId}/received` | Get reviews received by company | hassan |
| GET | `/company/{companyId}/written` | Get reviews written by company | hassan |
| GET | `/company/{companyId}/reviewed-contracts` | Get reviewed contracts by company | hassan |
| GET | `/search/{keyword}` | Search reviews by keyword | hassan |
| GET | `/exchange-type/{exchangeType}` | Filter reviews by exchange type (TOKENS/BARTER) | hassan |
| GET | `/company/{companyId}/best-to-worst` | Get company reviews sorted best to worst (by rating) | hassan |
| POST | `/create-pending-reviews/{contractAgreementId}` | Create pending reviews for completed contract | hassan |
| POST | `/handle-rejection/{contractAgreementId}` | Handle contract rejection and process token refund | hassan |

---

## CreditTransactionController (`/api/v1/transaction`)
| Method | Path | Description | Name |
|---|---|---|---|
| GET | `/get-all` | Get all transactions (Admin) | muteb |
| GET | `/get-by-companyId/{companyId}` | Get company transactions (Admin view) | muteb |
| GET | `/get-my-transactions` | Get current company transactions (PENDING/ACCEPTED/CANCELLED) | muteb |
| POST | `/add-balance` | Add credit to company account (Admin) | muteb |
| POST | `/refund/{contractId}` | Process credit refund for disputed contract (Admin) | muteb |

---

## SubscriptionController (`/api/v1/subscription`)
| Method | Path | Description | Name |
|---|---|---|---|
| GET | `/get-all` | Get all subscriptions (Admin) | hassan |
| POST | `/monthly/{companyProfileId}` | Subscribe monthly (120 SAR/month, priority features) | hassan |
| POST | `/yearly/{companyProfileId}` | Subscribe yearly (1,200 SAR/year, save 2 months) | hassan |
| DELETE | `/cancel/{companyId}/{subscriptionId}` | Cancel subscription (active until period end, no refunds) | hassan |

---

## TicketController (`/api/v1/ticket`)
| Method | Path | Description | Name |
|---|---|---|---|
| GET | `/get-all/{adminId}` | Get all tickets with priority (Admin) | muteb |
| POST | `/create/{companyId}/{contractId}` | Create support ticket (categories: CONTRACT/SUBSCRIPTION/PLATFORM/SUGGESTION) | muteb |
| PUT | `/update/{ticketId}/{companyId}` | Update ticket (only OPEN status) | muteb |
| DELETE | `/delete/{ticketId}/{companyId}` | Delete ticket (only OPEN status) | muteb |

---

## Business Logic & Key Workflows

### Service Exchange Workflow (Token-Based)
1. **Requester** creates token-based service request → System validates sufficient token balance
2. **Provider** searches requests (filter by category, token range, dates) → Submits competitive bid
3. **Requester** reviews all bids → Accepts best bid → Request status: CLOSED, Bid status: ACCEPTED
4. **Requester** creates contract → System **holds tokens in escrow** (PENDING transaction) → Sends approval email to provider
5. **Both parties** approve contract → Contract status: **ACTIVE** → Tokens remain in escrow → Work begins
6. **Provider** completes work → Marks as DELIVERED → Includes delivery proof
7. **Requester** reviews deliverables → Marks as DELIVERED → Contract status: **COMPLETED**
8. **System** transfers tokens from escrow to provider → Transaction status: ACCEPTED → Updates total earned/spent
9. **Both parties** receive review reminder emails → Submit reviews (1-5 stars + description)

### Service Exchange Workflow (Barter)
1. **Requester** creates barter request → Specifies desired service category in exchange
2. **Provider** submits bid → Offers their service in exchange (no tokens involved)
3. **Requester** accepts bid → Creates contract (no token escrow needed)
4. **Both parties** approve contract → Contract status: ACTIVE
5. **Provider** delivers their service → Marks as DELIVERED
6. **Requester** delivers their service → Marks as DELIVERED  
7. **Both parties** have delivered → Contract status: COMPLETED
8. **Both parties** submit reviews → Transparent feedback exchange

### Contract Rejection Workflow
1. **Either party** rejects contract (during PENDING or ACTIVE status)
2. **System** checks exchange type:
   - If TOKENS: Releases held tokens back to requester's balance
   - If BARTER: No token operations needed
3. **System** updates contract status to **CANCELLED**
4. **System** reopens service request to **OPEN** status (can receive new bids)
5. **System** sends cancellation emails to both parties with details

### Credit Refund Workflow (Admin)
1. **Admin** identifies disputed/problematic contract (status: COMPLETED or DISPUTED)
2. **Admin** validates transaction is token-based and in PENDING/ACCEPTED status
3. **Admin** calls refund endpoint → System returns tokens to requester's balance
4. **System** updates transaction status to **CANCELLED**
5. **System** sends refund notification emails to both parties

### Review System Workflow
1. **Contract** reaches COMPLETED status
2. **System** sends review reminder emails to both requester and provider
3. **Companies** submit ratings (1-5 stars, decimals allowed like 4.5) + descriptions (min 10 chars)
4. **System** validates:
   - Contract is COMPLETED or DISPUTED
   - No duplicate review exists (one review per contract)
   - No self-reviews (cannot review own company)
5. **System** saves review → Updates company's average rating → Visible on profile
6. **Companies** can update or delete their own reviews anytime

### Subscription Benefits Workflow
1. **Company** subscribes (monthly 120 SAR or yearly 1,200 SAR)
2. **System** activates subscription → Sets is_active = true, is_subscriber = true
3. **Benefits Applied**:
   - Priority in search results (subscribers appear first)
   - Higher ticket priority (CONTRACT tickets: HIGH, others: MEDIUM)
   - Premium badge on profile
   - Enhanced profile visibility
4. **Auto-renewal** until cancelled
5. **Cancellation** → Remains active until period end → No partial refunds

### Support Ticket Prioritization
**Automatic Priority Assignment:**
- **HIGH Priority**: CONTRACT tickets (always), SUBSCRIPTION tickets (if subscriber)
- **MEDIUM Priority**: PLATFORM tickets (all users), SUBSCRIPTION tickets (non-subscribers), SUGGESTION tickets (if subscriber)
- **LOW Priority**: SUGGESTION tickets (non-subscribers)

**Resolution Flow:**
1. Company creates ticket → Status: OPEN
2. Admin reviews → Investigates issue
3. Admin resolves → Status: RESOLVED → Email sent to company
4. Admin closes → Status: CLOSED

---

## Token Escrow System

### Three-State Token Lifecycle

#### 1. HOLD (Contract Creation)
- **Trigger**: Contract created from accepted bid (token-based)
- **Action**: Tokens deducted from requester's balance
- **Transaction**: Created with **PENDING** status
- **State**: Tokens held in escrow (not available to requester or provider)
- **Purpose**: Ensures requester has committed funds before work begins

#### 2. RELEASE (Contract Cancellation/Rejection)
- **Trigger**: Contract cancelled or rejected by either party
- **Action**: Tokens returned to requester's balance
- **Transaction**: Status updated to **CANCELLED**
- **State**: Requester's purchasing power restored
- **Purpose**: Fair resolution when contract doesn't proceed

#### 3. TRANSFER (Contract Completion)
- **Trigger**: Both parties mark deliverables as complete
- **Action**: Tokens moved from escrow to provider's balance
- **Transaction**: Status updated to **ACCEPTED**
- **Metrics Updated**: 
  - Provider's `total_earned` increases by token amount
  - Requester's `total_spent` increases by token amount
- **State**: Payment finalized and irreversible
- **Purpose**: Secure payment upon successful delivery

---

## Status Workflows

### Service Request Status Flow
```
OPEN → CLOSED → (reopens to OPEN if contract cancelled)
  ↓
CANCELLED (if requester cancels)
```
- **OPEN**: Accepting bids, can update/delete, visible to all
- **CLOSED**: Bid accepted, no more bids, contract creation in progress
- **CANCELLED**: Request cancelled by requester (only when OPEN)

### Bid Status Flow
```
PENDING → ACCEPTED or REJECTED
```
- **PENDING**: Awaiting requester decision, can update/delete
- **ACCEPTED**: Chosen for contract, triggers contract creation
- **REJECTED**: Not selected, provider receives email with rejection notes

### Contract Status Flow
```
PENDING → ACTIVE → COMPLETED
    ↓
CANCELLED (if rejected)
    ↓
DISPUTED (admin review)
```
- **PENDING**: Awaiting bilateral approval, tokens held in escrow
- **ACTIVE**: Both approved, work in progress, can be extended once
- **COMPLETED**: Both delivered, tokens transferred, reviews enabled
- **CANCELLED**: Rejected before completion, tokens refunded, request reopens
- **DISPUTED**: Under admin review (via support ticket)

### Transaction Status Flow
```
PENDING → ACCEPTED or CANCELLED
```
- **PENDING**: Tokens held in escrow during active contract
- **ACCEPTED**: Tokens transferred to provider (contract completed)
- **CANCELLED**: Tokens returned to requester (contract cancelled/refunded)

### Ticket Status Flow
```
OPEN → RESOLVED → CLOSED
```
- **OPEN**: Issue reported, can update/delete, awaiting admin
- **RESOLVED**: Admin responded and fixed, email sent
- **CLOSED**: Finalized by admin

### Subscription Status Flow
```
INACTIVE → ACTIVE → CANCELLED (remains ACTIVE until period end)
```
- **ACTIVE**: Subscription active, benefits applied, auto-renews
- **CANCELLED**: Cancelled by user, active until end of current period

---

## Data Validation Rules

### Service Request Validation
- Title: 10-100 characters
- Description: 50-500 characters
- Deliverables: 50-500 characters
- Start Date: Must be valid YYYY-MM-DD format
- End Date: Must be after start date
- Token Amount: Required for TOKEN and EITHER types, must be positive
- Category: Must be valid category ID (1-10)
- Barter Category: Required for BARTER type only

### Bid Validation
- Description: 50-500 characters
- Deliverables: 50-500 characters
- Estimated Hours: Must be positive number
- Start Date: Cannot be after end date
- End Date: Must allow enough time for estimated hours
- Exchange Type: Must match service request type
- Token Amount: Required for token-based bids, must be positive
- Can only bid on OPEN requests

### Review Validation
- Rating: 1 to 5 (decimals allowed, e.g., 4.5)
- Description: Minimum 10 characters
- Contract must be COMPLETED or DISPUTED
- One review per contract (prevents duplicates)
- Cannot review own company (self-review prevented)
- Can only update/delete own reviews

### Contract Validation
- Request must be CLOSED
- Bid must be ACCEPTED
- Requester must have sufficient tokens (for token-based)
- Both parties must approve to activate
- Extension allowed only once (50% of original duration)

---

## Categories & Skills

### Available Categories (10)
1. **Web Development** - Websites, web apps, frontend/backend
2. **Mobile Development** - iOS, Android, cross-platform apps
3. **Digital Marketing** - SEO, social media, content marketing
4. **Graphic Design** - Logos, branding, UI/UX design
5. **Content Writing** - Blogs, copywriting, technical writing
6. **Video Production** - Editing, animation, promotional videos
7. **Data Analysis** - Business intelligence, data visualization
8. **IT Consulting** - Technology strategy, infrastructure
9. **Cloud Services** - AWS, Azure, cloud migration
10. **Cybersecurity** - Security audits, penetration testing

### Available Skills (10+)
1. **React.js** - Frontend JavaScript library
2. **Node.js** - Backend JavaScript runtime
3. **Python** - General-purpose programming
4. **Java** - Enterprise application development
5. **Flutter** - Cross-platform mobile framework
6. **AWS** - Amazon Web Services cloud platform
7. **Docker** - Containerization technology
8. **PostgreSQL** - Relational database
9. **MongoDB** - NoSQL database
10. **Machine Learning** - AI and predictive models

---

## Security Features

### Authentication
- **JWT Token-based authentication** with 24-hour expiration
- **HTTP-only cookies** to prevent XSS attacks
- **BCrypt password hashing** with salt (10 rounds)
- Secure logout (clears JWT cookie)

### Authorization
- **Role-based access control** (COMPANY, ADMIN)
- Endpoint-level security with `@PreAuthorize`
- **Ownership validation** for all resource access
- Admin-only operations strictly enforced

### Data Protection
- **Password encryption** before database storage
- **Secure token handling** with secret key rotation capability
- **Email validation** to prevent duplicate accounts
- **Input validation** on all endpoints (Jakarta Validation)
- **SQL Injection prevention** via JPA/Hibernate
- **CORS configuration** for controlled cross-origin access

### Business Logic Security
- Token escrow prevents payment fraud
- Bilateral approval prevents unilateral contracts
- Review system prevents self-reviews and duplicates
- Transaction audit trail (cannot delete transactions)
- Soft delete patterns for data recovery

---

## Email Notification System

### Bidding Notifications
- **Bid Accepted**: "Your bid has been chosen for contract #123 on project 'Mobile App Development'. Please review and accept the contract to begin work."
- **Bid Rejected**: "Thank you for your bid on 'Mobile App Development'. We have selected another provider. Feedback: 'Timeline requirements not met.' We appreciate your interest."

### Contract Notifications
- **Contract Approval Required**: "A contract has been created for your accepted bid on 'Mobile App Development'. Please review terms and accept to activate the contract."
- **Contract Activated**: "Contract #123 is now ACTIVE. Both parties have approved. Work can begin. Expected completion: 2025-04-30."
- **Contract Completed**: "Contract #123 has been successfully completed. Tokens have been transferred to provider. Please leave a review."
- **Contract Cancelled**: "Contract #123 has been cancelled. Tokens have been refunded to requester. Service request has been reopened."

### Review Notifications
- **Review Reminder**: "Contract #123 for 'Mobile App Development' is complete. Please rate your experience with [Company Name] to help build platform trust."

### Refund Notifications
- **Token Refund**: "A refund of 15,000 tokens has been processed for contract #123. Tokens have been returned to your account balance."

### Subscription Notifications
- **Subscription Activated**: "Your monthly subscription is now active. Enjoy priority search, higher support priority, and premium badge."
- **Subscription Cancelled**: "Your subscription has been cancelled. Benefits will remain active until [end date]. No partial refunds."

### Support Notifications
- **Ticket Created**: "Support ticket #456 has been created. Category: CONTRACT. Priority: HIGH. Our team will respond within 24-48 hours."
- **Ticket Resolved**: "Your support ticket #456 has been resolved. Resolution: [admin response]. Status: CLOSED."

---

## Best Practices

### For Service Requesters
1. **Write Clear Requests**
   - Specific requirements (50-500 chars)
   - Realistic timelines (start/end dates)
   - Detailed deliverables
   - Appropriate budget (check market rates)

2. **Review Bids Carefully**
   - Check company profiles (skills, ratings)
   - Read past reviews (written and received)
   - Compare proposals (price, timeline, quality)
   - Don't just choose lowest price

3. **Manage Contracts Professionally**
   - Respond promptly to provider questions
   - Review deliverables thoroughly
   - Provide constructive feedback
   - Mark complete only when satisfied

4. **Leave Honest Reviews**
   - Review after every completion
   - Be fair and constructive (min 10 chars)
   - Rate accurately (1-5 stars)
   - Help build platform trust

### For Service Providers
1. **Submit Quality Bids**
   - Showcase experience (50-500 chars)
   - Be realistic about timelines
   - Price competitively (check similar bids)
   - Highlight unique value proposition

2. **Deliver on Promises**
   - Meet agreed deadlines
   - Provide quality work
   - Communicate progress regularly
   - Address issues promptly

3. **Build Reputation**
   - Request reviews from satisfied clients
   - Respond to feedback constructively
   - Maintain high ratings (4+ stars)
   - Build long-term relationships

4. **Manage Workload**
   - Don't overcommit (track active contracts)
   - Only bid on projects you can complete
   - Update clients on progress
   - Be honest about delays

---

## Common Scenarios

### Scenario 1: First Service Request (Token-Based)
1. Login → Navigate to "Service Requests" → "Create New"
2. Choose "Token Request" (ensure sufficient balance)
3. Fill: Title (e.g., "Mobile App Development")
4. Description (50-500 chars): Requirements, features, tech stack
5. Deliverables: "iOS app, Android app, source code, documentation"
6. Dates: Start 2025-02-01, End 2025-04-30
7. Token Amount: 15000.0
8. Category: Mobile Development
9. Submit → Status: OPEN
10. Wait for bids (usually 1-7 days)
11. Review bids → Accept best → Create contract
12. Both approve → Work begins

### Scenario 2: Submitting First Bid
1. Browse requests → Filter: Mobile Development
2. Find: "Mobile App Development" (15000 tokens)
3. Read requirements carefully
4. Click "Submit Bid"
5. Description: "We specialize in React Native..." (50-500 chars)
6. Deliverables: "Complete apps, testing, support" (50-500 chars)
7. Hours: 800.0
8. Dates: 2025-02-05 to 2025-04-25
9. Exchange Type: TOKENS
10. Amount: 14500.0 (competitive pricing)
11. Submit → Status: PENDING
12. Wait for response (3-14 days)
13. If accepted → Review contract → Accept → Begin work

### Scenario 3: Contract Dispute Resolution
1. Attempt direct resolution with other party (professional communication)
2. Document all communications (emails, messages)
3. Navigate to "Support Tickets" → "Create Ticket"
4. Category: CONTRACT
5. Title: "Incomplete deliverables on mobile app contract"
6. Body: Detailed issue (10-1000 chars)
   - Contract ID: 123
   - Expected: "Responsive design, payment integration"
   - Received: "Only basic layout"
   - Request: "Admin review and resolution"
7. Submit → Priority: HIGH
8. Wait for admin review (24-48 hours)
9. Admin investigates → Reviews contract, deliverables, communications
10. Admin resolves → May process refund or mediate completion
11. Follow admin guidance

### Scenario 4: Handling Changed Requirements
1. **If contract not started (PENDING)**:
   - Contact other party immediately
   - Explain situation professionally
   - Can reject contract (tokens refunded, request reopens)

2. **If contract active (ACTIVE)**:
   - Cannot directly cancel
   - Create support ticket (Category: CONTRACT)
   - Explain changed circumstances
   - Admin reviews and decides
   - May approve cancellation with refund

3. **If work partially complete**:
   - Discuss partial payment with other party
   - Create ticket for admin mediation
   - Provide evidence of completed work
   - Admin may process partial refund

---

## Troubleshooting

### Cannot Create Service Request
- ✓ Check: Do you have COMPANY role? (not ADMIN)
- ✓ Check: All required fields filled?
- ✓ Check: Description 50-500 characters?
- ✓ Check: Date format YYYY-MM-DD?
- ✓ Check: End date after start date?
- ✓ Check: For TOKEN type, is token amount > 0?
- ✓ Check: For BARTER type, barter category selected?

### Cannot Submit Bid
- ✓ Check: Is request status OPEN? (not CLOSED/CANCELLED)
- ✓ Check: Exchange type matches request? (TOKENS/BARTER)
- ✓ Check: Start date before end date?
- ✓ Check: Estimated hours fit within timeline?
- ✓ Check: Description 50-500 characters?
- ✓ Check: For token bids, is amount > 0?

### Tokens Not Deducted from Balance
- ✓ Check: Was contract actually created? (check "My Contracts")
- ✓ Check: View "My Transactions" for confirmation
- ✓ Check: Transaction status should be PENDING (escrow)
- ✓ Wait: May take a few seconds to update
- ✓ Refresh: Browser cache may show old balance

### Cannot Accept Contract
- ✓ Check: Are you the service provider? (not requester)
- ✓ Check: Is contract status PENDING? (not ACTIVE/CANCELLED)
- ✓ Check: Has requester already accepted? (should be marked)
- ✓ Check: Is your account in good standing?
- ✓ Contact: Support if issue persists (create ticket)

### Review Not Showing on Profile
- ✓ Check: Is contract COMPLETED? (not ACTIVE/PENDING)
- ✓ Check: Was review actually submitted? (check "Written Reviews")
- ✓ Check: Rating between 1-5? Description min 10 chars?
- ✓ Wait: Reviews appear immediately but may need page refresh
- ✓ Refresh: Clear browser cache and reload page

### Subscription Not Activating
- ✓ Check: Payment processed successfully?
- ✓ Check: Sufficient balance for subscription fee?
- ✓ Check: No existing active subscription? (only one at a time)
- ✓ Wait: Activation is immediate but may take seconds
- ✓ Contact: Create SUBSCRIPTION ticket if not resolved

---

## Quick Reference

### Request Statuses
- **OPEN**: Accepting bids, can update/delete
- **CLOSED**: Bid accepted, contract creation in progress
- **CANCELLED**: Request cancelled by requester

### Bid Statuses
- **PENDING**: Awaiting requester decision, can update/delete
- **ACCEPTED**: Chosen for contract, leads to contract creation
- **REJECTED**: Not selected, provider notified via email

### Contract Statuses
- **PENDING**: Awaiting bilateral approval, tokens in escrow
- **ACTIVE**: Both approved, work in progress, can extend once
- **COMPLETED**: Work delivered, tokens transferred, reviews enabled
- **CANCELLED**: Terminated, tokens refunded, request reopens
- **DISPUTED**: Under admin review via support ticket

### Transaction Statuses
- **PENDING**: Tokens held in escrow during active contract
- **ACCEPTED**: Tokens transferred to provider (completed)
- **CANCELLED**: Tokens returned to requester (cancelled/refunded)

### Ticket Statuses
- **OPEN**: Issue reported, awaiting admin response
- **RESOLVED**: Admin responded and fixed issue
- **CLOSED**: Ticket finalized by admin

### Ticket Categories & Priorities
- **CONTRACT** → HIGH priority (disputes, deliverable issues)
- **SUBSCRIPTION** → HIGH (subscribers) / MEDIUM (non-subscribers)
- **PLATFORM** → MEDIUM (technical issues, bugs)
- **SUGGESTION** → MEDIUM (subscribers) / LOW (feature requests)

### Exchange Types
- **TOKENS**: Pay with platform currency, tokens held in escrow
- **BARTER**: Service-for-service exchange, no tokens involved
- **EITHER**: Accepts both payment methods, flexible option

---

## JUnit Tests Summary

| Test Class | Layer | Covered Repository/Service/Controller | Count | Name |
|---|---|---|---:|---|
| UserRepositoryTest | Repository | UserRepository, CompanyProfileRepository, CompanyCreditRepository | 6 | muteb |
| ServiceRequestServiceTest | Service | ServiceRequestService (with ServiceRequestRepository, CompanyProfileRepository, CategoryRepository) | 10 | hassan |
| ContractAgreementControllerTest | Controller | ContractAgreementController (with mocked ContractAgreementService) | 8 | muath |
| **Total** |  |  | **24** |  |
