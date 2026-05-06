# GitHub Copilot Test Case Generator - Improved# Simple Copilot Agents Structure



## OverviewUsage:

/test-case-generator Generate test cases for login feature

This repository contains a **GitHub Copilot Agent** for generating high-quality test cases using ISTQB techniques. The agent provides a structured, multi-phase workflow that ensures comprehensive test coverage and maintains consistent quality standards.

Structure:

### ✨ Key Features.github/

  Agents/

- 🎯 **ISTQB-Based**: Uses proven testing techniques (Equivalence Partitioning, Boundary Value Analysis, Decision Tables, State Transitions, Error Guessing)  Prompts/

- ✅ **Approval Workflow**: Multi-phase process with explicit approval gates (patterns → detailed cases → CSV)  Skills/

- 📊 **Complete Coverage**: Happy paths, error scenarios, edge cases, boundary conditions  Templates/

- 📋 **CSV Export**: Ready for integration with TestRail, Jira, Azure Test Plans

- 🔍 **Quality-First**: Built-in validation and review guidanceEach agent explicitly declares which prompts and skills to use.

- 📚 **Comprehensive Documentation**: Guides, templates, examples, and checklists

---

## Quick Start

### In GitHub Copilot Chat

```
/test-case-generator Your feature description here
```

**Example**:
```
/test-case-generator Verify user can log in with valid email and password
```

### What Happens

1. **Agent asks clarifying questions** about your feature
2. **Agent generates test patterns** (high-level structure)
3. **You review and approve** patterns
4. **Agent generates detailed test cases** with examples
5. **You review and approve** test cases
6. **Agent exports CSV** ready for test management tools

### Expected Time

- Simple features: 5-10 minutes
- Moderate features: 15-20 minutes
- Complex workflows: 20-30 minutes

---

## 📚 Documentation Structure

```
.github/copilot/
├── instructions.md              ← START HERE (Central Hub)
├── agents/
│   └── test-case-generator.md   ← Agent definition
├── instructions/
│   ├── system-prompt.md         ← QA role & quality standards
│   ├── generation-guide.md      ← How to generate test cases
│   └── review-guide.md          ← How to review test cases
├── skills/
│   ├── istqb-techniques.md      ← ISTQB techniques explained
│   └── test-design-checklist.md ← Design & review checklist
├── templates/
│   └── testcase-template.md     ← Template + 7 real examples
└── chatmodes/
    └── test-generator.chatmode.md ← Chat personality & interaction
```

---

## 🎓 Learning Resources

### For QA Engineers New to ISTQB

**5-Minute Quick Start**:
1. Read: `.github/copilot/agents/test-case-generator.md` (Overview section)
2. Try: Use `/test-case-generator` with a simple feature
3. Review: Examples in `.github/copilot/templates/testcase-template.md`

**30-Minute Deep Dive**:
1. Read: `.github/copilot/instructions.md` (Central Hub)
2. Study: `.github/copilot/skills/istqb-techniques.md` (First 2 techniques)
3. Practice: Generate your first test case set

**1-Hour Comprehensive**:
1. Master all files in `.github/copilot/`
2. Generate 3-5 test case sets
3. Review peer test cases using checklist

### For Experienced QA Leads

**Quick Reference**:
- Agent definition: `.github/copilot/agents/test-case-generator.md`
- All ISTQB techniques: `.github/copilot/skills/istqb-techniques.md`
- Comprehensive checklist: `.github/copilot/skills/test-design-checklist.md`
- Review process: `.github/copilot/instructions/review-guide.md`

**Advanced Usage**:
- Combine multiple ISTQB techniques
- Customize coverage levels
- Use CSV for test management integration
- Mentor team on structured test design

---

## 📋 Usage Examples

### Example 1: Simple Feature

```
/test-case-generator Verify user can log in with valid credentials
```

**Agent generates:**
- Login happy path test
- Invalid email tests
- Invalid password tests
- Locked account tests
- Session timeout tests
- Export as CSV with all details

**CSV Output**: Ready to import to TestRail or Jira

### Example 2: Complex Feature

```
/test-case-generator E-commerce checkout including:
- Add items to cart
- Coupon code application
- Shipping address validation
- Multiple payment methods
- Order confirmation
```

**Agent generates:**
- Valid checkout flow
- Invalid shipping address tests
- Expired coupon tests
- Payment failure handling
- Concurrent order tests
- Inventory check tests

