# Test Case Generation Guide

## Overview
This guide provides detailed instructions for generating comprehensive, high-quality test cases using ISTQB techniques.

---

## ISTQB Techniques for Test Case Generation

### 1. Equivalence Partitioning
**What**: Divide input domain into equivalence classes that should be treated similarly

**When to use**: Input validation, field processing, state handling

**Example**:
```
Feature: User Age Input
Equivalence Classes:
- Valid: 18-100
- Invalid (too young): 0-17
- Invalid (too old): 101+
- Invalid (non-numeric): "abc", null

Test Cases:
- Valid: Age = 25 → Accepted
- Too young: Age = 10 → "Must be 18+"
- Too old: Age = 150 → "Age exceeds limit"
- Non-numeric: Age = "xyz" → "Enter valid number"
```

### 2. Boundary Value Analysis
**What**: Test the edges and transitions between partitions

**When to use**: Numeric ranges, dates, time values, array sizes

**Example**:
```
Feature: Discount (Valid range: 0-100%)
Boundary Values:
- Exact boundaries: 0, 100
- Just inside: 0.01, 99.99
- Just outside: -0.01, 100.01

Test Cases:
- Discount = 0 → No discount applied
- Discount = 0.01 → $0.01 discount per item
- Discount = 100 → Free (100% discount)
- Discount = 100.01 → Error: "Invalid discount"
- Discount = -0.01 → Error: "Discount cannot be negative"
```

### 3. Decision Table Testing
**What**: Combine multiple conditions and their outcomes systematically

**When to use**: Complex business logic, multiple conditions, state combinations

**Example**:
```
Feature: Loan Approval Logic

| Credit Score | Income | Debt | Loan Approved | Reason |
|--------------|--------|------|--------------|--------|
| > 700 | > $50K | < 40% | ✅ Yes | All criteria met |
| > 700 | > $50K | ≥ 40% | ❌ No | High debt-to-income |
| > 700 | < $50K | Any | ❌ No | Insufficient income |
| < 700 | Any | Any | ❌ No | Low credit score |

→ Generates 4 test cases covering all logic branches
```

### 4. State Transition Testing
**What**: Test system behavior as it moves between states

**When to use**: Workflows, state machines, multi-step processes

**Example**:
```
Feature: Order Processing

States:
- Pending → In Progress → Shipped → Delivered
- Any state → Cancelled (valid)
- Invalid transitions (error):
  - Pending → Delivered (skip states)
  - Shipped → In Progress (go backward)

Test Cases:
1. Valid transition: Pending → In Progress → Shipped → Delivered ✅
2. Valid cancel: In Progress → Cancelled ✅
3. Invalid skip: Pending → Shipped ❌ "Must go through In Progress"
4. Invalid backward: Shipped → Pending ❌ "Cannot go backward"
```

### 5. Error Guessing
**What**: Based on experience, guess what could go wrong

**When to use**: As supplement to other techniques, real-world scenarios

**Common Error Patterns**:
- Off-by-one errors (< vs ≤)
- Null pointer exceptions
- Divide by zero
- Empty collections
- Special characters in text
- Session timeouts
- Race conditions
- Resource exhaustion

**Example**:
```
Feature: File Upload

Error scenarios:
1. Empty file → "File cannot be empty"
2. File too large (> limit) → "File exceeds 10MB limit"
3. Invalid format (.exe) → "Only images allowed"
4. Duplicate filename → "File already exists"
5. Network interruption → "Upload failed, retry?"
6. Insufficient disk space → "Insufficient storage"
7. Special characters in filename → "Invalid filename"
8. Concurrent uploads → Proper queueing
```

---

## Coverage Strategy

### Complete Coverage Checklist

```
☐ Happy Path
  - Primary success scenario
  - Standard user workflow
  Example: Valid login → Dashboard

☐ Alternative Paths
  - Secondary valid workflows
  - Optional features
  Example: Login with SSO → Dashboard

☐ Edge Cases
  - Boundary conditions
  - Extreme values
  Example: Very long password (500 chars)

☐ Negative Cases
  - Invalid inputs
  - Error conditions
  Example: Wrong password → Error message

☐ Error Handling
  - System failures
  - Graceful degradation
  Example: Network timeout → Retry prompt

☐ Security Scenarios
  - Authentication/Authorization
  - Data protection
  Example: Unauthorized user access → Denied

☐ State Transitions
  - Multi-step workflows
  - State dependencies
  Example: Draft → Review → Published

☐ Performance Scenarios
  - Load handling
  - Timeout scenarios
  Example: Slow network → Timeout handling
```

---

## Prioritization Guidelines

