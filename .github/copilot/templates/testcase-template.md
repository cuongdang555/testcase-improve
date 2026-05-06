# Test Case Template - Standard Format

## Template Structure

```
Title: [Action verb] [Feature/Field] [Expected outcome]

Preconditions:
- [User role/permission]
- [System state]
- [Test data needed]
- [Environment setup]

Steps:
1. [First action]
2. [Second action]
3. [Verification action]

Expected Result:
- [Observable outcome]
- [State changes]
- [Messages/notifications]

Priority: [Critical | High | Medium | Low]
```

---

## Field Descriptions

### Title
- **Purpose**: One-line summary of what is tested
- **Format**: `Verb + Feature/Field + Expected Outcome`
- **Examples**:
  - ✅ "Verify user can login with valid credentials"
  - ✅ "Verify email field rejects invalid format"
  - ✅ "Verify order cannot be submitted without payment"
  - ❌ "Login test"
  - ❌ "Email validation"

### Preconditions
- **Purpose**: Setup required for test to run
- **Format**: Bullet list, specific and complete
- **Include**:
  - User role and permissions
  - System state (logged in? data exists?)
  - Test data that must exist
  - Environment configuration
  - Any time-dependent setup
- **Must NOT assume**: Make everything explicit

### Steps
- **Purpose**: Exact sequence to execute test
- **Format**: Numbered list (1, 2, 3...)
- **Rules**:
  - ONE action per step
  - Use action verbs: Click, Enter, Select, Verify, Check
  - Specific values, not variables
  - UI elements clearly identified
  - Include wait times if needed
- **Max**: 10 steps (ideally < 6)

### Expected Result
- **Purpose**: What should happen when test passes
- **Format**: Bullet list or paragraph
- **Include**:
  - Exact UI changes
  - Exact messages (copy-paste)
  - Data changes
  - System state changes
  - Any notifications
- **Must be**: Specific, measurable, observable

### Priority
- **Critical**: Must work, test first
- **High**: Important, test early
- **Medium**: Standard features, test regularly
- **Low**: Optional, test when time permits

---

## Real-World Examples

### Example 1: Simple Positive Test

```
Title: Verify user can log in with valid email and password

Preconditions:
- User is on the login page (https://example.com/login)
- User account exists with email: testuser@example.com
- Password for account: SecurePass123!
- User has not yet logged in
- Cookies are enabled in browser

Steps:
1. Click in the "Email Address" text field
2. Type "testuser@example.com"
3. Click in the "Password" text field
4. Type "SecurePass123!"
5. Click the blue "Sign In" button
6. Wait up to 5 seconds for page to load

Expected Result:
- User is successfully authenticated
- Browser redirects to dashboard page (https://example.com/dashboard)
- Welcome message displays: "Welcome, Test User"
- User avatar appears in top-right corner
- Navigation menu shows "Logout" option
- Session cookie is set with secure flag

Priority: Critical
```

### Example 2: Boundary Value Test

```
Title: Verify discount cannot exceed 100%

Preconditions:
- User is logged in with Admin role
- Product "Widget A" exists with price $100
- Discount field accepts 0-100%
- System database is accessible

Steps:
1. Navigate to Admin > Products
2. Click on "Widget A" product
3. Click "Edit Pricing" button
4. Click in the "Discount Percentage" field
5. Clear any existing value
6. Type "100.01"
7. Click "Save" button
8. Wait 2 seconds for validation

Expected Result:
- Save operation is blocked
- Error message displays in red text above the field: "Discount cannot exceed 100%"
- Field value remains "100.01" (not cleared)
- "Save" button remains enabled for retry
- Product pricing is NOT updated in database

Priority: High
```

### Example 3: Negative Test - Invalid Input

```
Title: Verify email field rejects invalid email format

Preconditions:
- User is on the registration page
- Email validation is enabled
- Browser has JavaScript enabled
- No previous registration attempts

Steps:
1. Click in the "Email Address" field
2. Type "invalid-email-without-at-sign"
3. Press Tab key to move to next field (trigger validation)
4. Wait 1 second for validation message

Expected Result:
- Email field shows validation error in real-time
- Red border appears around email field
- Error message displays below field: "Please enter a valid email address (format: name@domain.com)"
- "Create Account" button is disabled (greyed out)
- User cannot submit form

Priority: Medium
```

### Example 4: Decision Table - Multi-Condition Logic

```
Title: Verify order shipping eligibility based on order value and weight

Preconditions:
- User is on checkout page
- Shipping carriers are configured (FedEx, UPS, Local)
- Order weight limits: FedEx/UPS max 70 lbs, Local max 30 lbs
- Order value limits for free shipping: $50+

Steps:
1. Add item "Product A" (weight: 5 lbs, price: $60) to cart
2. Proceed to checkout
3. Enter shipping address
4. Select shipping method: "Standard Shipping"
5. Review order total and shipping options
6. Click "Continue to Payment"

Expected Result:
- Shipping options displayed: ✅ FedEx ($15), ✅ UPS ($12), ✅ Local ($5)
- Free shipping eligibility shows: "Free shipping! Order value over $50"
- If user selects FedEx: Order subtotal $60 + Shipping $0 = $60 total
- Shipping cost $15 is waived due to $50+ threshold
- User can proceed to payment

Priority: High
```

