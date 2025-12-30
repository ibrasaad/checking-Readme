# 🤝 Manfaa – B2B Service Marketplace Platform  

## Overview  
**Manfaa** is a backend system that aggregates B2B service exchange opportunities in Saudi Arabia.  
It enables companies to easily find and offer professional services through two exchange mechanisms, while managing the complete lifecycle from request to delivery.  

Companies gain access to **Token-based payments or Barter exchanges** with secure escrow and contract management.  

---

## Features  

### Company  
- Sign up / Login.  
- Create company profile (name, industry, team size, description).  
- Manage company skills portfolio.  
- **Service Requests**:
  - Create requests (Token/Barter/Either exchange type).
  - Specify deliverables, timeline, and budget.
  - Update or delete open requests.
  - Browse and search available requests.
  - Filter by category, status, exchange type, date range, token amount.
  - Sort by token amount (ascending/descending).
- **Bidding**:
  - Submit competitive bids with pricing and timeline.
  - Update or delete pending bids.
  - View all submitted bids.
  - Accept or reject received bids (as requester).
- **Contracts**:
  - Create contracts from accepted bids.
  - Approve contracts (bilateral approval required).
  - Track contract status (PENDING → ACTIVE → COMPLETED).
  - Mark delivery complete.
  - Extend contract time (once, 50% duration).
  - Cancel active contracts.
  - Delete pending contracts.
- **Credits**:
  - View token balance, total earned, total spent.
  - View transaction history (incoming and outgoing).
  - Secure token escrow for payments.
- **Reviews**:
  - Rate completed contracts (1-5 stars).
  - Write detailed review descriptions.
  - View received reviews (reputation).
  - View written reviews.
  - Update or delete own reviews.
- **Subscriptions**:
  - Subscribe monthly or yearly.
  - View subscription status.
  - Cancel active subscriptions.
- **Support**:
  - Create support tickets for contract issues.
  - Update ticket details.
  - Delete open tickets.
  - Track ticket status and resolution.
- Receive email notifications for:
  - Bid acceptance/rejection.
  - Contract approvals and completions.
  - Review reminders.
  - Refund confirmations.

### Admin  
- View all users.  
- Add new admins.  
- Update user details.  
- Delete users.  
- Delete company profiles.  
- **Categories**:
  - Add service categories.
  - Update category details.
  - Delete categories.
  - View all categories.
- **Skills**:
  - Add skills to library.
  - Update skill details.
  - Delete skills.
  - View all skills.
- **Monitoring**:
  - View all reviews.
  - View all support tickets.
  - Resolve support tickets.
  - View all transactions.
  - View all subscriptions.
- **Operations**:
  - Process credit refunds.
  - Add credits to companies.
  - Access system-wide reports.

---

## Tech Stack  
- **Backend:** Spring Boot 3, Spring Security, Hibernate/JPA  
- **Database:** MySQL  
- **Email Service:** JavaMailSender (SMTP)  
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
- `GET /api/v1/service-request/all` → Get all service requests.  
- `POST /api/v1/service-request/token/{companyId}` → Create token-based request.  
- `POST /api/v1/bid/{companyId}/{requestId}` → Submit a bid.  
- `PUT /api/v1/bid/accept/{bidId}/{userId}` → Accept a bid.  
- `POST /api/v1/contract/{userId}` → Create a contract.  
- `PUT /api/v1/contract/complete/{contractId}/{userId}` → Mark delivery complete.  
- `POST /api/v1/review/{reviewerCompanyId}/{reviewedCompanyId}/{contractId}` → Add review.  
- `POST /api/v1/subscription/monthly/{companyProfileId}` → Subscribe monthly.  

### Admin  
- `GET /api/v1/user/all` → Get all users.  
- `DELETE /api/v1/user/delete/{userId}` → Delete a user.  
- `POST /api/v1/category/add/{userId}` → Add service category.  
- `POST /api/v1/skills/add` → Add skill to library.  
- `POST /api/v1/credit/refund/{contractId}` → Process credit refund.  

---

## Diagrams

### ER Diagram
![ER Diagram](link-to-your-er-diagram.png)

> This ER Diagram shows all main entities in Manfaa, including **Users, CompanyProfiles, CompanyCredits, ServiceRequests, ServiceBids, ContractAgreements, Reviews, CreditTransactions, Subscriptions, Tickets, Categories, and Skills**, along with their relationships.  
> It also visualizes one-to-one, one-to-many, and many-to-many relations clearly.  

