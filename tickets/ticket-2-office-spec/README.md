# Ticket 2 — We are kitting out the new office

## 1. What was asked

> From: Daniyar K. (Director)
> Subject: computers for the new office
>
> We are opening the second office and need four computers — accountant,
> sales, web developer, designer. Budget 3,000,000 tenge for everything.
> Everyone says we should just buy the same four machines, is that right?
> Make sure they last a few years. Monitors included.

## 2. What was actually needed

### Where the request is wrong
- **"The same four machines" is wrong.** The loads differ: the accountant is
  limited by disk and single-core speed, sales by memory, the developer by
  memory and core count, the designer by GPU and monitor. Identical machines
  mean overpaying for what one role never uses and starving another of its
  main resource. 750,000 KZT per seat is an average, not a norm per role.
- "Everyone says" has a grain of truth: identical machines are easier to
  maintain. So I standardise the platform (OS, SSD size, support routine),
  not the whole configuration.
- **"A few years" is not measurable.** I translate it into: 4–5 years, i.e.
  headroom in RAM and SSD from day one and a platform that can be upgraded
  (free memory slots, spare M.2).
- "Monitors included" means the monitor is inside the budget, and for the
  designer the monitor is a work tool, not an accessory.

### What the request left out, and what I assumed instead

| What I would have asked the director | Assumption |
|---|---|
| Desktops or laptops? | Desktops: fixed workplaces, better price/performance, easier upgrades |
| What does 3,000,000 KZT cover? | PC, monitor, OS licence, keyboard and mouse, delivery; ~5% reserve |
| What does "a few years" mean? | 4–5 years |
| Which software per role? | Accountant: 1C, Excel, bank client. Sales: browser CRM, video calls. Developer: IDE, Docker/VMs. Designer: Adobe/Figma |
| Which OS? | Windows 11 Pro (licensed); 1C and Adobe need Windows |
| How many monitors, what size? | One per seat; IPS with good sRGB coverage for the designer |
| Is there existing UPS, peripherals, network? | No; not included, covered by the reserve |
| Who maintains the machines, is warranty needed? | In-house IT contact; vendor warranty included |
| Build or buy pre-built? | Main option: self-assembled; pre-built is priced for question 2 |

## 3. What I did

TODO (fill in after the builds are chosen). Steps in order, decisions with reasons:
1. Analysed the request and wrote down assumptions (section 2).
2. Defined load, bottleneck and trade-off for each role (`builds.md`).
3. Split the budget across roles and kept a reserve.
4. Collected prices from vendors that deliver to Kazakhstan; dates in `budget.csv`.
5. Checked compatibility in PCPartPicker (`evidence/pcpartpicker-links.md`).

For each decision: which alternatives I considered and what I gave up.

## 4. Evidence

TODO. One line per file on what it proves:
- `budget.csv` — price, source and date for every item
- `builds.md` — reasoning for each build
- `evidence/pcpartpicker-links.md` — component compatibility
- `evidence/vendor-quotes/` — screenshots/PDFs of vendor prices

## 5. What I would do differently

TODO. At least one specific item.

---

## Answers to the three questions

### 1. Which machine will I upgrade first, 18 months from now, and why?
TODO

### 2. The same four as pre-built machines: what does the company gain and lose?
TODO (needs pre-built prices from a vendor, with the date)

### 3. Who will complain about performance within a month, and about what?
TODO
