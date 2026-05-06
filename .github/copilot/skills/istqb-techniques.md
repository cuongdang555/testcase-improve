# ISTQB Testing Techniques & Best Practices

## 1. Equivalence Partitioning

### Definition
Equivalence Partitioning divides the input domain into partitions (classes) where each partition is expected to behave the same way. Testing one value from each partition represents all values.

### When to Use
- Input validation (email, password, numbers)
- Field value processing
- Multi-state scenarios
- Any feature with defined valid/invalid ranges

### How to Apply

**Step 1**: Identify input ranges and states
```
Example: Age field (valid: 18-100)
States: 
  - Valid (18-100)
  - Invalid too young (0-17)
  - Invalid too old (101+)
  - Invalid non-numeric
```

**Step 2**: Define boundaries
```
Boundaries:
  - Below valid range: 0, 1, 17
  - Valid range: 18, 50, 100
  - Above valid range: 101, 999
  - Non-numeric: "abc", null
```

**Step 3**: Create test cases
```
One representative value from each partition:
1. Age = 25 (valid) → Accept
2. Age = 10 (too young) → Reject
3. Age = 150 (too old) → Reject
4. Age = "abc" (non-numeric) → Reject
```

### Example in Real Scenario

**Feature**: Credit Card Validation
```
Partition 1: Valid Cards
- 16-digit card numbers that pass Luhn algorithm
- Test: 4532-1234-5678-9010 → Accepted

Partition 2: Invalid Format
- Cards with < 16 digits or non-numeric
- Test: "1234-ABCD-5678" → "Invalid format"

Partition 3: Expired Cards
- Valid format but expiration date passed
- Test: 04/2020 on 2026 → "Card expired"

Partition 4: Insufficient Funds
- Valid card format but account has insufficient balance
- Test: $500 transaction, $100 balance → "Insufficient funds"
```

---

## 2. Boundary Value Analysis

### Definition
Boundary Value Analysis focuses on testing at the boundaries of input domains. The assumption is that the most errors occur at boundaries.

### When to Use
- Numeric ranges (prices, quantities, ages)
- Date/time values
- String lengths
- Collection sizes (min/max items)
- Timeout values

### Boundary Types

| Boundary | Definition | Example (Range: 0-100) |
|----------|-----------|--------|
| Exact Lower | Minimum valid value | 0 |
| Just Above Lower | Minimum valid + 1 unit | 1 (or 0.01) |
| Just Below Upper | Maximum valid - 1 unit | 99 (or 99.99) |
| Exact Upper | Maximum valid value | 100 |
| Just Above Upper | Maximum valid + 1 unit | 101 (or 100.01) |

### How to Apply

**Step 1**: Identify boundaries
```
Feature: Order Discount (Valid range: 0-100%)
Boundaries:
  - 0% (minimum valid)
  - 0.01% (just above minimum)
  - 99.99% (just below maximum)
  - 100% (maximum valid)
  - -0.01% (just below minimum - invalid)
  - 100.01% (just above maximum - invalid)
```

**Step 2**: Create test cases for each boundary
```
1. Discount = 0% → No discount
2. Discount = 0.01% → Apply 0.01% discount
3. Discount = 100% → Free (100% discount)
4. Discount = 99.99% → Apply 99.99% discount
5. Discount = -0.01% → Error: "Invalid discount"
6. Discount = 100.01% → Error: "Invalid discount"
```

### Example in Real Scenario

**Feature**: File Upload Size Limit (Max 10MB)
```
Boundaries:
  - 0 bytes (empty file)
  - 1 byte (minimum valid)
  - 10,485,759 bytes (just below limit = 10MB - 1)
  - 10,485,760 bytes (exactly 10MB)
  - 10,485,761 bytes (just above limit)

Test Cases:
1. Upload 0-byte file → Error: "File cannot be empty"
2. Upload 1-byte file → Success
3. Upload 9.9MB file → Success
4. Upload 10.0MB file → Success
5. Upload 10.1MB file → Error: "File exceeds 10MB limit"
```

---