### Use Case Diagram
![Use Case Diagram](link-to-your-usecase-diagram.png)

> The Use Case Diagram illustrates interactions between **Companies and Admins** with the Manfaa system.  
> It highlights key functionalities like **service requests, bidding, contract management, reviews, credit operations, and subscription handling**.  

---

### Links

- [🎨 Figma Design](link-to-figma)
- [📬 Postman Documentation](link-to-postman)  
- [📊 Presentation (Canva)](link-to-presentation)

---

## Enhancements & Creative Improvements
- **Token Escrow System**: Secure three-state token lifecycle (hold → release/transfer) ensures transaction integrity.  
- **Dual Exchange Types**: Flexible payment options (Tokens, Barter, or Either) for diverse business needs.  
- **Bilateral Approval**: Both parties must approve contracts before activation for trust and transparency.  
- **Email Automation**: Automated notifications for bids, contracts, reviews, and refunds keep parties informed.  
- **Review System**: Transparent feedback mechanism with ratings to build company reputation.  
- **Subscription Model**: Monthly and yearly plans for premium platform features.  

---

## Summary
Manfaa is designed to be a **full-featured backend solution** for B2B service exchange in Saudi Arabia.  
It balances **service requester convenience, provider opportunities, and admin control**, while integrating **secure token escrow and bilateral contract approval**.  
With clear data modeling, automated email notifications, and comprehensive dispute resolution, Manfaa provides a complete ecosystem for B2B service operations.  

---

# API Endpoints Summary

| Controller | Count |
|---|---:|
| AuthController | 2 |
| UserController | 4 |
| CompanyProfileController | 5 |
| CategoryController | 4 |
| SkillsController | 6 |
| ServiceRequestController | 11 |
| ServiceBidController | 6 |
| ContractAgreementController | 8 |
| ReviewController | 7 |
| CreditTransactionController | 4 |
| SubscriptionController | 4 |
| TicketController | 4 |
| **Total** | **65** |

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
| GET | `/all` | Get all users | muteb |
| POST | `/add/{userId}` | Add new user/admin | muteb |
| PUT | `/update/{userId}` | Update user details | muteb |
| DELETE | `/delete/{userId}` | Delete user | muteb |

---

## CompanyProfileController (`/api/v1/company`)
| Method | Path | Description | Name |
|---|---|---|---|
| POST | `/register` | Register new company | hassan |
| GET | `/all` | Get all company profiles | hassan |
| GET | `/{id}` | Get company full details | hassan |
| PUT | `/update/{companyProfileId}` | Update company profile | hassan |
| DELETE | `/delete/{companyProfileId}` | Delete company profile | hassan |

---

## CategoryController (`/api/v1/category`)
| Method | Path | Description | Name |
|---|---|---|---|
| GET | `/all` | Get all categories | muteb |
| POST | `/add/{userId}` | Add category | muteb |
| PUT | `/update/{userId}/{categoryId}` | Update category | muteb |
| DELETE | `/delete/{userId}/{categoryId}` | Delete category | muteb |

---

## SkillsController (`/api/v1/skills`)
| Method | Path | Description | Name |
|---|---|---|---|
| GET | `/all` | Get all skills | muteb |
| POST | `/add` | Add skill | muteb |
| PUT | `/update/{skillsId}` | Update skill | muteb |
| DELETE | `/delete/{skillsId}` | Delete skill | muteb |
| POST | `/assign/{userId}/{skillId}` | Assign skill to company | muteb |
| DELETE | `/remove/{userId}/{skillId}` | Remove skill from company | muteb |

---

## ServiceRequestController (`/api/v1/service-request`)
| Method | Path | Description | Name |
|---|---|---|---|
| GET | `/all` | Get all service requests | hassan |
| POST | `/token/{companyId}` | Create token-based request | hassan |
| POST | `/barter/{companyId}` | Create barter request | hassan |
| POST | `/either/{companyId}` | Create either-type request | hassan |
| PUT | `/update/{id}/{requestId}` | Update service request | hassan |
| DELETE | `/delete/{requestId}/{id}` | Delete service request | hassan |
| GET | `/category/{categoryId}` | Get requests by category | hassan |
| GET | `/status/{status}` | Get requests by status | hassan |
| GET | `/exchange/{exchangeType}` | Get requests by exchange type | hassan |
| GET | `/dateRange?start={date}&end={date}` | Filter by date range | hassan |
| GET | `/tokenRange?min={amount}&max={amount}` | Filter by token amount | hassan |

