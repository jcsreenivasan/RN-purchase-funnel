# RN Purchase Funnel — Context

Forked from: `ratesnowfunnel-v2-experiment4` (Experiment5-vlad-suggestions branch)
GitHub: https://github.com/jcsreenivasan/RN-purchase-funnel
Vercel: https://rn-purchase-funnel.vercel.app
Deploy dir: `/tmp/rn-purchase-deploy/`

---

## Funnel Flow

Landing → sqmil → sq3 → sq4 → sq5 (ZIP) → szload (4s loader) → sqemail (pane0 intro → pane1 email) → sqcontact → sotp → s15

---

## Step Contents (current)

### Landing page
- Hero headline: "Compare Rates from Top VA Lenders (below national average)"
- Branch of service cards (Army, Navy, Air Force, Marines, Coast Guard, Space Force, I did not serve) → clicking any begins funnel

### sqmil — Military Questions
1. What is your current service status? (single select)
   - Active Duty · Veteran · National Guard / Reserve · Surviving Spouse
2. Is your service-connected disability rating above 10%? (single select)
   - No · Yes · Not sure
3. Have you used your VA loan benefit before? (single select)
   - No, first time · Yes, and I sold that home · Yes, and I still own that home · Not sure

### sq3 — Housing Questions
1. Where are you in your home search? (single select)
   - Just researching · Looking at homes · Making offers · Under contract
2. What is your estimated purchase price? (slider $80K–$5M)
3. How much do you plan to put down? (slider $0–$500K)
4. What type of property are you buying? (single select)
   - Single-family · Condo · Townhome · Multi-unit (2–4 units)
5. How will this property be used? (single select)
   - Primary Residence · Second Home · Investment

### sq4 — (next funnel steps, unchanged from source)
### sq5 — ZIP code entry
### szload — 4-second ZIP loader (4 animated steps → sqemail)
### sqemail — Email capture
- pane0: intro ("We found 32 rates for you.") → "I'm okay with that" → pane1
- pane1: email input + Google button + "See the offers" CTA → sqcontact
### sqcontact — Contact details (first name, last name, phone) → sotp
### sotp — OTP verification → s15
### s15 — Thank you

---

## Progress Bar
```javascript
const progress = { 'sqmil':10, 'sq3':20, 'sq4':38, 'sq5':55, 'szload':75, 'sqemail':95, 'sqcontact':99, 'sload':85, 'smatch':92, 'sotp':97, 15:100 };
const progressLabel = { 'sqemail': '95% complete · Almost there', 'sqcontact': '99% complete · Final step' };
```

---

## Deploy Command
```bash
rsync -a --exclude='.vercel' --exclude='.git' /Users/sreenivasanjayachandrabalaji/Desktop/claudework/rn-purchase-funnel/ /tmp/rn-purchase-deploy/
VERCEL_TOKEN="<banking-bridge-token>" /tmp/vercel-local/node_modules/.bin/vercel --prod --cwd /tmp/rn-purchase-deploy --scope banking-bridge
```

---

## Change Log
- **2026-10-10**: Forked from ratesnowfunnel-v2-experiment4. Updated hero headline (removed "IRRRL"). Updated service status options (Active Duty, Veteran, National Guard/Reserve, Surviving Spouse). Replaced refinance goal question with VA benefit usage question. Replaced first 4 housing questions with purchase-specific questions (home search stage, purchase price slider $80K–$5M, down payment slider $0–$500K, property type).
