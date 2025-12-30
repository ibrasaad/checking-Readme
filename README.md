# 🤝 Manfaa – B2B Service Exchange Platform  

## Overview  
**Manfaa** is a backend system that aggregates B2B service exchange opportunities in Saudi Arabia.  
It enables companies to easily find and offer professional services through two exchange mechanisms, while managing the complete lifecycle from request to delivery.  

Companies gain access to **Token-based payments or Barter exchanges** with secure escrow and bilateral contract approval.  

---

## Features  

### Company  
- Sign up / Login.  
- Create company profile (name, industry, team size, description).  
- Manage skills portfolio (assign/remove from available skills).  
- **Service Requests**:
  - Create requests (Token/Barter/Either exchange type).
  - Specify deliverables, timeline, and budget.
  - Update or delete OPEN requests.
  - Browse and filter by category, exchange type, token range, date range.
  - Sort by token amount (ascending/descending).
- **Bidding**:
  - Submit competitive bids with pricing and timeline.
  - Update or delete PENDING bids.
  - Accept or reject received bids (as requester).
  - Receive email notifications on bid decisions.
- **Contracts**:
  - Create contracts from accepted bids.
  - Bilateral approval required (both parties must accept).
  - Track status (PENDING → ACTIVE → COMPLETED).
  - Mark delivery complete with proof.
  - Extend contract time once (50% of original duration).
  - Cancel or reject contracts.
  - **Token Escrow**: Secure payment held until completion.
- **Credits**:
  - View token balance, total earned, total spent.
  - View transaction history.
  - Purchase tokens via payment gateway.
- **Reviews**:
  - Rate completed contracts (1-5 stars, decimals allowed).
  - Write review descriptions (min 10 characters).
  - View received and written reviews.
  - Update or delete own reviews.
  - Search reviews by keyword.
  - Filter by exchange type.
  - Sort by rating (best to worst).
- **Subscriptions**:
  - Subscribe monthly (120 SAR) or yearly (1,200 SAR).
  - Benefits: Priority search, higher support priority, premium badge.
  - Cancel anytime (active until period end).
- **Support Tickets**:
  - Create tickets (CONTRACT/SUBSCRIPTION/PLATFORM/SUGGESTION).
  - Auto-priority based on category and subscriber status.
  - Update or delete OPEN tickets.
  - Track resolution status.
- Email notifications for bids, contracts, reviews, refunds, and tickets.

### Admin  
- View all users.  
- Add new admins.  
- Update or delete users.  
- Delete company profiles.  
- **Categories** (10 categories):
  - Web Development, Mobile Development, Digital Marketing.
  - Graphic Design, Content Writing, Video Production.
  - Data Analysis, IT Consulting, Cloud Services, Cybersecurity.
  - Add, update, delete categories.
- **Skills** (10+ skills):
  - React.js, Node.js, Python, Java, Flutter.
  - AWS, Docker, PostgreSQL, MongoDB, Machine Learning.
  - Add, update, delete skills.
  - Search skills by keyword.
- **Monitoring**:
  - View all reviews, tickets, transactions, subscriptions.
  - Resolve tickets.
  - View all company credits.
- **Operations**:
  - Process credit refunds.
  - Add credits to companies.
  - Handle contract rejections and refunds.

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
- `POST /api/v1/contract/create` → Create a contract.  
- `POST /api/v1/contract/complete/{contractId}` → Mark delivery complete.  
- `POST /api/v1/reviews/add/{reviewedCompanyId}/{contractId}` → Add review.  
- `POST /api/v1/subscription/monthly/{companyProfileId}` → Subscribe monthly.  

### Admin  
- `GET /api/v1/user/get-all` → Get all users.  
- `DELETE /api/v1/user/delete/{userId}` → Delete a user.  
- `POST /api/v1/category/add` → Add service category.  
- `POST /api/v1/skills/add` → Add skill to library.  
- `POST /api/v1/transaction/refund/{contractId}` → Process credit refund.  

---

## Diagrams

### ER Diagram
![ER Diagram](link-to-your-er-diagram.png)

> This ER Diagram shows all main entities in Manfaa, including **Users, CompanyProfiles, CompanyCredits, ServiceRequests, ServiceBids, ContractAgreements, Reviews, CreditTransactions, Subscriptions, Tickets, Categories, and Skills**, along with their relationships.  
> It also visualizes one-to-one, one-to-many, and many-to-many relations clearly.  

### Use Case Diagram
![Use Case Diagram](link-to-your-usecase-diagram.png)

> The Use Case Diagram illustrates interactions between **Companies and Admins** with the Manfaa system.  
> It highlights key functionalities like **service requests, bidding, contract management with escrow, reviews, credit operations, and subscription handling**.  

