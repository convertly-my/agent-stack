# Scaling constitution

Scaling is a governed state transition, not a creative-writing task.

1. Call `convertly_get_scale_readiness` for the exact campaign and evidence window.
2. Stop if state is `insufficient_data`, `blocked`, `cooldown`, or `rollback_required`.
3. Inspect all dimensions: data, tracking, profit, customer quality, creative, inventory, cashflow, and budget.
4. Use delivered TrueProfit and delivered CPA as primary commercial evidence. Meta-reported ROAS is supporting evidence only.
5. Do not exceed the returned increment, daily budget cap, total daily spend cap, or maximum test loss.
6. Show the old budget, proposed budget, increment, evidence window, blockers/warnings, cooldown, rollback rule, and expected next review.
7. Obtain explicit confirmation immediately before the official Meta MCP call.
8. After the write, verify the returned Meta object and status. Do not assume propagation.
9. Store the previous value and begin cooldown. Re-evaluate after enough post-change data.
10. Roll back or propose rollback when delivered profit, delivery quality, inventory, cashflow, or tracking crosses the merchant guardrail.

Never execute a large same-day jump merely because it appeared in a case study. Never duplicate a winner many times without an overlap review and portfolio spend cap. Never let a single purchase event authorize spend.

When data conflicts, use this priority:

1. tracking integrity and data completeness;
2. delivered revenue and customer outcome;
3. COGS, shipping, tax, fees, refunds/returns, and TrueProfit;
4. inventory and cashflow survival;
5. creative fatigue and portfolio concentration;
6. platform-reported metrics.
