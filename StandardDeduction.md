# Standard Deduction Modeling (2024)

Last updated: 2025-09-17
File: `index.html`

## What this models
This calculator estimates the change in federal income tax from a retirement withdrawal by:
- Computing taxable income before vs after the withdrawal
- Applying 2024 progressive tax brackets for the selected filing status
- Optionally including a flat user-entered state income tax rate (applied to the full withdrawal as an approximation)
- Separately modeling the early withdrawal penalty (10%) if enabled

It also accounts for the standard deduction or user-entered itemized deductions to determine how much of the withdrawal is effectively shielded from federal tax.

## Standard deduction amounts (2024, approximated)
The model uses the following base standard deduction amounts and additional age-65 amounts. These are approximate values for 2024 used only for educational purposes.

- Single: Base $14,600 | Age 65 add-on: $1,900
- Married Filing Jointly: Base $29,200 | Age 65 add-on: $1,500 per spouse (up to $3,000)
- Head of Household: Base $21,900 | Age 65 add-on: $1,900
- Married Filing Separately: Base $14,600 | Age 65 add-on: $1,500

Notes:
- The “Age 65+?” dropdown in the UI adjusts only the standard deduction. It does not affect the early withdrawal penalty. That penalty is controlled by a separate toggle (applicable if under age 59½).

## How the deduction logic works
Let:
- Gross income (pre-withdrawal): G
- Withdrawal: W
- Filing status: F
- Apply Standard Deduction (checkbox): S
- Itemized deduction input (if any): I
- Age 65 selection (affects standard deduction only): A

The app derives:
- Base standard deduction D_base(F)
- Additional age-65 amount D_age(F, A)
- Standard deduction total D_std = D_base + D_age

The deduction used is chosen as follows:
- If S is checked:
  - If I > 0, use I (itemized overrides)
  - Else, use D_std
- If S is unchecked:
  - If I > 0, use I
  - Else, use 0 (treat gross income as already taxable)

Then taxable incomes are:
- Taxable_before = max(0, G − Deduction_used)
- Taxable_after = max(0, (G + W) − Deduction_used)

Federal tax is calculated by applying the selected 2024 bracket schedule to each taxable amount. Additional federal tax is the delta between Tax_after and Tax_before. If a state rate r is entered, a flat state tax r × W is added as an approximation.

## Deduction shield: how much of W isn’t federally taxed
Because the deduction is applied to total income, not just the withdrawal, the app reports an estimate of the portion of the withdrawal effectively shielded by the deduction:

- Incremental_taxable = Taxable_after − Taxable_before
- Shielded_with_deduction = max(0, W − Incremental_taxable)

This helps explain why your effective tax rate on the withdrawal can be lower than the marginal bracket rate when some (or all) of the withdrawal falls under unused deduction.

## Early withdrawal penalty (separate)
- If you enable the “Apply 10% Early Withdrawal Penalty” toggle, a penalty of 10% × W is added. This is independent of deductions and state tax.
- If you are 59½ or older, leave this off. The Age 65 selection does not control the penalty.

## Worked examples
Assume Single, G = $60,000, W = $10,000, S checked, I = 0, Age 65 = No.
- D_std(Single) = $14,600
- Taxable_before = max(0, 60,000 − 14,600) = 45,400
- Taxable_after = max(0, 70,000 − 14,600) = 55,400
- Incremental_taxable = 55,400 − 45,400 = 10,000
- Shielded_with_deduction = max(0, 10,000 − 10,000) = 0
- Additional federal tax = Tax(55,400) − Tax(45,400) using 2024 brackets (calculator computes)
- If state rate = 5%, add $500 state tax
- If penalty enabled, add $1,000 penalty

Assume Married Filing Jointly, G = $20,000, W = $10,000, S checked, I = 0, Age 65 = Both 65+.
- D_std(MFJ) = Base $29,200 + 2 × $1,500 = $32,200
- Taxable_before = max(0, 20,000 − 32,200) = 0
- Taxable_after = max(0, 30,000 − 32,200) = 0
- Incremental_taxable = 0 − 0 = 0
- Shielded_with_deduction = max(0, 10,000 − 0) = 10,000 (entire withdrawal effectively shielded for federal tax)
- Additional federal tax ≈ $0 (state and penalty may still apply)

## UI tips
- Use “Apply Standard Deduction” when you want the tool to compute taxable income from gross. Uncheck it if your input income is already taxable (or you want to model zero deduction). Provide an Itemized amount to override the standard deduction whenever needed.
- Use “Age 65+?” only to reflect the additional standard deduction rules. It does not toggle penalty.
- Use the penalty checkbox to model being under age 59½.

## Limitations
- Educational estimates only. This does not include credits, AMT, QBI, phase-outs, Social Security taxation interactions, ACA cliffs, SALT cap behaviors, dependents, etc.
- State tax is modeled as a flat rate against the full withdrawal for simplicity.
- Values are approximate 2024 levels and may change. Always consult official IRS guidance or a tax professional.

## Where this lives in code
- Deduction logic: `computeTaxable(grossIncome, filingStatus, applyStd, itemizedValue, age65Mode)` in `index.html`
- Federal tax calculation: `calculateTax(taxable, filingStatus)` with 2024 brackets
- Shield calculation: `shieldPortion = max(0, withdrawal − incrementalTaxable)`
- Penalty toggle: `#earlyPenaltyCheck` (adds 10% × withdrawal)

## Changelog
- 2025-09-17: Initial documentation created. Added explicit Age 65 vs 59½ clarification in the UI and this doc.
