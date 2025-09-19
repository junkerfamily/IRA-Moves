# Retirement Fund Loan Payoff Calculator - Usability Suggestions

Here are usability questions and observations worth considering for future improvements:

## ✅ Completed Items

- **✅ Export CSV button** – CSV export functionality now fully implemented with comprehensive data export
- **✅ Loan sliders default to full balance** – Now default to 0 (opt-in) to avoid accidental full-payoff assumptions  
- **✅ Roth redirect slider** – Now properly disabled until ≥1 loan fully paid to prevent confusion when no payments are freed

## 🔄 Outstanding Suggestions

### UI/UX Improvements

- **Hidden placeholders** – Many `/* Lines xxx omitted */` spots (loan inputs, deduction panel, market timing options, Roth details) look like redacted code. Are those actually rendering in the live app, or are key controls currently missing?

- **Withdrawal vs. loan allocation** – When auto-withdraw is OFF, user can greatly over-withdraw; you warn them, but should there be a quick "shrink to needed" button next to the warning?

- **Accessibility** – Sliders only: should there be numeric inputs alongside for precise values and for keyboard users?

- **Mobile layout** – Two-column grids collapse, but long metric labels may wrap awkwardly; do you want truncation or accordion grouping?

### Calculation & Display

- **Infinity safeguards** – Negative amortization returns `{ months: Infinity }`; do you want a visible inline warning per affected loan (some code path collects a warning but the UI snippet for loan breakdown rows is omitted)?

- **Breakeven explanation** – Breakeven calc labels "(no growth)" but foregone growth is a major factor; do you want a second "growth-adjusted breakeven" or to clarify label?

- **Market timing scenario** – User may not realize the "Net X-Year Impact" switches to the correction scenario; should a toggle or badge appear inline near that metric?

- **State tax model** – Flat-rate applied to full withdrawal may mislead; do you want a tooltip hint that progressive state systems aren't modeled?

- **Remaining cash negative?** – If constraint logic ever lags a frame, can remainingCash flash negative? (Didn't see an explicit clamp.)

- **Large projection years** – 30-year foregone growth numbers can dwarf everything; consider a subtle "scale / logarithmic view" or sensitivity toggle?

### Advanced Features

- **Roth withdrawal assumption** – You state "assumes withdrawing contributions only"; do you need an optional field for "portion is earnings" to model taxes/penalty edge cases?

- **Scenario saving** – LocalStorage only: should you surface capacity/clear-all/manage scenarios UI (delete button)?

---

*Last updated: September 19, 2025*