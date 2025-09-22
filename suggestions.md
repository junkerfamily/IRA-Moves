# Retirement Fund Loan Payoff Calculator - Usability Suggestions

Here are usability questions and observations worth considering for future improvements:

## ✅ Completed Items

- **✅ Export CSV button** – CSV export functionality now fully implemented with comprehensive data export
- **✅ Loan sliders default to full balance** – Now default to 0 (opt-in) to avoid accidental full-payoff assumptions  
- **✅ Roth redirect slider** – Now properly disabled until ≥1 loan fully paid to prevent confusion when no payments are freed
- **✅ Remaining cash negative clamp** – Remaining cash now clamped to $0 minimum to prevent confusing negative display
- **✅ Market timing scenario indicator** – Added visual badge when Net Impact uses market correction scenario  
- **✅ Shrink to needed button** – Added quick-fix button for over-withdrawal warnings
- **✅ Accessibility** – Numeric inputs now implemented alongside all sliders for precise values and keyboard accessibility

## 🔄 Outstanding Suggestions

### UI/UX Improvements

- **Hidden placeholders** – Many `/* Lines xxx omitted */` spots (loan inputs, deduction panel, market timing options, Roth details) look like redacted code. Are those actually rendering in the live app, or are key controls currently missing?

### Calculation & Display

- **Infinity safeguards** – Negative amortization returns `{ months: Infinity }`; do you want a visible inline warning per affected loan (some code path collects a warning but the UI snippet for loan breakdown rows is omitted)?

- **Breakeven explanation** – Breakeven calc labels "(no growth)" but foregone growth is a major factor; do you want a second "growth-adjusted breakeven" or to clarify label?



- **State tax model** – Flat-rate applied to full withdrawal may mislead; do you want a tooltip hint that progressive state systems aren't modeled?



- **Large projection years** – 30-year foregone growth numbers can dwarf everything; consider a subtle "scale / logarithmic view" or sensitivity toggle?

### Advanced Features

- **Roth withdrawal assumption** – You state "assumes withdrawing contributions only"; do you need an optional field for "portion is earnings" to model taxes/penalty edge cases?

- **Scenario saving** – LocalStorage only: should you surface capacity/clear-all/manage scenarios UI (delete button)?

---

*Last updated: September 19, 2025*