### Priority Levels

| Priority | Criteria | Example | Execution |
|----------|----------|---------|-----------|
| 🔴 **Critical** | Blocks core functionality, security risk, data loss risk | Login, Payment, Authentication | Must run first |
| 🟠 **High** | Major feature, affects many users | Search, Filter, Export | Run early |
| 🟡 **Medium** | Standard feature, affects some users | Sorting, UI updates, Notifications | Run regularly |
| 🟢 **Low** | Nice-to-have, cosmetic, edge case | Animations, Unused features | Run when time permits |

**Assignment Rules**:
- 1 Critical per feature (usually happy path)
- 2-4 High per feature (main alternatives, main error cases)
- 3-6 Medium per feature (edge cases, alternative flows)
- 1-3 Low per feature (cosmetic, rare scenarios)

---

## Test Case Structure Examples

### Example 1: Simple Login Feature
```
Title: Verify user can login with valid credentials

Preconditions:
- User is on the login page
- User account exists in system
- Credentials are: email=user@example.com, password=Test123!

Steps:
1. Enter email address "user@example.com" in Email field
2. Enter password "Test123!" in Password field
3. Click the "Login" button
4. Wait for page to load

Expected Result:
- User is authenticated successfully
- Browser redirects to dashboard page
- Welcome message displays: "Welcome, User"
- Session token is stored in browser

Priority: Critical
```

### Example 2: Complex Business Logic
```
Title: Verify discount is applied correctly for bulk orders

Preconditions:
- User is logged in
- Shopping cart is empty
- System discount rules:
  - 5-9 items: 5% discount
  - 10-19 items: 10% discount
  - 20+ items: 15% discount

Steps:
1. Navigate to product catalog
2. Add item "Widget A" (price: $10) to cart 15 times
3. Navigate to shopping cart
4. Verify subtotal is $150 (15 × $10)
5. Observe applied discount calculation
6. Proceed to checkout
7. Verify final price calculation

Expected Result:
- Subtotal: $150.00
- Discount (10%): -$15.00
- Final Price: $135.00
- Discount breakdown displays: "10% bulk discount applied"
- Order total matches calculation

Priority: High
```

### Example 3: Error Scenario
```
Title: Verify error message displays when uploading unsupported file type

Preconditions:
- User is on file upload page
- File "document.pdf" exists locally
- Supported formats: .jpg, .png, .gif only

Steps:
1. Click "Choose File" button
2. Select "document.pdf" from local machine
3. Click "Upload" button
4. Wait for system response

Expected Result:
- Upload is rejected
- Error message displays: "File type not supported. Please upload JPG, PNG, or GIF."
- File is not stored on server
- User can retry with different file
- Upload button remains functional

Priority: Medium
```

---

## Quick Reference: Do's and Don'ts

### ✅ DO

- ✅ Write test cases that test ONE thing
- ✅ Use clear, action-oriented language
- ✅ Include all preconditions needed to run test independently
- ✅ Make expected results measurable and specific
- ✅ Use realistic data that represents actual user scenarios
- ✅ Group related test cases logically
- ✅ Review for duplication and redundancy

### ❌ DON'T

- ❌ Write vague or ambiguous test cases
- ❌ Combine multiple test scenarios into one case
- ❌ Assume preconditions that aren't explicitly stated
- ❌ Make expected results subjective ("should work fine")
- ❌ Use dummy data that doesn't reflect real usage
- ❌ Create interdependent test cases
- ❌ Ignore edge cases and error scenarios

---

## Workflow Steps

### Step 1: Understand Requirements
- Read and analyze feature requirements
- Identify inputs, outputs, and business rules
- List constraints and assumptions

### Step 2: Identify Test Scenarios
- Brainstorm using ISTQB techniques
- Create rough test patterns (not detailed cases yet)
- Group by category (happy path, edge cases, errors)

### Step 3: Define Preconditions
- What system state is required?
- What user permissions are needed?
- What test data must exist?

### Step 4: Write Steps
- Each step is atomic (one action)
- Use imperative language (Click, Enter, Select)
- Be specific about values and elements
- Include wait times if needed

### Step 5: Define Expected Results
- What observable behavior should occur?
- Include UI changes, data changes, system state
- Be measurable and specific
- Include error messages exactly as shown

### Step 6: Assign Priority
- Critical: Core functionality, must pass
- High: Important features, should pass
- Medium: Edge cases, nice to pass
- Low: Cosmetic, optional

---

## Using Test Case Templates

See `templates/testcase-template.md` for the standard format.

For working examples, see `templates/testcase-example.md`.

---
*Last Updated: 2026-05-06*
