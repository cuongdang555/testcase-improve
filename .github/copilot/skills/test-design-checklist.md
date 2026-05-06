# Test Case Design Checklist

## Overview
Use this comprehensive checklist during test case design to ensure complete, high-quality coverage.

---

## ✅ Pre-Design Phase

Before writing any test cases:

### Requirements Analysis
- [ ] Read requirement document completely
- [ ] Understand feature functionality
- [ ] Identify acceptance criteria
- [ ] List edge cases mentioned
- [ ] Note any constraints or limitations
- [ ] Identify dependencies on other features

### Stakeholder Input
- [ ] Clarify unclear requirements with team
- [ ] Understand business impact
- [ ] Identify critical paths
- [ ] Get examples from product owner
- [ ] Discuss known issues or concerns

### Test Planning
- [ ] Identify test environment requirements
- [ ] Plan test data needs
- [ ] Determine execution sequence
- [ ] Estimate test case count
- [ ] Identify test automation needs
- [ ] Plan coverage goals (80%+, 90%+, etc.)

---

## ✅ Design Phase Checklist

### Test Structure

#### Title
- [ ] Starts with action verb (Verify, Test, Validate, Check)
- [ ] Specific about what is tested
- [ ] Concise (< 80 characters)
- [ ] Not too technical
- [ ] Not too vague
- [ ] No special characters (except parentheses, hyphens)

#### Preconditions
- [ ] Clearly states system state before test
- [ ] Includes user role/permissions
- [ ] Lists all required test data
- [ ] Specifies environment configuration
- [ ] Explains any time-dependent setup
- [ ] Can be replicated independently
- [ ] Not ambiguous or assumed

#### Steps
- [ ] Each step is atomic (one action)
- [ ] Steps are numbered sequentially
- [ ] Clear action verbs used (Click, Enter, Select, Verify)
- [ ] Specific values provided (not "a value")
- [ ] Easy to follow (10 steps max, ideally < 6)
- [ ] No "and" combining multiple actions
- [ ] UI elements clearly identified
- [ ] Wait times specified if needed
- [ ] Can be executed without guessing

#### Expected Result
- [ ] Specific about what happens
- [ ] Measurable (can verify objectively)
- [ ] Not subjective ("should work")
- [ ] Includes UI changes if applicable
- [ ] Includes data changes if applicable
- [ ] Exact messages shown (copy-paste from app)
- [ ] No "and" combining multiple outcomes
- [ ] Covers all aspects of the test

#### Priority
- [ ] Assigned (Critical/High/Medium/Low)
- [ ] Appropriate for scenario type
- [ ] Aligns with business impact

---

### Happy Path Coverage

For each feature, ensure:

- [ ] ONE primary success scenario (labeled Critical)
- [ ] Covers typical user workflow
- [ ] Represents actual usage
- [ ] All main steps included
- [ ] Happy path test comes first
- [ ] Uses realistic data
- [ ] Verifies key outcomes

**Example**: E-commerce Checkout
```
✅ MUST HAVE:
Title: Verify user can complete checkout with valid payment info
- User adds item, proceeds to checkout, enters valid card, completes purchase
```

---

### Negative Test Coverage

For each field/action, ensure:

- [ ] At least ONE test for each error scenario
- [ ] Invalid input handled gracefully
- [ ] Missing required fields caught
- [ ] Wrong data type rejected
- [ ] Empty values validated
- [ ] Special characters handled
- [ ] Exact error messages verified

**Coverage Checklist**:
```
For Email Field:
□ Empty email → Error message
□ No @ symbol → Error message
□ No domain → Error message
□ Special chars → Error message
□ Very long email → Error message
□ Duplicate email (exists) → Error message

For Password Field:
□ Empty password → Error
□ Too short (< min) → Error
□ No uppercase → Error
□ No special char → Error
□ Common passwords → Error (if applicable)
```

---

### Edge Case Coverage

Identify and test:

