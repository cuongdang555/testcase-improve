# GitHub Copilot InstructionsWhen user input starts with "/test-case-generator":

- Read .github/Agents/test-case-generator.md

## Active Agents- Follow its instructions strictly

### Test Case Generator Agent
**Trigger**: `/test-case-generator`

When user invokes with `/test-case-generator`:
1. Load agent definition: `.github/copilot/agents/test-case-generator.md`
2. Follow the strict multi-phase workflow (patterns → approval → details → approval → CSV)
3. Load all referenced resources:
   - Instructions: `system-prompt.md`, `generation-guide.md`, `review-guide.md`
   - Skills: `istqb-techniques.md`, `test-design-checklist.md`
   - Templates: `testcase-template.md`
   - Chat mode: `test-generator.chatmode.md`
4. NEVER skip approval phases
5. Provide high-quality test cases using ISTQB techniques

**Full Documentation**: See `.github/copilot/instructions.md` (central hub)

---

## Folder Structure

```
.github/
├── copilot-instructions.md (THIS FILE)
└── copilot/                 (Main configuration)
    ├── instructions.md      (Central hub - START HERE)
    ├── agents/
    │   └── test-case-generator.md
    ├── instructions/
    │   ├── system-prompt.md
    │   ├── generation-guide.md
    │   └── review-guide.md
    ├── skills/
    │   ├── istqb-techniques.md
    │   └── test-design-checklist.md
    ├── templates/
    │   └── testcase-template.md
    └── chatmodes/
        └── test-generator.chatmode.md
```

---

## Quick Reference

- **Generate test cases**: `/test-case-generator` + your feature description
- **Learn about agents**: Read `.github/copilot/instructions.md`
- **See examples**: Check `.github/copilot/templates/testcase-template.md`
- **Understand ISTQB**: Review `.github/copilot/skills/istqb-techniques.md`

---

*Last Updated: 2026-05-06*
*For detailed information, see `.github/copilot/instructions.md`*
