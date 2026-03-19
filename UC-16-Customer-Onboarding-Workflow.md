# Use Case 16 — Customer Onboarding Workflow Automation

**Category:** Sales & CRM
**Author:** Christopher Ayodeji Ojo — [Trublshut](https://whop.com/trublshut)
**Tools:** n8n · HubSpot API · Jira / Asana API · Slack API · Gmail / Outlook · Google Calendar / Microsoft Graph

---

## 🔴 The Problem

After a deal is won, customer onboarding is chaotic — multiple teams need to be coordinated, tasks get missed, and the customer experience suffers from inconsistency and slow starts.

There is no standard process. The sales rep manually emails the delivery team. The delivery team manually emails Finance. Someone forgets to send the welcome email. The kickoff call gets scheduled a week late. The customer's first impression is disorganisation — right after they have just paid.

---

## ✅ The Solution

An automated customer onboarding workflow triggered at deal close — creating all tasks in the project management tool, notifying all teams, sending welcome communications, scheduling the kickoff call, and keeping the process on track with reminders and check-ins.

Every new client gets an identical, high-quality onboarding experience. Nothing falls through the cracks.

---

## ⚙️ How It Works

```
Deal marked "Closed Won" in HubSpot
        ↓
n8n webhook trigger fires
        ↓
Create onboarding project in Jira / Asana
with standard task list (pre-defined template):
→ Account Manager: send welcome email, schedule kickoff
→ Delivery: set up client environment, share credentials
→ Finance: set up billing, send first invoice
→ Support: create client account in support desk
        ↓
Assign tasks to correct team members by role
        ↓
Send welcome email to client
(personalised: name, company, assigned account manager, next steps)
        ↓
Post internal kickoff notification to Slack channel
(client name, deal value, AM assigned, key dates)
        ↓
Create kickoff call invite via Calendar API
(invite: client contacts + account manager)
        ↓
DAY 3: check all tasks for completion
→ Overdue tasks: send reminder to assigned team member
        ↓
DAY 7: send client check-in email
("How's everything going? Here's your account overview...")
        ↓
All tasks marked complete:
→ Update HubSpot: stage → "Active Client"
→ Post internal completion notification
```

---

## 🛠️ Tech Stack

| Tool | Role |
|------|------|
| n8n | Orchestration + webhook trigger + scheduling |
| HubSpot API | Deal trigger + contact data + stage updates |
| Jira / Asana API | Onboarding project + task creation + assignment |
| Slack API | Internal team notifications |
| Gmail / Outlook | Client welcome + check-in emails |
| Google Calendar / Microsoft Graph | Kickoff call invite creation |

---

## 🔧 Key Logic

- **Task template:** onboarding task list stored as a JSON template in n8n — each task has: title, assignee role, due date offset (e.g. "Day 1", "Day 3"), dependencies. Template updated centrally without changing the workflow
- **Role-to-person mapping:** SharePoint or Airtable lookup table maps team roles (Account Manager, Delivery Lead, Finance) to current team members — easy to update when team changes
- **Client personalisation:** welcome email and check-in populated from HubSpot contact fields (name, company, assigned AM) — not a generic template
- **Task completion check:** n8n polls Jira/Asana for task completion status on Day 3 — overdue tasks trigger reminders to the specific assignee, not the whole team
- **Escalation:** if a task is overdue by more than 2 days, escalation notification sent to the team lead
- **Calendar invite:** created with the client's primary contact (from HubSpot) + assigned account manager — invite description includes the agenda and preparation notes

---

## 📊 Outcomes

- ✅ Every new client gets an identical, high-quality onboarding experience from day one
- ✅ All internal teams notified and tasked immediately at deal close — no manual coordination
- ✅ Nothing falls through the cracks — overdue task reminders fire automatically
- ✅ Client receives a professional welcome within minutes of the deal closing
- ✅ Customer satisfaction improved through fast, consistent onboarding

---

## 📁 How to Use This

1. Define your standard onboarding task list as a JSON array in n8n (task name, role, due date offset)
2. Create a SharePoint/Airtable table mapping roles to current team members
3. In n8n, create a webhook trigger subscribed to HubSpot's "Deal Stage Changed" event — filter for stage = "Closed Won"
4. Pull deal and contact details from HubSpot API
5. Use Jira/Asana API to create a project from a template — or create individual tasks from the JSON array
6. Send client welcome email via Gmail/Outlook with personalised content
7. Post Slack notification to the onboarding channel with deal summary
8. Use Google Calendar / Microsoft Graph API to create a meeting invite with client + AM
9. Add n8n Wait nodes (Day 3, Day 7) with Jira/Asana task status checks and reminder/check-in actions

---

## 🔗 Related Use Cases

- [Use Case 13 — Automated Sales Follow-Up Sequence](./UC-13-Automated-Sales-Follow-Up-Sequence.md)
- [Use Case 15 — Proposal & Contract Generation Automation](./UC-15-Proposal-Contract-Generation.md)

---

*© 2026 Christopher Ayodeji Ojo · Trublshut AI Automation · christopherayodeji131@gmail.com*