- [ ] Boundary values (min, max, just outside)
- [ ] Empty collections (0 items)
- [ ] Maximum collections (1000+ items)
- [ ] Null/undefined values
- [ ] Special characters (!, @, #, $, %, &, *)
- [ ] Very long strings (100+ chars)
- [ ] Very short strings (1 char)
- [ ] Unicode/international characters
- [ ] Whitespace only
- [ ] Leading/trailing whitespace

**Example**: Quantity Field (Valid: 1-999)
```
□ 0 items → Error "Minimum quantity is 1"
□ 1 item → Success (lower boundary)
□ 500 items → Success (middle)
□ 999 items → Success (upper boundary)
□ 1000 items → Error "Maximum quantity is 999"
□ -1 items → Error "Quantity must be positive"
□ 999.5 items → Error "Must be whole number"
□ "abc" → Error "Must be numeric"
□ Null → Error "Quantity required"
```

---

### State Transition Coverage

For workflows, ensure:

- [ ] All valid transitions tested
- [ ] Invalid transitions prevented (or error shown)
- [ ] State changes persist
- [ ] Cannot skip intermediate states
- [ ] Cannot go backward illegally
- [ ] Concurrent transitions handled
- [ ] State conflicts resolved

**Example**: Order Processing Workflow
```
Valid Paths:
□ New → Pending → In Progress → Shipped → Delivered
□ New → Pending → Cancelled
□ In Progress → Shipped → Cancelled

Invalid Paths (should fail):
□ New → Shipped (skip Pending)
□ Shipped → Pending (go backward)
□ Delivered → In Progress (go backward)
```

---

### Decision Table Coverage

For complex logic:

- [ ] All condition combinations identified
- [ ] Decision table created (rows = combinations)
- [ ] At least one test case per combination
- [ ] Edge combinations not missed
- [ ] Redundant combinations consolidated

**Example**: Feature Eligibility
```
|Membership|Premium|Age>21|Result|
|---|---|---|---|
|Yes|Yes|Yes|✅ All benefits|
|Yes|Yes|No|⚠️ Limited benefits|
|Yes|No|Yes|✅ Standard benefits|
|Yes|No|No|⚠️ Limited benefits|
|No|Any|Yes|✅ Basic benefits|
|No|Any|No|❌ Not eligible|

→ 6 test cases minimum
```

---

### Data Validation Coverage

Ensure these validation scenarios:

- [ ] Required field validation
- [ ] Format validation (email, phone, etc.)
- [ ] Range validation (min/max values)
- [ ] Length validation (min/max chars)
- [ ] Uniqueness validation (no duplicates)
- [ ] Dependency validation (field A requires field B)
- [ ] Cross-field validation (field A + field B combo)
- [ ] Business logic validation (not just format)

**Validation Examples**:
```
Email Field:
□ Required: empty → Error
□ Format: no @ → Error
□ Format: @@ → Error
□ Uniqueness: duplicate → Error
□ Length: 254+ chars → Error

Age Field:
□ Required: empty → Error
□ Type: letters → Error
□ Range: < 0 → Error
□ Range: > 150 → Error
□ Business logic: < 18 for age-restricted feature → Error
```

---

### Authorization & Security

Include tests for:

- [ ] Unauthorized access prevented
- [ ] Role-based access enforced
- [ ] Public data visible to all
- [ ] Private data visible to owner only
- [ ] Admin-only features protected
- [ ] No privilege escalation possible
- [ ] No information disclosure
- [ ] SQL injection prevented
- [ ] XSS prevented
- [ ] CSRF tokens validated

**Example**: User Profile Edit
```
□ Owner can edit own profile
□ Owner cannot edit others' profiles
□ Admin can edit any profile
□ Anonymous user cannot edit
□ Special characters in fields don't cause errors
□ Submission doesn't reveal passwords
```

---

### Performance & Load

For systems under load:

- [ ] Normal load behavior verified
- [ ] Peak load handled gracefully
- [ ] Timeouts handled properly
- [ ] Slow network scenarios tested
- [ ] Concurrent operations handled
- [ ] Resource limits respected
- [ ] Throttling/rate limiting works

**Example**: High Load Scenarios
```
□ Single concurrent user: OK
□ 100 concurrent users: Performance acceptable
□ 1000 concurrent users: Graceful degradation
□ Network latency 5s: Timeout handling
□ Connection drops: Retry logic
```

---

### Error Handling

Ensure all errors are tested:

- [ ] User error messages are helpful
- [ ] Technical errors logged
- [ ] Error recovery possible
- [ ] No data loss on error
- [ ] Error doesn't crash system
- [ ] Error doesn't expose internals
- [ ] Retry mechanism works
- [ ] Fallback options provided

**Error Scenario Examples**:
```
□ Network timeout → "Connection timeout, retry?"
□ Invalid data → "Please fix: [specific field]"
□ Permission denied → "You don't have access"
□ Resource not found → "Item not found"
□ Server error → "Something went wrong, try again later"
□ Database error → No internal details leaked
```

---

### Completeness Check

Final validation:

- [ ] All requirements covered
- [ ] All user stories have tests
- [ ] All acceptance criteria verified
- [ ] All known issues addressed
- [ ] All bug fixes validated
- [ ] No obvious gaps in coverage
- [ ] Test count reasonable (not too few, not too many)

**Coverage Goals**:
```
Minimum: 80% - Basic happy path + main error cases
Target: 90% - Add edge cases and state transitions
Comprehensive: 95%+ - Cover everything, including rare scenarios
```

---

## ✅ Test Case Review Checklist

Before finalizing test cases:

### Content Review
- [ ] All test cases follow same format
- [ ] Terminology is consistent
- [ ] No duplicate test cases
- [ ] No contradictory test cases
- [ ] Clear relationship between related tests
- [ ] Proper grouping/organization

### Quality Review
- [ ] No spelling errors
- [ ] No grammar errors
- [ ] Formatting is consistent
- [ ] Tables render correctly
- [ ] Lists are formatted properly
- [ ] All references work

### Executability Review
- [ ] Test can be executed manually
- [ ] Test can be automated (if needed)
- [ ] All necessary test data described
- [ ] Preconditions are reproducible
- [ ] Expected results are clear
- [ ] No ambiguous instructions

### Coverage Review
- [ ] Happy path: ✅ Covered
- [ ] Error scenarios: ✅ Covered
- [ ] Edge cases: ✅ Covered
- [ ] Boundary conditions: ✅ Covered
- [ ] State transitions: ✅ Covered
- [ ] Security scenarios: ✅ Covered

---

## ✅ Priority Assignment Checklist

### Critical Priority
- [ ] Core business function (must work)
- [ ] High-risk feature
- [ ] Security-critical
- [ ] Data integrity critical
- [ ] User-facing critical path
- [ ] Priority = Critical (5-10% of tests)

### High Priority
- [ ] Important business function
- [ ] Affects multiple users
- [ ] Integration point
- [ ] Known problem area
- [ ] Priority = High (15-25% of tests)

### Medium Priority
- [ ] Standard feature
- [ ] Nice-to-have functionality
- [ ] Edge cases
- [ ] Cosmetic issues
- [ ] Priority = Medium (40-60% of tests)

### Low Priority
- [ ] Optional features
- [ ] Rarely used paths
- [ ] Nice-to-have improvements
- [ ] Future enhancements
- [ ] Priority = Low (10-20% of tests)

---

## ✅ Sign-Off Checklist

Before delivering test cases:

- [ ] All checklist items reviewed
- [ ] No outstanding issues
- [ ] Quality standards met
- [ ] Coverage goals achieved
- [ ] Stakeholder reviewed
- [ ] Ready for execution
- [ ] Ready for automation
- [ ] Documentation complete

**Sign-Off Form**:
```
Test Set: ________________
Feature: ________________
Version: ________________
Created by: ________________ Date: ________
Reviewed by: ________________ Date: ________
Approved by: ________________ Date: ________
Total Test Cases: ___
Critical: ___ | High: ___ | Medium: ___ | Low: ___
Estimated Execution Time: ___
Coverage Target: ___% | Achieved: ___%
```

---

## Quick Reference Matrix

| Aspect | ✅ Good | ❌ Bad |
|--------|---------|--------|
| **Title** | "Verify login succeeds with valid credentials" | "Test login" |
| **Steps** | 1. Click email field 2. Enter "test@example.com" | "Fill email and password, click login" |
| **Result** | "User redirected to dashboard; Welcome msg displays" | "Should work correctly" |
| **Test Count** | 20-25 for complex feature | 5 (too few) or 100+ (too many) |
| **Duplicates** | 0 duplicates | Multiple similar tests |
| **Coverage** | 80%+ of scenarios | Only happy path |
| **Priority** | Mixed distribution | All same priority |

---
*Last Updated: 2026-05-06*