**Coverage includes**: Happy path, errors, edge cases, state transitions

### Example 3: Business Logic

```
/test-case-generator Loan approval logic:
- Credit score > 700
- Income > $50K
- Debt-to-income ratio < 40%
Requirement: Approve loan if all criteria met
```

**Agent generates:**
- Decision table with 8 combinations
- All valid and invalid scenarios
- Exact error messages
- Priority assignments

---

## 🔄 Workflow Details

### Phase 1: Test Patterns

Agent generates high-level test patterns (not detailed cases yet):

```
Happy Path
- User enters valid email
- System sends reset code
- User enters new password
- System confirms reset

Error Scenarios
- Invalid email → Error message
- Expired token → Error message
- Weak password → Error message
```

**Your Role**: Review and approve or request changes

### Phase 2: Detailed Test Cases

Agent expands patterns into full test cases:

```
Title: Verify user can reset password with valid email

Preconditions:
- User account exists: john@example.com
- Reset link expires after 24 hours

Steps:
1. Navigate to login page
2. Click "Forgot Password?"
3. Enter email: john@example.com
...

Expected Result:
- Success message displays
- User can login with new password

Priority: Critical
```

**Your Role**: Review quality and approve or request changes

### Phase 3: CSV Export

Agent exports ready-to-use CSV:

```csv
Title,Preconditions,Steps,Expected Result,Priority
"Verify user can reset password...","User account exists...","1. Navigate...","Success message displays...",Critical
...
```

**Your Role**: Use CSV in test management tool

---

## 📊 Test Case Quality Standards

### All Test Cases Must Have

- ✅ **Clear Title**: Action verb + Feature + Expected outcome
- ✅ **Complete Preconditions**: Everything needed to run test
- ✅ **Atomic Steps**: One action per step, specific values
- ✅ **Measurable Results**: Not vague, observable outcomes
- ✅ **Priority Assignment**: Critical/High/Medium/Low
- ✅ **No Duplication**: Each test focuses on one scenario

### Coverage Includes

- ✅ **Happy Path**: Normal/success scenario (1-2 tests)
- ✅ **Error Scenarios**: Invalid input, missing data, errors (5-10 tests)
- ✅ **Edge Cases**: Boundary conditions, extreme values (3-5 tests)
- ✅ **State Transitions**: Workflow steps, state changes (2-5 tests)
- ✅ **Security**: Authorization, authentication (1-3 tests)

**Target**: 15-25 test cases for typical features

---

## 🛠️ Integration with Test Management Tools

### Export Format

CSV with columns:
- `Title`: Test case name
- `Preconditions`: Setup requirements
- `Steps`: Action sequence
- `Expected Result`: Observable outcomes
- `Priority`: Critical/High/Medium/Low

### Supported Imports

- ✅ **TestRail**: Direct CSV import
- ✅ **Jira**: Copy to test plan
- ✅ **Azure Test Plans**: CSV import
- ✅ **Manual Spreadsheet**: Direct use

### Integration Steps

1. Generate test cases with `/test-case-generator`
2. Approve and export to CSV
3. Import CSV to your test tool
4. Assign test cases to team members
5. Execute tests and track results

---

## 💡 Pro Tips

1. **Be Specific**: More context = better test cases
2. **Use Examples**: Reference similar features
3. **Ask Questions**: Don't hesitate to request clarifications
4. **Review Carefully**: Quality matters more than speed
5. **Iterate**: It's okay to request refinements
6. **Learn Techniques**: Understanding ISTQB helps improve requests
7. **Share Results**: Help team learn from good test sets

---

## 🐛 Troubleshooting

### Too Many Test Cases?

Request: "Create minimal test set covering critical paths only"

### Test Cases Too Vague?

Request: "Include specific UI elements and exact error messages"

### Missing a Scenario?

During review phases, mention: "Add test for network timeout scenario"

### Need Different Format?

Request: "Export as [Markdown table / JSON / Jira format]"

---

## 📞 Support & Feedback

### Getting Help

In Copilot Chat:
- Type `/test-case-generator HELP` for commands
- Ask clarifying questions at any phase
- Request examples for specific scenarios

In Documentation:
- Check `.github/copilot/instructions.md` (Central Hub)
- See examples in `.github/copilot/templates/testcase-template.md`
- Review troubleshooting sections

### Providing Feedback

