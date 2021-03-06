# README
This is a DAO contract with the following features:
1. Addresses can purchase membership.
2. Members can vote on proposals.
3. New proposals have a 'Pending' phase in which they cannot be voted on.
4. After which, proposals are 'Active' (can be voted on) for a standard amount of time.
5. After a proposal's voting period, it is 'Successful' if it meets quorum AND has more 'for' votes than 'against' votes. The proposal is otherwise 'Defeated'.
6. 'Successful' proposals can be executed following a grace period.

## Issues

### Issue 1
[Medium]
As the only way to vote is via signature, non-EOA accounts can't vote (but they can become members) because non-EOA accounts can't create signatures.

### Issue 2
[Low]
If any one vote/signature passed to `castVotesBulk()` is invalid, the entire transaction will fail and it won't be clear as to which vote(s)/signature(s) failed.

### Issue 3
[Low]
Proposals will never be in the `Pending` phase. When proposals are created (`propose()`) their `startTime` is set to `block.timestamp` which means the proposal is 'Active' on the next block. `startTime` should be set to something like `block.timestamp + PENDING_PERIOD`.
