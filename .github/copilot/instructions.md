# GitHub Copilot Instructions - Central Hub

**Last Updated**: 2026-05-06

---

## Overview

This folder (`.github/copilot/`) contains all configuration and guidance for GitHub Copilot agents, skills, and chat modes used in this project.

### Quick Navigation

```
.github/copilot/
├── instructions.md (THIS FILE)        ← Start here
├── agents/                             ← Agent definitions
│   └── test-case-generator.md
├── instructions/                       ← Detailed guides
│   ├── system-prompt.md
│   ├── generation-guide.md
│   └── review-guide.md
├── skills/                             ← Reusable skills
│   ├── istqb-techniques.md
│   └── test-design-checklist.md
├── templates/                          ← Output templates
│   └── testcase-template.md
└── chatmodes/                          ← Chat interactions
    └── test-generator.chatmode.md
```

---

## 🎯 Available Agents

### Agent: Test Case Generator

**Purpose**: Generate high-quality test cases using ISTQB techniques

**How to Use**:
```
/test-case-generator Your feature description here
```

**What It Does**:
1. Asks clarifying questions about your feature
2. Generates test patterns (high-level structure)
3. You review and approve patterns
4. Generates detailed test cases
5. You review and approve test cases
6. Exports as CSV ready for import

**Key Features**:
- ✅ ISTQB-based systematic approach
- ✅ Multi-phase approval workflow
- ✅ Complete coverage (happy path + errors + edges)
- ✅ CSV export for test management tools
- ✅ Real examples and guidance

**Detailed Documentation**: See `agents/test-case-generator.md`

**Time Required**: 5-20 minutes depending on feature complexity

---

## 📚 Documentation Structure

### Instructions (Detailed Guides)

#### 1. `instructions/system-prompt.md`
- **Content**: QA engineer role definition
- **Includes**: Quality standards, test case format, tone and style
- **Use when**: Understanding what makes a good test case
- **Key sections**:
  - Role & expertise
  - Test case format
  - Quality standards
  - Common mistakes to avoid

#### 2. `instructions/generation-guide.md`
- **Content**: How to generate test cases using ISTQB techniques
- **Includes**: 5 techniques with examples, coverage strategy, step-by-step workflow
- **Use when**: Learning how to create comprehensive test cases
- **Key sections**:
  - ISTQB Techniques (with real examples)
  - Coverage strategy
  - Prioritization guidelines
  - Test case structure examples

#### 3. `instructions/review-guide.md`
- **Content**: How to review and validate test cases
- **Includes**: Review criteria, quality gates, common issues
- **Use when**: Evaluating test case quality
- **Key sections**:
  - Pre-review checklist
  - Detailed review criteria
  - Quality gates
  - Metrics and targets

---

### Skills (Reusable Knowledge)

#### 1. `skills/istqb-techniques.md`
- **Content**: ISTQB testing techniques explained
- **Techniques covered**:
  - ✓ Equivalence Partitioning
  - ✓ Boundary Value Analysis
  - ✓ Decision Table Testing
  - ✓ State Transition Testing
  - ✓ Error Guessing
- **Use when**: Understanding which technique to apply
- **Each technique includes**:
  - Definition
  - When to use
  - How to apply (step-by-step)
  - Real-world examples
  - Common errors

#### 2. `skills/test-design-checklist.md`
- **Content**: Comprehensive checklist for test design
- **Includes**: Pre-design, design phase, review, sign-off
- **Use when**: Ensuring complete test coverage
- **Coverage areas**:
  - Happy path coverage
  - Negative test coverage
  - Edge case coverage
  - State transition coverage
  - Decision table coverage
  - Data validation coverage

---

### Templates (Output Formats)

#### 1. `templates/testcase-template.md`
- **Content**: Standard test case format and examples
- **Includes**: Template, field descriptions, 7 real-world examples
- **Use when**: Writing or reviewing test cases
- **Examples included**:
  - Simple positive test
  - Boundary value test
  - Negative test
  - Decision table test
  - State transition test
  - Complex error scenario
  - Security test

---

### Chat Modes (Interaction Styles)

#### 1. `chatmodes/test-generator.chatmode.md`
- **Content**: Chat personality and interaction guidelines
- **Includes**: Personality profile, interaction flow, response templates
- **Use when**: Understanding how the agent communicates
- **Key sections**:
  - System personality
  - Tone & style
  - Interaction flow (6 phases)
  - Output formatting
  - Troubleshooting tips

