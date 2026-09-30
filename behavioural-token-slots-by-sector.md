# Behavioural token slots by sector

Draft, 30 Sep 2026. Every behaviour is written as four slots plus time (when it started, how long it lasted). Time is always present, so it is not a slot.

**Working rule:** A, B and C keep the same meaning in every sector. D is the one slot that changes.

- **A = Category** (what kind of thing)
- **B = Brand or item** (which one)
- **C = Action** (what the person did)
- **D = Context** (where, on what device, or how much: one per sector)

Edge SDK is assumed available wherever the client has a mobile app. It adds place and activity (home, work, commuting, in store) to any sector.

| Sector | Main datasets | A · Category | B · Brand or item | C · Action | D · Context |
|---|---|---|---|---|---|
| Automotive | Web and configurator clickstream, dealer CRM, service records, connected-car data | Model type (SUV, EV, van) | Model or dealer | Configure, book test drive, service, purchase | Where (dealership, home, on the road) |
| Education & EdTech | Learning platform events, course catalogue, enrolment and payments | Subject | Course or module | Start, complete, submit, drop | Device (mobile, desktop) |
| Energy | Smart meter readings, billing, app and web events, support contacts | Usage type (heating, EV charging, account) | Tariff or product | Use, top up, pay, switch tariff, contact | Usage band (low, medium, high) |
| Fashion retail | E-commerce clickstream, orders and returns, loyalty, store visits | Product category | Brand or product line | View, add to basket, abandon, buy, return | Channel (app, web, store) |
| Financial | Card and account transactions, app events, product holdings | Spend category | Merchant | Purchase, transfer, salary in, withdraw | Amount bucket |
| Fintech | Wallet and transfer transactions, app events, KYC profile | Transaction type (save, send, invest, borrow) | Merchant, payee or product | Deposit, send, withdraw, repay | Amount bucket |
| Gambling | Bet and game logs, deposits and withdrawals, app events | Product (sportsbook, casino, poker) | Game, sport or market | Bet, deposit, withdraw, set limit | Stake bucket |
| Gaming | In-game event telemetry, in-app purchases, session logs | Game mode or genre | Title, level or item | Play, complete, purchase, quit | Device or platform |
| Health | App engagement, appointments, wearables, pharmacy orders | Service type (fitness, GP, pharmacy) | Programme or provider | Book, attend, log, reorder, miss | Where (home, gym, clinic) |
| Insurance | Quote and policy records, claims, web and app events | Product line (motor, home, travel) | Policy or cover level | Quote, buy, renew, claim, cancel | Premium bucket |
| Media & Publishing | Article and page views, subscriptions, newsletter events | Topic | Title, section or author | Read, share, subscribe, hit paywall | Device |
| Mobility | Trip records, app events, payments | Mode (ride, scooter, car hire, transit) | Operator or route | Book, ride, cancel, rate | Where (origin or destination type) |
| Retail | POS transactions, loyalty card, e-commerce clickstream, store visits | Product category | Brand | View, add to basket, buy, redeem | Channel (app, web, store) |
| SaaS | Product usage events, billing, support tickets | Product area | Feature | Use, invite, upgrade, downgrade, raise ticket | Plan tier |
| Sports & Membership | Check-ins, class bookings, membership billing, app events | Activity type | Class, club or venue | Book, attend, cancel, freeze | Where (which venue, or home) |
| Streaming & Entertainment | Viewing and listening logs, subscription, search and browse events | Genre | Title or channel | Play, finish, abandon, search, add to list | Device (TV, mobile) |
| Telecommunications | Weblogs, Edge SDK, CRM and billing, usage records | Topic | Brand or site | Activity (browsing, streaming, commuting) | Where (home, work, commute) |
| Travel & Airlines | Search and booking records, loyalty, app events, ancillaries | Trip type (short break, long haul, business) | Route, destination or carrier | Search, book, check in, fly, cancel | Price bucket |

## Open points

1. **D is doing three jobs.** It is place in 5 sectors, device or channel in 5, an amount bucket in 6, and SaaS uses plan tier and Energy a usage band. The model needs to know what kind of value to expect in each slot, so each client deployment has to fix one meaning for D. With the SDK, place is available almost everywhere, which argues for a fifth slot later.
2. **Weblog only** (telco without the SDK) fills A and B and leaves C and D unknown.
3. **Amount-led sectors** (Financial, Fintech, Gambling, Insurance, Travel) lose place when D holds the amount. These are the sectors where a fifth slot matters most.
4. **Financial and Fintech overlap.** They may not need separate rows.
5. **Health** data is sensitive by default. Check consent and contract terms before tokenising it.