---

### System Flow Diagrams

#### Token-Based Service Exchange Flow
```mermaid
flowchart TD
    A[Company A: Create Token Request] --> B{Validate Balance}
    B -->|Sufficient| C[Request Status: OPEN]
    B -->|Insufficient| D[Error: Insufficient Tokens]
    
    C --> E[Company B: Browse & Filter]
    E --> F[Company B: Submit Bid]
    F --> G[Bid Status: PENDING]
    
    G --> H[Company A: Review Bids]
    H --> I{Accept?}
    I -->|Yes| J[Bid: ACCEPTED]
    I -->|No| K[Bid: REJECTED]
    K --> L[Email Notification]
    
    J --> M[Request: CLOSED]
    M --> N[Company A: Create Contract]
    N --> O[Hold Tokens in Escrow]
    O --> P[Contract: PENDING]
    P --> Q[Email to Provider]
    
    Q --> R[Company B: Review Contract]
    R --> S{Accept?}
    S -->|Yes| T[Both Accepted]
    S -->|No| U[Contract: CANCELLED]
    U --> V[Release Tokens]
    V --> W[Request: OPEN]
    
    T --> X[Contract: ACTIVE]
    X --> Y[Work Begins]
    
    Y --> Z[Company B: Mark Delivered]
    Z --> AA[Company A: Review Work]
    AA --> AB{Satisfied?}
    
    AB -->|Yes| AC[Both Mark Delivered]
    AB -->|No| AD[Create Ticket]
    
    AC --> AE[Contract: COMPLETED]
    AE --> AF[Transfer Tokens]
    AF --> AG[Update Balances]
    AG --> AH[Email: Review Reminders]
    
    AH --> AI[Both Submit Reviews]
    AI --> AJ[Trust Built]
    
    style O fill:#ffeb3b
    style AF fill:#4caf50
    style V fill:#f44336
```

#### Barter Service Exchange Flow
```mermaid
flowchart TD
    A[Company A: Create Barter Request] --> B[Specify Desired Category]
    B --> C[Request: OPEN]
    
    C --> D[Company B: Find Request]
    D --> E[Submit Bid with Service Offer]
    E --> F[Bid: PENDING]
    
    F --> G[Company A: Review Bid]
    G --> H{Accept?}
    H -->|Yes| I[Bid: ACCEPTED]
    H -->|No| J[Bid: REJECTED]
    
    I --> K[Request: CLOSED]
    K --> L[Create Contract]
    L --> M[No Token Escrow]
    M --> N[Contract: PENDING]
    
    N --> O[Both Parties Review]
    O --> P{Both Accept?}
    P -->|Yes| Q[Contract: ACTIVE]
    P -->|No| R[Contract: CANCELLED]
    
    Q --> S[Work Phase]
    
    S --> T[Company B: Deliver Service]
    T --> U[Company A: Deliver Service]
    
    U --> V{Both Delivered?}
    V -->|Yes| W[Contract: COMPLETED]
    V -->|No| X[Wait]
    
    W --> Y[Both Submit Reviews]
    Y --> Z[Fair Trade Complete]
    
    style M fill:#9c27b0
    style W fill:#4caf50
```

#### Contract Lifecycle
```mermaid
stateDiagram-v2
    [*] --> PENDING: Contract Created
    
    PENDING --> ACTIVE: Both Parties Accept
    PENDING --> CANCELLED: Either Party Rejects
    
    ACTIVE --> COMPLETED: Both Mark Delivered
    ACTIVE --> CANCELLED: Contract Cancelled
    ACTIVE --> DISPUTED: Support Ticket
    
    DISPUTED --> CANCELLED: Admin Refunds
    DISPUTED --> COMPLETED: Admin Resolves
    
    COMPLETED --> [*]
    CANCELLED --> [*]
    
    note right of PENDING
        Tokens in escrow
        Awaiting approval
    end note
    
    note right of ACTIVE
        Work in progress
        Can extend once
    end note
    
    note right of COMPLETED
        Tokens transferred
        Reviews enabled
    end note
```

#### Token Escrow System
```mermaid
stateDiagram-v2
    [*] --> Requester_Balance: Initial State
    
    Requester_Balance --> Escrow: Contract Created
    note right of Escrow
        HOLD
        Transaction: PENDING
        Tokens locked
    end note
    
    Escrow --> Provider_Balance: Contract Completed
    note right of Provider_Balance
        TRANSFER
        Transaction: ACCEPTED
        Tokens moved
    end note
    
    Escrow --> Requester_Balance: Contract Cancelled
    note left of Requester_Balance
        RELEASE
        Transaction: CANCELLED
        Tokens returned
    end note
    
    Provider_Balance --> [*]
```