## 3. Decision Table Testing

### Definition
Decision Table Testing uses tabular format to represent different combinations of conditions and their corresponding actions/outcomes.

### When to Use
- Complex business logic with multiple conditions
- Multiple independent conditions with combinations
- Feature interactions (if A and B then X, else Y)
- Regulatory or compliance rules

### How to Apply

**Step 1**: Identify conditions and actions
```
Feature: Loan Approval
Conditions:
  - Credit Score (Good: >700, Bad: ≤700)
  - Income Level (High: >$50K, Low: ≤$50K)
  - Debt-to-Income Ratio (Acceptable: <40%, High: ≥40%)

Actions:
  - Loan Status (Approved, Rejected)
  - Message (specific reason)
```

**Step 2**: Create decision table
```
| # | Credit Score | Income | Debt Ratio | Status | Reason |
|----|---|---|---|---|---|
| 1 | Good | High | Acceptable | ✅ Approved | All criteria met |
| 2 | Good | High | High | ❌ Rejected | High debt-to-income |
| 3 | Good | Low | Any | ❌ Rejected | Insufficient income |
| 4 | Bad | Any | Any | ❌ Rejected | Low credit score |
```

**Step 3**: Create test case for each row

### Example in Real Scenario

**Feature**: E-commerce Shipping Eligibility
```
| Order Value | Order Weight | Destination | Can Ship | Shipping Fee |
|---|---|---|---|---|
| >$50 | <30 lbs | Domestic | ✅ Yes | Free |
| >$50 | <30 lbs | International | ✅ Yes | $25 |
| >$50 | ≥30 lbs | Domestic | ✅ Yes | $15 |
| >$50 | ≥30 lbs | International | ❌ No | N/A |
| ≤$50 | <30 lbs | Domestic | ✅ Yes | $5 |
| ≤$50 | <30 lbs | International | ❌ No | N/A |
| ≤$50 | ≥30 lbs | Any | ❌ No | N/A |

→ 7 test cases covering all logic combinations
```

---

## 4. State Transition Testing

### Definition
State Transition Testing examines how a system moves between different states and ensures only valid transitions occur.

### When to Use
- Multi-step workflows (e.g., order processing)
- State machines (e.g., user statuses)
- Workflow engines
- Process pipelines

### How to Apply

**Step 1**: Identify all states
```
Feature: Order Processing
States:
  - New
  - Pending
  - In Progress
  - Shipped
  - Delivered
  - Cancelled
```

**Step 2**: Map valid transitions
```
New → Pending (when payment received)
Pending → In Progress (when picking/packing starts)
In Progress → Shipped (when handed to courier)
Shipped → Delivered (when customer receives)
Any state → Cancelled (if customer requests)
```

**Step 3**: Identify invalid transitions
```
Invalid:
  - New → Shipped (skip states)
  - Delivered → In Progress (go backward)
  - Shipped → Pending (go backward)
```

**Step 4**: Create test cases
```
1. Valid sequence: New → Pending → In Progress → Shipped → Delivered ✅
2. Valid cancel: In Progress → Cancelled ✅
3. Invalid skip: New → Shipped → Error "Invalid state transition" ❌
4. Invalid backward: Shipped → Pending → Error "Cannot revert state" ❌
```

### Example in Real Scenario

**Feature**: User Account Lifecycle
```
States:
  - Inactive (just created, not verified)
  - Active (verified)
  - Suspended (policy violation)
  - Deleted (user requested)

Valid Transitions:
  Inactive → Active (email verified)
  Active → Suspended (violation detected)
  Suspended → Active (suspension lifted)
  Any → Deleted (user deletes account)

Test Cases:
1. New user verifies email: Inactive → Active ✅
2. Active user violates policy: Active → Suspended ✅
3. Admin lifts suspension: Suspended → Active ✅
4. User deletes account: Active → Deleted ✅
5. Inactive user tries to login: Blocked ❌
6. Suspended user tries to post: Blocked ❌
7. Deleted user tries to reactivate: Not found ❌
```

---

## 5. Error Guessing

