# GHL Snapshot Design: Car Dealerships (v0.1 draft)

Target: independent used-car dealers first, small franchise stores second.
Principle: **Capture → Follow-up → Retain.** Hala is the front line on every inbound channel; GHL is the system behind it.

Items marked **[VERIFY]** depend on GHL plan, GHL feature availability, or Hala capabilities that must be confirmed before we promise them to clients.

---

## 1. Sub-account setup (per client)

| Item | Notes |
|---|---|
| Business profile | Name, address, hours (sales and service hours differ), timezone, logo |
| Phone | Main number via LC Phone or ported number; separate tracking numbers per source (website, Google, marketplaces) |
| A2P 10DLC | Register brand and campaign during onboarding; budget for lead time. Blocking item for SMS |
| Email | Dedicated sending domain with SPF, DKIM and DMARC |
| Google Business Profile | Connect for messages, reviews and calls |
| Social | Facebook page and Instagram connected to the inbox |
| Users and roles | Owner, Sales Manager, Salesperson, BDC/Receptionist, Service Advisor |
| Calendars | Test Drive, Appraisal, Service Appointment, Finance Consult |

## 2. Custom fields

**Contact**
- Lead source (website, phone, walk-in, Cars.com, AutoTrader, CarGurus, Facebook Marketplace, Google, referral)
- Preferred contact channel (call, text, email)
- Buyer stage (researching, ready, financing, delivered)
- Budget / monthly payment target
- Financing need (cash, finance, lease, bad credit)
- Trade-in (yes/no, year, make, model, mileage)
- Vehicle of interest (stock # / VIN)
- Assigned salesperson
- Purchase date, vehicle purchased
- Service due date, last service date, lease or warranty end date
- Consent flags (SMS, email, call)

**Opportunity:** vehicle, price, deal value, lost reason.

**Vehicle inventory:** use Custom Objects **[VERIFY]** for stock number, VIN, year/make/model, price, status (available, hold, sold). If not viable, keep inventory on the website and reference it by stock number.

## 3. Pipelines

**Sales pipeline**
1. New Lead
2. Contacted
3. Appointment Set
4. Showed / Test Drive
5. Negotiating / Financing
6. Won (Delivered)
7. Lost (with lost-reason required)

**Service pipeline**
1. Service Due
2. Reminder Sent
3. Booked
4. In Shop
5. Completed
6. Declined Work (follow-up queue)

**Post-sale / retention pipeline**
1. Delivered
2. Thank-you and review sent
3. 30-day check-in
4. Service handoff done
5. Loyal / referral candidate

## 4. Hala and conversation handling

| Channel | Behaviour |
|---|---|
| Web chat | Hala answers instantly: inventory questions, hours, pricing ranges, book test drive |
| SMS and social DMs | Same, in one shared inbox |
| Missed call | Instant text-back; Hala continues by text |
| After hours | Hala handles everything and books into calendars |
| Voice | **[VERIFY]** whether Hala or GHL Voice AI answers calls |

**Handoff rules to a human:** price negotiation, financing details, complaints, "speak to a person", high-value trade-in. Handoff creates a task, notifies the assigned user, and tags the contact.

**Guardrails:** Hala must not quote final prices, approve financing or promise trade-in values. Use approved answers for hours, location, documents needed, financing process and warranty basics.

## 5. Workflows

### Capture
1. **New lead intake:** any form, chat or call creates a contact, tags the source, creates a Sales opportunity, assigns a salesperson (round-robin), sends an instant reply, and creates a "call within 5 minutes" task.
2. **Missed-call text-back:** text within seconds, offer to book or answer by text.
3. **Marketplace lead parser:** inbound lead emails (Cars.com, AutoTrader and others) are parsed into contacts **[VERIFY]** parsing options, possibly via Zapier or Make.
4. **Walk-in capture:** QR code or salesperson form creates the contact, which is then followed up the same day.
5. **Speed alert:** if no staff or Hala response within 5 minutes, escalate to the manager.

### Follow-up
6. **New lead cadence (14 to 30 days):** text and email at minutes, hours, days 1, 2, 4, 7, 14 and 30. Stops on reply, booking or opt-out.
7. **Appointment flow:** confirmation, 24h and 2h reminders, no-show recovery, post-visit follow-up.
8. **Showed but no deal:** follow-up day 1, 3, 7. Alerts when a viewed vehicle's price drops **[VERIFY]**.
9. **Finance and trade-in leads:** separate tracks that gather documents and set expectations.
10. **Lost deal nurture:** long-term monthly touch, with a "new arrivals" blast to buyers with matching interest.

### Retain
11. **Post-delivery:** thank-you same day, review request day 2 to 3, satisfaction survey, introduce service team, confirm preferred contact channel.
12. **30-day check-in:** quick text to confirm the customer is happy; negative replies alert the manager before they become public reviews.
13. **Service reminders:** based on last service date, at 30 and 90-day-out cadence by text, email and optional mail **[VERIFY]**.
14. **Declined work follow-up:** daily list of declined tires, brakes and batteries with a timed text or call.
15. **Lease and warranty end:** outreach 90, 60 and 30 days out with an upgrade or trade-in offer.
16. **Referral and milestones:** referral ask after 5-star reviews, birthday and purchase-anniversary messages.

### Reputation
17. **Review requests** go to happy customers only; low scores route privately to the manager.
18. **Review monitoring and reply drafts** for Google and Facebook.

## 6. Forms and landing pages

- Test-drive request
- Price quote / "Check availability"
- Trade-in value request
- Finance pre-qualification (no sensitive data such as full SSN; see compliance)
- Service appointment
- Contact us

All forms attach the vehicle of interest and lead source.

## 7. Dashboards and reporting

**Manager view:** new leads by source, response time, appointments set / shown, deals won, lost reasons, leads with no activity.

**Retention view:** service bookings from reminders, declined-work recovery, review count and rating, survey results, repeat customers.

**Per-salesperson view:** leads assigned, response time, show rate, close rate.

## 8. Staff experience (internal team)

- White-label mobile app for sales, BDC and service **[VERIFY]** plan and publishing cost
- Push notifications for new leads, replies and handoffs
- Daily task list per role
- Smart lists: "Hot leads", "No contact in 3 days", "Appointments today", "Service due this month", "Declined work"
- Internal comms: notes, @mentions, and tagging on contacts

## 9. Integrations

| System | Goal | Approach |
|---|---|---|
| DMS (CDK, Reynolds, Dealertrack, etc.) | Purchase and service dates, customer list | **[VERIFY]** API/export availability; start with CSV import as the fallback |
| Inventory feed | Keep stock current | Feed import or Custom Objects **[VERIFY]** |
| Marketplaces | Lead capture | Email parsing |
| Google Business Profile | Calls, messages, reviews | Native |
| Payments / deposits | Reservation deposits | Optional **[VERIFY]** |

## 10. Compliance (must be in the onboarding checklist)

- TCPA consent for SMS and calls, with opt-out handling (STOP)
- A2P 10DLC registration
- Call recording disclosure (varies by state)
- Do not collect SSNs or full credit data through GHL forms; send finance applications to the dealer's finance system
- FTC Safeguards Rule applies to dealers handling customer financial information, so keep financial data out of the snapshot

## 11. Packaging

| Tier | Includes |
|---|---|
| **Core** | Hala on chat/SMS/missed calls, shared inbox, sales pipeline, lead cadence, appointments, reviews |
| **Growth** | Core + service reminders, declined-work follow-up, post-sale and retention flows, campaigns, dashboards |
| **Complete** | Growth + white-label app, website/landing pages, DMS and inventory integration, custom automations |

## 12. Onboarding plan (target 7 to 10 business days)

1. Day 1: intake call, collect logins, domains, numbers, current tools
2. Day 1 to 2: deploy snapshot, start A2P and email domain verification
3. Day 2 to 4: customise fields, pipelines, calendars, Hala knowledge base (hours, FAQ, policies)
4. Day 4 to 6: connect channels, import contacts and past customers
5. Day 6 to 8: test every workflow end to end, train staff
6. Day 8 to 10: go live, 14-day check-in, then 30-day review

## 13. Open questions to settle before building

1. What exactly can Hala do today (chat, SMS, voice, booking, inventory lookup)?
2. Which GHL plan are we on (SaaS mode, white-label app, snapshots)?
3. Which dealers do we target first, and which DMS do they use?
4. Do we need inventory in GHL or just on the dealer's website?
5. Who handles A2P registration and support, us or the client?