### Example 5: State Transition Test

```
Title: Verify order cannot transition from "Delivered" to "In Progress"

Preconditions:
- User is logged in with Admin role
- Order ID: ORD-2026-001234 exists
- Order current status: "Delivered"
- Order was delivered on 2026-05-01
- Admin notification settings enabled

Steps:
1. Navigate to Admin > Orders
2. Search for order: ORD-2026-001234
3. Click on order to open details
4. Scroll to "Order Status" section
5. Click dropdown showing "Delivered"
6. Attempt to select "In Progress" from dropdown
7. Click "Update Order Status" button

Expected Result:
- Dropdown selection is rejected or hidden
- "In Progress" option is NOT available in dropdown (disabled/hidden)
- OR if selected, error message appears: "Cannot transition from Delivered to In Progress"
- Order status remains "Delivered"
- No status change email sent to customer
- Audit log records the failed state transition attempt

Priority: High
```

### Example 6: Complex Error Scenario

```
Title: Verify file upload fails gracefully when network disconnects mid-upload

Preconditions:
- User is on the file upload page
- Test file "large-document.pdf" (15 MB) is available locally
- Maximum file size: 20 MB
- System supports resume/retry
- Network is initially stable
- Browser developer tools can simulate network issues

Steps:
1. Click "Choose File" button
2. Select "large-document.pdf" (15 MB file)
3. Click "Upload" button
4. Wait 2 seconds for upload to start (monitor progress bar)
5. Simulate network disconnection (disable network or throttle to offline)
6. Wait 5 seconds (simulating timeout)
7. Network reconnection happens (re-enable network)
8. Wait for system response

Expected Result:
- Upload progress bar shows partial progress (e.g., 30-50% complete)
- Upload stops when network disconnects
- Error message displays: "Upload interrupted. Internet connection lost."
- "Retry Upload" button becomes visible and enabled
- "Cancel Upload" button remains available
- Partial file is NOT saved to server
- User can click "Retry Upload" to resume
- If resume not supported: "Start Over" button displayed instead
- User data is not lost

Priority: Medium
```

### Example 7: Security Test

```
Title: Verify unauthorized user cannot access admin dashboard

Preconditions:
- User with "Customer" role is logged in
- Customer user account: customer@example.com
- Admin dashboard URL: https://example.com/admin
- User session is active and valid

Steps:
1. User is logged in as customer@example.com
2. Directly navigate to admin URL: https://example.com/admin
3. Wait 2 seconds for page load or redirect
4. Inspect network requests and page response
5. Check browser console for errors

Expected Result:
- Request is blocked or redirected
- User is redirected to dashboard or access denied page
- Access denied message displays: "You do not have permission to access this area"
- No admin content is visible (including CSS, JavaScript, data)
- Session remains valid (user is not logged out)
- Audit log records unauthorized access attempt
- Security event may be emailed to security team

Priority: Critical
```

---

## Template Variations

### Minimal Template (Quick Tests)
```
Title: [Brief description]
Steps: [1-3 quick steps]
Result: [Expected outcome]
Priority: [Level]
```

### Extended Template (Complex Features)
```
Title: [Detailed description]
Tags: [test type, feature area]
Preconditions: [Comprehensive setup]
Steps: [Detailed sequence]
Expected Result: [Complete outcome description]
Priority: [Level]
Notes: [Additional context]
```

### BDD Template (Behavior-Driven Development)
```
Title: [Feature name]

Given: [Initial system state / preconditions]
When: [User actions / steps]
Then: [Observable outcomes / expected results]

Priority: [Level]
```

---

## Common Mistakes to Avoid

### ❌ Mistake 1: Vague Title
```
❌ "Test login"
✅ "Verify user can log in with valid credentials"
```

### ❌ Mistake 2: Compound Steps
```
❌ Step 1: "Enter email and password, then click login"
✅ Step 1: Enter email "user@example.com"
✅ Step 2: Enter password "Test123!"
✅ Step 3: Click "Login" button
```

### ❌ Mistake 3: Unmeasurable Results
```
❌ "System works correctly"
✅ "User is redirected to dashboard; Welcome message displays: 'Welcome, John'"
```

### ❌ Mistake 4: Assumed Preconditions
```
❌ Preconditions: "User is set up"
✅ Preconditions:
   - User account exists: john@example.com
   - User has Admin role
   - User profile is complete
   - User last logged in on 2026-05-05
```

### ❌ Mistake 5: Missing Data Values
```
❌ Step 1: "Enter email"
✅ Step 1: "Enter email 'test@example.com' in the Email field"
```

---

## Checklist for Each Test Case

Before finalizing:

- [ ] Title is specific and action-oriented
- [ ] Preconditions are complete and reproducible
- [ ] Steps are numbered and atomic (one action each)
- [ ] Steps use specific values, not variables
- [ ] Expected results are measurable and specific
- [ ] Priority is assigned appropriately
- [ ] No spelling or grammar errors
- [ ] Format matches team standard
- [ ] Test can be executed manually
- [ ] Test purpose is clear to reader

---

*Template Version: 1.0*
*Last Updated: 2026-05-06*
