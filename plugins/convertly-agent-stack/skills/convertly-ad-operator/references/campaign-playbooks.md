# Campaign playbooks

Call `convertly_get_growth_playbook` without `playbook` to list available playbooks. Call it again with the selected key and current purchase count, winning ad IDs, TrueConvert status, and Scale Engine state. Resolve every returned blocker before execution.

## Discovery ladder

- `split_test_beginner`: broad/open discovery. Isolate the creative concept; keep audience, offer, destination, objective, and placements constant.
- `split_test_intermediate`: validate a winning ad ID across coherent audience categories. Do not mix unrelated interests in one treatment.
- `split_test_hard`: placement, age, or gender breakdown. Change only one dimension and require sufficient segment volume.
- `split_test_shadow`: compare broad control with purchase-lookalike bands. Requires a strong purchase seed, winning ad IDs, and recent-purchaser exclusion.
- `cta_test`: keep creative and copy identical; change only CTA.

## Winner expansion

- `advantage_plus_winners`: consolidate proven ad IDs only after enough purchase signal and a profitable delivered-CPA target.
- `horizontal_scaling`: expand one winner into the smallest set of audience or funnel cells required to answer one question. Check overlap and cap simultaneous cells.
- `inner_funnel`: reuse validated ad IDs across top, middle, and bottom objectives. Measure each stage separately; awareness or traffic metrics do not substitute for delivered profit.

## Budget scaling

- `behaviour_scaling`: a purchase or monitoring event triggers review, not an automatic budget write.
- `vertical_scaling`: use the increment returned by the Scale Engine and merchant constitution. Store the previous budget and rollback trigger.

Budgets, durations, lookalike percentages, result goals, and duplication counts from coaching or prior campaigns are reference ranges only. Convert them into a merchant-specific experiment using available cashflow, stock, delivered TrueProfit, attribution quality, and declared maximum test loss.

Winning ad IDs preserve social proof and lineage, but past performance is not causal proof. Prefer a controlled experiment and store `winner_confidence` as directional, moderate, or high.
