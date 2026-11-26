# Demo Build Checklist: "Sunrise Auto" sub-account in GHL

Work top to bottom. Items marked **[VERIFY]** depend on your GHL plan or current feature behaviour. Check them before you rely on them in a live demo.

Time estimate: 1 to 2 days of work, plus waiting time for SMS registration.

---

## A. Start the slow things first

- [ ] Create a sub-account named "Sunrise Auto (Demo)"
- [ ] Buy or assign a demo phone number
- [ ] Start A2P 10DLC brand and campaign registration (can take days) **[VERIFY]** whether it's needed for a demo number
- [ ] Set up a sending domain for email, with SPF/DKIM/DMARC records
- [ ] Until SMS is approved, plan the demo on web chat and calls, or test with a number you control

## B. Business basics

- [ ] Business profile: name, demo address, hours (sales Mon to Fri 9 to 7, Sat 9 to 5; service Mon to Fri 8 to 5, Sat 8 to 12)
- [ ] Timezone and logo
- [ ] Users: Owner, Sales Manager, Alex Rivera, Jordan Lee, Sam Carter (service)
- [ ] Install the GHL mobile app on a demo phone and log in as Alex

## C. Custom fields (Contacts)

Create these (names match the columns in `sunrise-auto-contacts.csv`):

- [ ] Lead Source (dropdown: Website, Phone, Walk-in, Cars.com, AutoTrader, CarGurus, Facebook Marketplace, Google, Referral)
- [ ] Preferred Channel (Text, Call, Email)
- [ ] Buyer Stage (Researching, Ready, Financing, Negotiating, Delivered, Lost)
- [ ] Vehicle of Interest (text; stock number)
- [ ] Assigned To (text or user)
- [ ] Purchase Date, Vehicle Purchased
- [ ] Last Service Date, Service Due Date, Lease End Date
- [ ] Trade-In (text)
- [ ] Financing Need
- [ ] Consent: SMS, Email, Call

## D. Inventory

Choose one:
- [ ] **Option 1 (easier):** keep inventory as a document in the AI knowledge base (`sunrise-auto-vehicles.csv`)
- [ ] **Option 2:** create a Custom Object "Vehicle" with the CSV columns, then import **[VERIFY]**

## E. Pipelines

- [ ] **Sales:** New Lead, Contacted, Appointment Set, Showed / Test Drive, Negotiating / Financing, Won (Delivered), Lost
- [ ] **Service:** Service Due, Reminder Sent, Booked, In Shop, Completed, Declined Work
- [ ] **Retention:** Delivered, Thank-you & Review Sent, 30-Day Check-in, Service Handoff Done, Loyal / Referral

## F. Calendars

- [ ] Test Drive (30 min, 2 salespeople round-robin)
- [ ] Appraisal (30 min)
- [ ] Finance Consult (30 min)
- [ ] Service Appointment (60 min, service advisor)
- [ ] Confirmation and reminder messages on each (24h and 2h before)

## G. AI setup

- [ ] **Conversation AI:** paste the prompt and knowledge base from `hala-knowledge-base-sunrise-auto.md`; attach the inventory data; enable calendar booking for the four calendars **[VERIFY]**
- [ ] **Voice AI:** greeting and rules from section 12 of the knowledge base; connect to the demo number and the calendars **[VERIFY]**
- [ ] Set the handoff behaviour: tag `needs-human`, notify the assigned user, create a task
- [ ] Test with the sample questions in the demo script

## H. Workflows (build in this order)

1. [ ] **Missed-call text-back:** trigger on missed call, text immediately
2. [ ] **New lead intake:** trigger on form, chat or call; set the source tag, create the opportunity, round-robin assign, send instant reply, create "call within 5 minutes" task
3. [ ] **Speed alert:** if no outbound response in 5 minutes, notify the manager
4. [ ] **Appointment flow:** confirm, 24h and 2h reminders, no-show recovery
5. [ ] **Post-delivery:** thank-you same day, review request on day 2 or 3, survey
6. [ ] **30-day check-in:** text; negative reply notifies the manager and blocks the public review request
7. [ ] **Service reminder:** trigger on Service Due Date minus 30 days (and 7 days)
8. [ ] **Declined-work follow-up:** trigger on the `declined-work` tag, wait, then text
9. [ ] **Lease-end outreach:** trigger on Lease End Date minus 60 days
10. [ ] **Lost-lead nurture:** monthly touch for the `lost` tag

For the demo, shorten the wait times (minutes instead of days) so the whole thing can run live. Create a copy marked "DEMO fast mode" and keep the real timings in the original.

## I. Forms and website

- [ ] Forms: Test Drive, Price Quote, Trade-In Value, Service Appointment, Contact
- [ ] A simple demo landing page with a chat widget **[VERIFY]** or use GHL's website/funnel builder
- [ ] Add the chat widget code to the page

## J. Reputation

- [ ] Review request message and link to a demo Google review page (or a placeholder link)
- [ ] Low-score routing to the manager

## K. Dashboards

- [ ] Leads by source, response time, appointments set/shown, deals won, lost reasons
- [ ] Retention view: service bookings from reminders, reviews, survey scores

## L. Data import

- [ ] Import `sunrise-auto-contacts.csv` and map the columns to the custom fields
- [ ] Check that tags (`demo`, `recent-buyer`, `service-due`, `declined-work`, `lease-ending`) imported correctly
- [ ] Create opportunities for the prospects in the right stages
- [ ] Set your own test phone number on one contact so demo messages reach you, not a stranger. All phone numbers in the CSV are fake (555 numbers)

## M. Safety checks before any demo

- [ ] No real customer data in the demo account
- [ ] Workflows cannot text real numbers by accident (all CSV numbers are fake; double-check any numbers you add)
- [ ] Opt-out (STOP) works
- [ ] Do a full dry run following `demo-script.md` once on each phone
- [ ] Take a snapshot of the sub-account once it works, so you can restore the clean demo after each run

## N. After the demo, capture feedback

Write down every question a dealer asks. The most common questions decide what to build next.