---

## 🔄 Workflow at a Glance

### Standard Workflow

```
START: /test-case-generator
  ↓
Phase 0: Agent asks clarifying questions
  ↓
Phase 1: Agent generates test patterns
  ↓
YOU REVIEW: Approve patterns?
  ├─ NO → Agent refines patterns
  └─ YES ↓
Phase 3: Agent generates detailed test cases
  ↓
YOU REVIEW: Approve test cases?
  ├─ NO → Agent refines test cases
  └─ YES ↓
Phase 5: Agent exports CSV
  ↓
END: Use CSV in test management tool
```

### Time Investment

| Feature Type | Pattern Review | Detail Review | Total Time |
|--------------|---|---|---|
| Simple (1-2 features) | 2 min | 3 min | 5-10 min |
| Moderate (3-5 features) | 5 min | 8 min | 15-20 min |
| Complex (multi-step workflow) | 10 min | 15 min | 25-30 min |

---

## 📊 Resource Mapping

### By Use Case

**"I want to generate test cases"**
1. Start with: `agents/test-case-generator.md`
2. Reference: `instructions/generation-guide.md`
3. Use template: `templates/testcase-template.md`

**"I want to understand ISTQB techniques"**
1. Read: `skills/istqb-techniques.md`
2. Apply to: `instructions/generation-guide.md`
3. Validate with: `skills/test-design-checklist.md`

**"I want to review test cases"**
1. Use: `skills/test-design-checklist.md`
2. Follow: `instructions/review-guide.md`
3. Reference template: `templates/testcase-template.md`

**"I want to understand how the agent works"**
1. Read: `agents/test-case-generator.md`
2. See interaction style: `chatmodes/test-generator.chatmode.md`
3. Understand standards: `instructions/system-prompt.md`

---

## 🎓 Learning Path

### For QA Engineers New to ISTQB

**Step 1**: Understand the basics (30 min)
- [ ] Read: `skills/istqb-techniques.md` (first 2 techniques)
- [ ] Read: `instructions/system-prompt.md` (Quality Standards section)

**Step 2**: Learn by example (30 min)
- [ ] Review examples in: `templates/testcase-template.md`
- [ ] Try: Generate simple test cases with `/test-case-generator`

**Step 3**: Master the workflow (30 min)
- [ ] Read: `instructions/generation-guide.md`
- [ ] Understand: `instructions/review-guide.md`

**Step 4**: Become proficient (1-2 hours)
- [ ] Generate 3-5 test case sets
- [ ] Review peer's test cases
- [ ] Use checklist from: `skills/test-design-checklist.md`

### For Experienced QA Leads

**Quick Reference**:
- Agent capabilities: `agents/test-case-generator.md`
- Advanced techniques: `skills/istqb-techniques.md` (all 5 techniques)
- Comprehensive checklist: `skills/test-design-checklist.md`
- Review process: `instructions/review-guide.md`

**Advanced Usage**:
- Combine multiple ISTQB techniques
- Customize coverage for your product
- Use CSV output for test management integration
- Mentor team on structured test design

---

## 🔧 Configuration & Customization

### Default Behaviors

- **Default Mode**: Pattern approval before detailed cases
- **Default Output**: CSV format
- **Default Coverage**: 80% minimum coverage
- **Default Priority Mix**: 10% Critical, 20% High, 50% Medium, 20% Low

### Customization Options

**Reduce Approval Steps** (if needed):
- Mention in initial request: "Skip pattern review"
- Agent will go directly to detailed cases

**Change Output Format**:
- Ask for: "CSV", "Markdown table", "JSON", "Jira format"
- Agent will adapt output

**Adjust Coverage Level**:
- Request: "Quick test set (minimal coverage)" or "Comprehensive (high coverage)"
- Agent will adjust test count and scope

---

## 🐛 Troubleshooting

### Issue: Test cases are too many/too few
**Solution**: Specify in initial request
- Too many: "Create minimal test set covering critical paths"
- Too few: "Create comprehensive test set including edge cases"

### Issue: Test cases are too vague
**Solution**: Provide more context
- "Include specific API endpoints" or "Focus on UI-level interactions"

### Issue: Missing a specific scenario
**Solution**: Request during review phases
- Phase 2: "Add test for network timeout"
- Agent will refine patterns

### Issue: Want different priority distribution
**Solution**: Adjust before final export
- "Make 50% of tests Critical/High priority"
- Agent will redistribute

