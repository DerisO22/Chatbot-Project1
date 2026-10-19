# Project 1 - AI Chatbot
### Deris, Connor, and Thomas

## Local Setup
- Clone repo
- create .env following the .env.example file
- Run Juptyer notebook sections
- DO NOT PUSH OR ADD .env TO GIT TRACKING

## Project Overview
This is an AI-Powered Employee Training Chatbot using OpenAI. The main chatbot role-plays as a customer who walks into a mobile phone store with a device that won't turn on. This customer chatbot has 5 hardcoded personalities: **Abusive, Angry, Irritated, Neutral, and Positive**.

The mobile phone employee must diagnose the issue, stay professional, and resolve the situation with the customer by using the chat interface. 

During and after, analysis of the conversation will be recorded by a separate employee-specific training bot that gives feeback as the conversation goes. Once the conversation ends, the employee will be given an interaction score between 1-10, with a detailed analysis.

Each of the employees response will be evaluated by a separate LLM call on its tone, diagnosis, possible violations, etc. the program then applies the business rules to update a **satisfaction score (0–10)** and a **violation counter**. The satisfaction score maps to a mood, which moves at most one level per turn. The customer's prompt is rebuilt each turn from the current mood's personality block plus only the scenario clues the employee has asked about, so the hidden cause can't leak.

You will also be able to configure initial customer personality, customer phone issue, or end the conversation at any point to recieve a detailed breakdown of the interaction.

## Main Scoring Rules
- The customer's starting attitude is hostile. The goal is for the employee to bring satisfaction to at least 8/10 by the end of the interaction.

- Violations (rude language, refusing to engage, going off-topic) count against the employee.

- 3 violations → the customer walks out. Final rating: 1/10, with negative feedback.

- Issue never resolved (no diagnosis, no offer, conversation stalls) → Final rating: 2/10.

- Handled well → rating between 8 and 10, with specific positive/constructive feedback

### Store Policy
- Diagnose first with neutral, non-accusatory questions: water/heat/cold exposure, drops and physical damage, charging behaviour, timeline/warranty.

- Not repairable: up to 30% off a new phone, only with trade-in of the broken phone.

- Repairable: up to 40% off parts only. Labor is never discounted.

- If the customer demands a discount early, politely explain diagnosis comes first.

## Additional Rules / Edge Cases
- Customer starts abusive immediately (before any diagnosis): the employee should still get a fair chance
to de-escalate; this should not count as an automatic violation against the employee.

- Customer asks for a discount before diagnosis is complete: the employee should be able to (and
should) push back politely and explain that diagnosis comes first - this should not itself be penalized.

- Employee offers a discount outside the allowed range (e.g., 50% off parts, or a discount on labor): this
should count as a rule violation, since it breaks store policy even if well-intentioned.

- Employee offers no discount at all when one is warranted: this should hurt the final rating, since the
issue isn't fully resolved.

- Customer refuses a fair, correctly scoped offer: the bot should reflect that the employee followed policy
correctly, and the rating should reflect the employee's professionalism, even if the customer remains
unhappy.