Share what works well and what can improve to help evolve the agent.

---

## 📁 File Structure

```
testcase-improve/
├── README.md                    ← This file
├── IMPROVEMENT_ANALYSIS.md      ← Migration analysis
├── .github/
│   ├── copilot-instructions.md  ← Entry point for Copilot
│   ├── Agents/                  ← Legacy folder (old structure)
│   ├── copilot/                 ← NEW: Standard GitHub Copilot
│   │   ├── instructions.md      ← Central hub (START HERE)
│   │   ├── agents/
│   │   ├── instructions/
│   │   ├── skills/
│   │   ├── templates/
│   │   └── chatmodes/
│   ├── prompts/                 ← Legacy (migrated)
│   ├── skills/                  ← Legacy (migrated)
│   ├── templates/               ← Legacy (migrated)
│   └── chatmodes/               ← Legacy (migrated)
└── test-guide.txt
```

---

## ✨ What's New

### Version 1.0 (2026-05-06)

✅ **Reorganized to GitHub Standard**
- Moved to `.github/copilot/` (official convention)
- Proper namespace organization
- Easier extension and maintenance

✅ **Enhanced Documentation**
- System prompt (120+ lines vs 5)
- Generation guide (with detailed ISTQB techniques)
- Review guide (comprehensive criteria)
- Design checklist (80+ items)

✅ **Better Templates**
- Main template (with field descriptions)
- 7 real-world examples
- Template variations for different use cases

✅ **Chat Mode Definition**
- Personality profile
- Interaction flow (6 phases)
- Response templates
- Troubleshooting guidance

✅ **Central Hub**
- `.github/copilot/instructions.md` (main reference)
- Navigation for all resources
- Learning paths
- Quick reference

---

## 🎯 Next Steps

1. **Start Using**: Try `/test-case-generator` with a simple feature
2. **Learn Techniques**: Read ISTQB techniques guide
3. **Practice**: Generate 3-5 test case sets
4. **Refine**: Apply feedback and improve
5. **Share**: Help team adopt structured test design

---

## 📝 Related Documentation

- **ISTQB**: `.github/copilot/skills/istqb-techniques.md`
- **Generation Guide**: `.github/copilot/instructions/generation-guide.md`
- **Review Guide**: `.github/copilot/instructions/review-guide.md`
- **Design Checklist**: `.github/copilot/skills/test-design-checklist.md`
- **Examples**: `.github/copilot/templates/testcase-template.md`

---

## ✅ Validation Checklist

Before finalizing test cases:

- [ ] Title is specific and action-oriented
- [ ] Preconditions are complete and reproducible
- [ ] Steps are numbered and atomic
- [ ] Expected results are measurable
- [ ] Priority is assigned appropriately
- [ ] No spelling or grammar errors
- [ ] No duplicate test cases
- [ ] Coverage includes happy path, errors, edges
- [ ] Can be executed without ambiguity
- [ ] Ready for test management tool import

---

## 📊 Success Metrics

**For You**:
- ✅ Generate test cases in 5-20 minutes
- ✅ High-quality test cases (minimal revisions)
- ✅ 80%+ coverage achieved
- ✅ Confident in test completeness

**For Team**:
- ✅ Consistent test case quality
- ✅ Faster test creation
- ✅ Fewer defects missed
- ✅ Better collaboration

---

## 🚀 Getting Started Now

### Immediate (5 minutes)

```bash
# Open GitHub Copilot Chat in VS Code
# Type:
/test-case-generator Verify user registration form validates email field
```

### Quick Learning (30 minutes)

1. Read: `.github/copilot/agents/test-case-generator.md`
2. Review: `.github/copilot/templates/testcase-template.md` (examples)
3. Try: Generate your first test case set

### Comprehensive (1-2 hours)

1. Study all files in `.github/copilot/`
2. Generate multiple test case sets
3. Review peer test cases
4. Master ISTQB techniques

---

## 📞 Questions?

Refer to:
- 📖 `.github/copilot/instructions.md` (Central Hub)
- 🎯 `.github/copilot/agents/test-case-generator.md` (Agent Details)
- 📚 `.github/copilot/skills/istqb-techniques.md` (Techniques)
- ✅ `.github/copilot/skills/test-design-checklist.md` (Checklist)

---

*Last Updated: 2026-05-06*  
*Version: 1.0*  
*Status: ✅ Ready for Use*