---

## 📞 Support & Feedback

### Getting Help

**In Agent Chat**:
- Type `/test-case-generator HELP` for command reference
- Ask clarifying questions at any phase
- Request examples: "Show me an example of [scenario]"

**In Documentation**:
- Check troubleshooting sections in each guide
- See examples in `templates/testcase-template.md`

### Providing Feedback

**To improve this agent**:
1. Document what worked well
2. Note any improvements needed
3. Share with QA team lead
4. Updates will be reflected here

---

## 📈 Best Practices

### ✅ DO

- ✅ Provide clear feature descriptions
- ✅ Review and approve each phase carefully
- ✅ Use ISTQB techniques from the skills section
- ✅ Follow the template format consistently
- ✅ Validate coverage before export
- ✅ Use CSV output for integration

### ❌ DON'T

- ❌ Skip approval phases
- ❌ Accept vague test cases
- ❌ Create 100+ tests without filtering
- ❌ Use dummy data in production test cases
- ❌ Ignore review guidance
- ❌ Force all tests to same priority

---

## 📋 File Inventory

| File | Purpose | Maintenance |
|------|---------|-------------|
| `agents/test-case-generator.md` | Agent definition | Update with new features |
| `instructions/system-prompt.md` | QA role standards | Review quarterly |
| `instructions/generation-guide.md` | How to generate | Update with new techniques |
| `instructions/review-guide.md` | How to review | Update with lessons learned |
| `skills/istqb-techniques.md` | ISTQB techniques | Reference material, rarely changes |
| `skills/test-design-checklist.md` | Design checklist | Review quarterly |
| `templates/testcase-template.md` | Test case format | Update with new examples |
| `chatmodes/test-generator.chatmode.md` | Chat personality | Update as interactions evolve |

---

## 🚀 Quick Start

### Immediate Usage (5 minutes)

1. Open GitHub Copilot Chat
2. Type: `/test-case-generator` + your feature description
3. Follow agent's questions
4. Approve patterns and test cases
5. Get CSV export

### Learn More (30 minutes)

1. Read: `agents/test-case-generator.md`
2. Review: Examples in `templates/testcase-template.md`
3. Understand: `instructions/generation-guide.md`

### Become Expert (1-2 hours)

1. Master: All files in this folder
2. Practice: Generate 5+ test case sets
3. Review: Others' test cases using checklist
4. Help: Mentor team members

---

## 📝 Version & Updates

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-05-06 | Initial release - Test Case Generator Agent |

### Planned Enhancements

- [ ] Additional agents (Test Execution, Defect Logging)
- [ ] Integration with TestRail/Jira
- [ ] Performance testing techniques
- [ ] API/Backend test patterns
- [ ] Mobile-specific test patterns

---

## 🎯 Success Metrics

### For Individual Users
- ✅ Can generate test cases using `/test-case-generator`
- ✅ Test cases are clear and actionable
- ✅ Coverage is >80%
- ✅ Minimal revision needed after generation

### For QA Teams
- ✅ Consistent test case quality across team
- ✅ Reduced time to create test cases
- ✅ Fewer defects missed in testing
- ✅ Better test organization and tracking

### For Project
- ✅ Higher code coverage through comprehensive testing
- ✅ Faster defect detection
- ✅ Reduced post-release issues
- ✅ Better collaboration on test design

---

## 💡 Pro Tips

1. **Be Specific**: The more detail you provide, the better the test cases
2. **Use Examples**: Reference similar features when describing your feature
3. **Ask Questions**: Don't hesitate to ask agent to clarify or refine
4. **Review Carefully**: Take time to review patterns and test cases before approval
5. **Iterate**: It's okay to request changes - quality matters more than speed
6. **Learn Techniques**: Understanding ISTQB techniques will improve your requests
7. **Share Results**: Help team learn from good test case sets
8. **Provide Feedback**: Let us know what works and what can improve

---

## 🔗 Related Resources

**External References**:
- ISTQB Foundation Level Syllabus
- Testing Best Practices (Your Organization)
- Test Management Tools (TestRail, Jira, Azure Test Plans)
- CI/CD Integration Guides

**Internal References**:
- Project requirements and user stories
- Existing test cases for similar features
- Known issues and bug reports
- Team's testing standards

---

*This is the central hub for all GitHub Copilot testing agents and guidance.*  
*For questions or suggestions, contact your QA team lead or documentation owner.*

