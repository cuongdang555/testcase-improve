# Quick Reference Guide - Test Case Generator

## 🚀 Quick Start (2 minutes)

### In GitHub Copilot Chat, type:

```
/test-case-generator Verify user can log in with valid email and password
```

That's it! Agent will guide you through the rest.

---

## 📖 Documentation Roadmap

### Find What You Need

| I want to... | Read this | Location |
|---|---|---|
| Start using the agent | README.md | Root folder |
| Understand how it works | Central Hub | `.github/copilot/instructions.md` |
| Learn about the agent | Agent Definition | `.github/copilot/agents/test-case-generator.md` |
| Understand ISTQB techniques | Skills | `.github/copilot/skills/istqb-techniques.md` |
| See real examples | Templates | `.github/copilot/templates/testcase-template.md` |
| Review test cases | Checklist | `.github/copilot/skills/test-design-checklist.md` |
| Understand generation process | Generation Guide | `.github/copilot/instructions/generation-guide.md` |
| Learn review process | Review Guide | `.github/copilot/instructions/review-guide.md` |
| Know quality standards | System Prompt | `.github/copilot/instructions/system-prompt.md` |
| Understand chat interaction | Chatmode | `.github/copilot/chatmodes/test-generator.chatmode.md` |

---

## 🎯 Workflow at a Glance

```
Phase 0: Clarify Requirements
  ↓
Phase 1: Generate Test Patterns
  ↓
YOU APPROVE (or request changes)
  ↓
Phase 3: Generate Detailed Test Cases
  ↓
YOU APPROVE (or request changes)
  ↓
Phase 5: Export as CSV
  ↓
IMPORT TO TEST TOOL
```

**Time: 5-20 minutes total**

---

## 💡 Tips for Better Results

1. **Be Specific**: Describe feature clearly with examples
2. **Ask Questions**: Don't hesitate to clarify
3. **Review Carefully**: Don't rush approval
4. **Request Changes**: Iterate until perfect
5. **Learn Techniques**: Understand ISTQB (see istqb-techniques.md)

---

## 📊 Expected Output

### Phase 1: Test Patterns (5-10 patterns)
```
✓ Happy Path
✓ Error: Invalid email
✓ Error: Expired token
✓ Edge case: Very long email
```

### Phase 3: Detailed Test Cases (15-25 cases)
```
Title: Verify user can reset password with valid email
Preconditions: User account exists, email valid
Steps: 
  1. Navigate to login page
  2. Click "Forgot Password?"
  3. Enter email address
  4. Click "Send Link"
Expected Result: Email sent, confirmation message displays
Priority: Critical
```

### Phase 5: CSV Export
Ready to import to TestRail, Jira, Azure Test Plans

---

## 🔑 Key Commands

```
/test-case-generator HELP              Show available commands
/test-case-generator [description]     Start generation
```

**During interaction**:
- `APPROVE` → Move to next phase
- `Add [scenario]` → Include new test
- `Remove [test]` → Exclude test
- Questions → Ask for clarification

---

## ✅ Quality Checklist

Before approving test cases:

- [ ] Title is clear and specific?
- [ ] Preconditions are complete?
- [ ] Steps are numbered and atomic?
- [ ] Expected results are measurable?
- [ ] Priority is appropriate?
- [ ] No duplicate tests?
- [ ] Coverage is complete (happy path + errors + edges)?

---

## 🎓 ISTQB Techniques (5 types)

1. **Equivalence Partitioning**: Valid/invalid input groups
2. **Boundary Value Analysis**: Test limits and boundaries
3. **Decision Table**: Multiple condition combinations
4. **State Transition**: Workflow transitions
5. **Error Guessing**: Real-world failure scenarios

See: `.github/copilot/skills/istqb-techniques.md` for details

---

## 📚 Resources by Skill Level

### Beginner
- Start: `README.md`
- Learn: `templates/testcase-template.md` (examples)
- Try: `/test-case-generator` with simple feature

### Intermediate
- Master: `instructions/generation-guide.md`
- Practice: Generate 3-5 test sets
- Review: Peer test cases using checklist

### Advanced
- Deep Dive: All ISTQB techniques in `skills/istqb-techniques.md`
- Master: `skills/test-design-checklist.md` (all 100+ items)
- Leadership: Mentor team on best practices

---

## 🛠️ Integration with Test Tools

### Export Steps

1. Generate test cases
2. Approve final version
3. Request CSV export
4. Copy CSV data
5. Import to your test tool:
   - TestRail: Tools → Import → CSV
   - Jira: Create Test Plan → Import from CSV
   - Azure: Test Plans → New → Import CSV

---

## 📞 Common Questions

**Q: How long does it take?**  
A: 5-20 minutes depending on feature complexity

**Q: Do I need to know ISTQB?**  
A: No, agent guides you. But learning helps (see skills files)

**Q: Can I modify test cases after export?**  
A: Yes, all tools allow editing

**Q: What if I want more/fewer test cases?**  
A: Tell agent during approval phases

**Q: Can I use this for API testing?**  
A: Yes, describe API endpoints in request

**Q: Is there a limit to test cases?**  
A: No, but recommend 15-25 per feature

---

## 🚀 Getting Started Now

### Right Now (5 min)
1. Open Copilot Chat in VS Code
2. Type: `/test-case-generator` + simple feature
3. Follow agent's questions
4. Approve patterns
5. Approve test cases
6. Get CSV export

### Today (30 min)
1. Read: `README.md` and `Central Hub`
2. Review: Examples in `templates/testcase-template.md`
3. Generate: 1-2 test case sets
4. Understand: How it works

### This Week (1-2 hours)
1. Study: ISTQB techniques
2. Generate: 5+ test case sets
3. Review: Peer's test cases
4. Become: Proficient with agent

---

## 📋 File Inventory

```
.github/copilot/
├── instructions.md                    ← Central Hub (START HERE)
├── agents/
│   └── test-case-generator.md        ← Agent definition
├── instructions/
│   ├── system-prompt.md              ← QA role & standards
│   ├── generation-guide.md           ← How to generate
│   └── review-guide.md               ← How to review
├── skills/
│   ├── istqb-techniques.md           ← 5 ISTQB techniques
│   └── test-design-checklist.md      ← 100+ checklist items
├── templates/
│   └── testcase-template.md          ← Template + 7 examples
└── chatmodes/
    └── test-generator.chatmode.md    ← Chat personality
```

---

## ✨ What Makes This Special

✅ **ISTQB-Based**: Systematic, proven methodology  
✅ **Approval Workflow**: Multi-phase quality gates  
✅ **Complete Coverage**: Happy path + errors + edges  
✅ **CSV Export**: Ready for test tools  
✅ **Well-Documented**: 3000+ lines of guidance  
✅ **Real Examples**: 10+ detailed scenarios  
✅ **Learning Paths**: 3 structured paths  
✅ **No Skipping**: Quality-first approach  

---

## 🎯 Success Metrics

You'll know it's working when:
- ✅ You generate test cases in 5-20 minutes
- ✅ Test cases are clear and specific
- ✅ Coverage is 80%+ complete
- ✅ Minimal revisions needed
- ✅ Tests are ready to import

---

## 📝 Version & Updates

- **Version**: 1.0
- **Release Date**: 2026-05-06
- **Status**: ✅ Ready for Production

---

*For detailed information, see `.github/copilot/instructions.md`*
