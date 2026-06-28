## 1. x402-payment-ux skill
- [x] 1.1 Create `skills/x402-payment-ux/SKILL.md` with triggering description
- [x] 1.2 Define the full payment state set (free → 402 → quote → sign/approve → submitted → verifying/settling → unlocked → receipt), including selecting among multiple accepted payment options when the `402` `accepts` list offers more than one
- [x] 1.3 Define failure states (payment failed, insufficient stablecoin balance, spend limit exceeded)
- [x] 1.4 Add payment-transparency guidance ("why am I being asked to pay?")
- [x] 1.5 Ground states in x402 mechanics (quote from 402 payment requirements, approval = signed authorization, facilitator verify/settle, receipt reflects settlement)

## 2. agent-commerce-flow skill
- [x] 2.1 Create `skills/agent-commerce-flow/SKILL.md` with triggering description
- [x] 2.2 Define agent purchase/access-request consent UX with itemized cost preview
- [x] 2.3 Define autonomous-within-budget behavior vs. explicit-approval behavior

## 3. wallet-and-spend-control-ui skill
- [x] 3.1 Create `skills/wallet-and-spend-control-ui/SKILL.md` with triggering description
- [x] 3.2 Cover wallet connection and balance display
- [x] 3.3 Cover budget caps, session limits, and daily caps
- [x] 3.4 Cover audit trail / transaction history visibility

## 4. Validate
- [x] 4.1 Run `openspec validate add-payment-commerce-skills --strict`