### Definition
Error Guessing uses experience and intuition to identify test cases for errors that might occur based on common mistakes.

### When to Use
- Supplement to other techniques
- Real-world error scenarios
- Security vulnerabilities
- Performance issues

### Common Error Patterns

#### Input Errors
- Empty/null values
- Very long strings (buffer overflow)
- Special characters (injection)
- Duplicate entries
- Wrong data type
- Whitespace-only input

#### Boundary Errors
- Off-by-one (< vs ≤)
- Integer overflow
- Division by zero
- Uninitialized variables

#### Concurrency Errors
- Race conditions
- Deadlocks
- Resource conflicts
- Order dependencies

#### Integration Errors
- Network timeouts
- Database disconnection
- API rate limiting
- Session expiration

#### Business Logic Errors
- State inconsistency
- Calculation errors
- Authorization bypass
- Data loss scenarios

### Error Guessing Examples

**Feature**: Password Reset
```
Error Scenarios:
1. Empty email field → "Email is required"
2. Non-existent email → "Email not found" (security: don't reveal)
3. User just reset → "Can only reset once per 24 hours"
4. Account suspended → "Cannot reset suspended account"
5. Old browser (no crypto) → Fallback process
6. Network timeout → "Connection lost, please retry"
7. Concurrent reset requests → Last one wins
8. Session expired → Redirect to login
9. Token link manipulated → "Invalid reset token"
10. Token expired → "Link expired, request new one"
```

**Feature**: File Upload
```
Error Scenarios:
1. No file selected → "Please select a file"
2. Empty file → "File cannot be empty"
3. File too large (>limit) → "File exceeds 10MB"
4. Unsupported format → "Only .pdf, .doc allowed"
5. Duplicate filename → "File already exists, overwrite?"
6. Virus detected (mock) → "File failed security scan"
7. Network interrupted → "Upload interrupted, retry?"
8. Disk full → "Insufficient storage space"
9. Special characters in name → "Invalid filename"
10. Very long filename (>255) → "Filename too long"
```

---

## Technique Selection Guide

| Scenario | Best Technique | Why |
|----------|---|---|
| Email validation | Equivalence Partitioning | Valid/invalid formats |
| Age range (18-100) | Boundary Value Analysis | Test limits |
| Loan approval logic | Decision Table | Multiple conditions |
| Order workflow | State Transition | Sequential states |
| File upload errors | Error Guessing | Real-world failures |
| Discount calculation | Boundary Value Analysis | Percentage limits |
| User registration | Decision Table | Multiple criteria |
| Payment processing | State Transition | Transaction states |
| Search filters | Equivalence Partitioning | Valid/invalid combos |
| API rate limiting | Error Guessing | Concurrency issues |

---

## Combining Techniques

Most complex features need MULTIPLE techniques:

**Example: E-commerce Checkout**
```
1. Equivalence Partitioning
   - Valid/invalid credit cards
   - Valid/invalid addresses
   - Valid/invalid phone numbers

2. Boundary Value Analysis
   - Order value: $0.01 - $999,999.99
   - Quantity: 1 - 1000 items
   - Coupon discount: 0% - 100%

3. Decision Table
   - Membership (Yes/No) × Coupon (Yes/No) × Express Shipping (Yes/No)
   - 8 combinations = 8 test cases

4. State Transition
   - Cart → Checkout → Payment → Confirmation
   - Invalid: Cart → Confirmation

5. Error Guessing
   - Network timeout during payment
   - Insufficient inventory
   - Payment processor down
   - Session timeout
   - Invalid coupon code
```

---

## Key Takeaways

✅ **Use these techniques to:**
- Cover all important scenarios systematically
- Find edge cases and boundary errors
- Test complex business logic thoroughly
- Identify real-world failure scenarios
- Achieve high code/requirement coverage

❌ **Avoid these mistakes:**
- Testing random cases without technique structure
- Missing boundary conditions
- Ignoring error scenarios
- Creating too many redundant tests
- Not understanding business logic before testing

---
*Last Updated: 2026-05-06*