---

### Links

- [🎨 Figma Design](link-to-figma)
- [📬 Postman Documentation](link-to-postman)  
- [📊 Presentation (Canva)](link-to-presentation)

---

## Enhancements & Creative Improvements
- **Token Escrow System**: Secure three-state token lifecycle (HOLD → RELEASE/TRANSFER) ensures transaction integrity.  
- **Dual Exchange Types**: Flexible payment options (Tokens, Barter, or Either) for diverse B2B business needs.  
- **Bilateral Contract Approval**: Both requester and provider must approve contracts before activation.  
- **Email Automation**: Automated notifications at every step (bids, contracts, reviews, refunds).  
- **Advanced Review System**: Transparent feedback with search, filtering, and sorting capabilities.  
- **Subscription Model**: Monthly (120 SAR) and yearly (1,200 SAR) plans with priority features.  
- **Smart Ticket Prioritization**: Automatic priority assignment based on category and subscriber status.  

---

## Summary
Manfaa is designed to be a **full-featured backend solution** for B2B service exchange in Saudi Arabia.  
It balances **service requester convenience, provider opportunities, and admin control**, while integrating **secure token escrow, bilateral contract approval, and comprehensive dispute resolution**.  
With clear data modeling, automated email notifications, and robust review system, Manfaa provides a complete ecosystem for B2B service operations.  

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
| POST | `/login` | User login (returns JWT token) | muath |
| POST | `/logout` | User logout (clears JWT cookie) | muath |

---

## UserController (`/api/v1/user`)
| Method | Path | Description | Name |
|---|---|---|---|
| GET | `/get-all` | Get all users | muteb |
| POST | `/add` | Add new user/admin | muteb |
| PUT | `/update/{userId}` | Update user details | muteb |
| DELETE | `/delete/{userId}` | Delete user | muteb |

---

## CompanyProfileController (`/api/v1/company`)
| Method | Path | Description | Name |
|---|---|---|---|
| GET | `/get-all` | Get all company profiles | hassan |
| POST | `/register` | Register new company | hassan |
| PUT | `/update` | Update company profile | hassan |
| DELETE | `/delete` | Delete company profile | hassan |
| GET | `/get-companies-full` | Get all companies with full details | hassan |
| GET | `/get-company-full` | Get current company full details | hassan |
| GET | `/get-company-id-full/{companyId}` | Get company by ID with full details | hassan |

---

## CategoryController (`/api/v1/category`)
| Method | Path | Description | Name |
|---|---|---|---|
| GET | `/get` | Get all categories | muteb |
| POST | `/add` | Add category (Admin) | muteb |
| PUT | `/update/{categoryId}` | Update category (Admin) | muteb |
| DELETE | `/delete/{categoryId}` | Delete category (Admin) | muteb |

---

## SkillsController (`/api/v1/skills`)
| Method | Path | Description | Name |
|---|---|---|---|
| GET | `/get-all` | Get all skills | muteb |
| POST | `/add` | Add skill (Admin) | muteb |
| PUT | `/update/{skillsId}` | Update skill (Admin) | muteb |
| DELETE | `/delete/{skillsId}` | Delete skill (Admin) | muteb |
| POST | `/assign/{userId}/{skillId}` | Assign skill to company | muteb |
| DELETE | `/remove/{userId}/{skillId}` | Remove skill from company | muteb |
| GET | `/company/{companyId}` | Get skills by company | muteb |
| GET | `/search/{keyword}` | Search skills by keyword | muteb |

---

## CompanyCreditController (`/api/v1/credit`)
| Method | Path | Description | Name |
|---|---|---|---|
| GET | `/get-all` | Get all company credits | muteb |

---

## ServiceRequestController (`/api/v1/service-request`)
| Method | Path | Description | Name |
|---|---|---|---|
| GET | `/get-all` | Get all service requests | hassan |
| POST | `/token/{companyId}` | Create token-based request | hassan |
| POST | `/barter/{companyId}` | Create barter request | hassan |
| POST | `/either/{companyId}` | Create either-type request | hassan |
| PUT | `/update/{id}/{requestId}` | Update service request | hassan |
| DELETE | `/delete/{requestId}/{id}` | Delete service request | hassan |
| GET | `/category/{categoryId}` | Get requests by category | hassan |
| GET | `/status/{status}` | Get requests by status | hassan |
| GET | `/exchange/{exchangeType}` | Get requests by exchange type | hassan |
| GET | `/date-range` | Filter by date range | hassan |
| GET | `/token-range` | Filter by token amount | hassan |
| GET | `/sort/{order}` | Sort by token amount | hassan |
| GET | `/company/{companyId}/request-with-bids/{requestId}` | Get request with bids | hassan |