---

## ServiceBidController (`/api/v1/bid`)
| Method | Path | Description | Name |
|---|---|---|---|
| GET | `/all` | Get all bids | muath |
| POST | `/{companyId}/{requestId}` | Create service bid | muath |
| PUT | `/update/{id}/{bidId}` | Update bid | muath |
| DELETE | `/delete/{id}/{bidId}` | Delete bid | muath |
| PUT | `/accept/{bidId}/{userId}` | Accept bid (Requester) | muath |
| PUT | `/reject/{bidId}/{userId}` | Reject bid with notes (Requester) | muath |

---

## ContractAgreementController (`/api/v1/contract`)
| Method | Path | Description | Name |
|---|---|---|---|
| GET | `/all` | Get all contracts | muath |
| POST | `/{userId}` | Create contract from accepted bid | muath |
| DELETE | `/{id}/{contractId}` | Delete pending contract | muath |
| PUT | `/accept/{userId}/{contractId}` | Approve contract | muath |
| PUT | `/reject/{userId}/{contractId}` | Reject contract | muath |
| PUT | `/complete/{contractId}/{userId}` | Mark delivery complete | muath |
| PUT | `/cancel/{contractId}/{userId}` | Cancel contract | muath |
| PUT | `/extend/{contractId}/{userId}` | Extend contract time | muath |

---

## ReviewController (`/api/v1/review`)
| Method | Path | Description | Name |
|---|---|---|---|
| GET | `/all/{adminId}` | Get all reviews (Admin) | hassan |
| GET | `/{reviewId}/{companyId}` | Get review by ID | hassan |
| POST | `/{reviewerCompanyId}/{reviewedCompanyId}/{contractId}` | Add review | hassan |
| PUT | `/{userId}/{reviewId}` | Update review | hassan |
| DELETE | `/{userId}/{reviewId}` | Delete review | hassan |
| GET | `/received/{companyId}` | Get reviews received by company | hassan |
| GET | `/written/{companyId}` | Get reviews written by company | hassan |

---

## CreditTransactionController (`/api/v1/credit`)
| Method | Path | Description | Name |
|---|---|---|---|
| GET | `/all` | Get all transactions (Admin) | muteb |
| GET | `/transactions/{companyId}` | Get company transactions | muteb |
| POST | `/refund/{contractId}` | Process credit refund (Admin) | muteb |
| POST | `/add/{userId}/{amount}` | Add credit to company (Admin) | muteb |

---

## SubscriptionController (`/api/v1/subscription`)
| Method | Path | Description | Name |
|---|---|---|---|
| GET | `/all` | Get all subscriptions (Admin) | hassan |
| POST | `/monthly/{companyProfileId}` | Subscribe monthly | hassan |
| POST | `/yearly/{companyProfileId}` | Subscribe yearly | hassan |
| DELETE | `/cancel/{companyId}/{subscriptionId}` | Cancel subscription | hassan |

---

## TicketController (`/api/v1/ticket`)
| Method | Path | Description | Name |
|---|---|---|---|
| GET | `/all/{adminId}` | Get all tickets (Admin) | muteb |
| POST | `/{companyId}/{contractId}` | Create support ticket | muteb |
| PUT | `/{ticketId}/{companyId}` | Update ticket | muteb |
| DELETE | `/{ticketId}/{companyId}` | Delete ticket | muteb |

---

## JUnit Tests Summary

| Test Class | Layer | Covered Repository/Service/Controller | Count | Name |
|---|---|---|---:|---|
| UserRepositoryTest | Repository | UserRepository, CompanyProfileRepository, CompanyCreditRepository | 6 | muteb |
| ServiceRequestServiceTest | Service | ServiceRequestService (with ServiceRequestRepository, CompanyProfileRepository, CategoryRepository) | 10 | hassan |
| ContractAgreementControllerTest | Controller | ContractAgreementController (with mocked ContractAgreementService) | 8 | muath |
| **Total** |  |  | **24** |  |
