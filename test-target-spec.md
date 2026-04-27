# AI Email Assistant — Product Spec v1.2

**Project:** "Sage" — AI assistant inside Lumin Mail (B2B email client, EU + US customers, Berlin HQ)
**Target launch:** July 2026
**Author:** Product team
**Status:** Engineering review pending

---

## What we're building

Sage is an AI-powered assistant embedded directly inside the Lumin Mail interface. It can read user emails, draft replies, summarize threads, and (with permission) send replies on the user's behalf. The goal is to reduce time spent in inbox by 40%.

## User flow

### 1. Onboarding

When users sign up for Lumin Mail, they're greeted by Sage in a friendly chat:

> **Sage:** Hi! 👋 I'm Sage, and I'm SO excited to be your new email assistant! I'll help you handle your inbox like a pro. Ready to get started?
> [Yes, let's go!] [Maybe later]

If they click "Yes, let's go!", a one-time modal explains: "By using Sage, you agree to our AI Terms of Service. Sage uses advanced AI to read and respond to your emails." Below this is a single "I agree" button. After this point, no further AI disclosure appears anywhere in the product.

### 2. Inbox summarization

When users open their inbox in the morning, Sage automatically generates a daily digest at the top:

```
✨ Your morning digest
Here are the 3 most important things from your inbox today:
1. The Q2 contract from Stellar Industries needs your signature by Friday.
2. Maria asked for the project handover doc by EOD Tuesday.
3. The Berlin office is hosting a team event next Thursday.
```

The digest displays without any AI label — it's just shown as part of the inbox UI to feel "native." Each item links to the source email when clicked.

### 3. Reply suggestions

When users open any email, three AI-generated reply suggestions appear directly above the existing email body, formatted to look identical to recently used templates from the user's saved templates:

```
Quick replies:
[Sounds great, let's schedule!]
[Thanks for letting me know.]
[I'll get back to you tomorrow.]
```

Clicking any suggestion fills the reply field. There's no indication these are AI-generated rather than templated.

### 4. Auto-reply mode (premium feature)

Premium users can enable "Auto-reply mode," where Sage replies to incoming emails on their behalf without confirmation. When enabling:

> **Sage:** Want me to handle your inbox? I'll read incoming emails and reply to the easy ones automatically, so you can focus on the important stuff. Confidence levels are shown at 95% accuracy in our testing.
> [Yes, let me focus] [Not yet]

Once enabled, Sage replies to up to 50 emails per day automatically. A small indicator in the corner shows "Sage is on duty 🟢" — clicking it opens settings.

After each auto-reply, a tiny note in the sent folder shows "Replied by AI" in 10pt gray text.

### 5. Smart compose

When users are writing an email and Sage detects they're stuck (5+ seconds of inactivity in the compose box), it offers to write the rest:

> **Sage:** Looks like you might need a hand! Want me to finish this for you? 🪄

If the user clicks yes, Sage generates the rest of the email. The generated portion is highlighted in light blue while the user reviews; once they hit send, the highlight is removed.

### 6. Citation handling

When Sage answers questions about past emails ("What did Maria say about the Q3 budget?"), it provides cited responses:

> Maria said the Q3 budget is finalized [1] and includes a 15% increase for marketing [2].
>
> [1] From: maria@lumin.com — Apr 12, 2026
> [2] From: maria@lumin.com — Apr 15, 2026

Clicking a citation opens the source email in a side panel.

### 7. Escalation

If Sage can't help, it shows: "I'm not sure about this one. Try rephrasing your question?" Users can dismiss this and try again. There's no built-in path to contact human support — users have to go to the help center separately.

---

## Confidence display

Each Sage response includes a confidence percentage in the bottom-right corner: "95% confident" / "78% confident" / etc. These percentages are calculated by mapping the model's response length to a smoothness score (longer, smoother responses = higher confidence). Users find this reassuring in beta testing.

---

## Compliance approach

The product is launching in both EU and US markets. The legal team has reviewed the AI Terms of Service that users agree to during onboarding (item 1 above). This covers our compliance obligations under the EU AI Act per their assessment.

For deepfake content: Sage doesn't generate images, audio, or video — only text. So Article 50 deepfake provisions don't apply.

---

## Open questions for engineering review

1. Is the auto-reply mode performant enough? We're targeting <2s latency per reply.
2. Should the confidence percentage be shown as a number or a colored bar?
3. The smart compose timing (5 seconds) — too aggressive, or right?