---

## ServiceBidController (`/api/v1/bid`)
| Method | Path | Description | Name |
|---|---|---|---|
| GET | `/get-all` | Get all bids | muath |
| POST | `/create/{companyId}/{requestId}` | Submit bid | muath |
| PUT | `/update/{id}/{bidId}` | Update bid | muath |
| DELETE | `/delete/{id}/{bidId}` | Delete bid | muath |
| POST | `/accept/{bidId}/{userId}` | Accept bid | muath |
| POST | `/reject/{bidId}/{userId}` | Reject bid with notes | muath |

---

## ContractAgreementController (`/api/v1/contract`)
| Method | Path | Description | Name |
|---|---|---|---|
| GET | `/get-all` | Get all contracts | muath |
| POST | `/create` | Create contract | muath |
| DELETE | `/delete/{contractId}` | Delete pending contract | muath |
| POST | `/accept/{contractId}` | Approve contract | muath |
| POST | `/reject/{contractId}` | Reject contract | muath |
| POST | `/complete/{contractId}` | Mark delivery complete | muath |

---

## ReviewController (`/api/v1/reviews`)
| Method | Path | Description | Name |
|---|---|---|---|
| GET | `/get-all` | Get all reviews (Admin) | hassan |
| GET | `/get/{reviewId}` | Get review by ID | hassan |
| POST | `/add/{reviewedCompanyId}/{contractId}` | Add review | hassan |
| PUT | `/update/{reviewId}` | Update review | hassan |
| DELETE | `/delete/{reviewId}` | Delete review | hassan |
| GET | `/company/{companyId}/received` | Get reviews received | hassan |
| GET | `/company/{companyId}/written` | Get reviews written | hassan |
| GET | `/company/{companyId}/reviewed-contracts` | Get reviewed contracts | hassan |
| GET | `/search/{keyword}` | Search reviews by keyword | hassan |
| GET | `/exchange-type/{exchangeType}` | Filter reviews by exchange type | hassan |
| GET | `/company/{companyId}/best-to-worst` | Sort reviews by rating | hassan |
| POST | `/create-pending-reviews/{contractAgreementId}` | Create pending reviews | hassan |
| POST | `/handle-rejection/{contractAgreementId}` | Handle rejection & refund | hassan |

---

## CreditTransactionController (`/api/v1/transaction`)
| Method | Path | Description | Name |
|---|---|---|---|
| GET | `/get-all` | Get all transactions (Admin) | muteb |
| GET | `/get-by-companyId/{companyId}` | Get company transactions (Admin) | muteb |
| GET | `/get-my-transactions` | Get current company transactions | muteb |
| POST | `/add-balance` | Add credit to company (Admin) | muteb |
| POST | `/refund/{contractId}` | Process credit refund (Admin) | muteb |

---

## SubscriptionController (`/api/v1/subscription`)
| Method | Path | Description | Name |
|---|---|---|---|
| GET | `/get-all` | Get all subscriptions (Admin) | hassan |
| POST | `/monthly/{companyProfileId}` | Subscribe monthly (120 SAR) | hassan |
| POST | `/yearly/{companyProfileId}` | Subscribe yearly (1,200 SAR) | hassan |
| DELETE | `/cancel/{companyId}/{subscriptionId}` | Cancel subscription | hassan |

---

## TicketController (`/api/v1/ticket`)
| Method | Path | Description | Name |
|---|---|---|---|
| GET | `/get-all/{adminId}` | Get all tickets (Admin) | muteb |
| POST | `/create/{companyId}/{contractId}` | Create support ticket | muteb |
| PUT | `/update/{ticketId}/{companyId}` | Update ticket | muteb |
| DELETE | `/delete/{ticketId}/{companyId}` | Delete ticket | muteb |

---

## JUnit Tests Summary

| Test Class | Layer | Covered Repository/Service/Controller | Count | Name |
|---|---|---|---:|---|
| UserRepositoryTest | Repository | UserRepository, CompanyProfileRepository, CompanyCreditRepository | 6 | muteb |
| ServiceRequestServiceTest | Service | ServiceRequestService (with ServiceRequestRepository, CompanyProfileRepository, CategoryRepository) | 10 | hassan |
| ContractAgreementControllerTest | Controller | ContractAgreementController (with mocked ContractAgreementService) | 8 | muath |
| **Total** |  |  | **24** |  |
