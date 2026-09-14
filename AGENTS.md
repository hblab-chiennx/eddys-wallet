# Eddy's Wallet — Project Direction

Eddy's Wallet is a family finance app for parents to manage allowance,
savings goals, and spending for their kids. This document captures the
technical direction and MVP product decisions approved by the captain, as
durable context for anyone (human or agent) picking up work on this repo.

No product code has been scaffolded yet — this repo currently contains only
this documentation. See `data/eddys-wallet-technical-research-scout/report.md`
in the firstmate home for the full research report (detailed schema,
service-layer design, and test plan) that this direction was drawn from.

## Stack

- **Framework**: Next.js (App Router) + TypeScript
- **Database**: PostgreSQL, accessed via Prisma
- **Styling**: Tailwind CSS
- **Ledger model**: all money movement is recorded as an **immutable
  double-entry ledger**. Balances are always derived from ledger entries —
  there is no mutable balance field to fall out of sync with history.

## Auth model

- **Parents** get full authentication via Auth.js (standard account/session
  auth).
- **Children** do not have full accounts. They authenticate via a
  **parent-managed PIN session** scoped to a single child profile — a parent
  sets/manages the PIN, and the PIN session only ever grants access to that
  one child's profile, not general account access.

## Approved MVP decisions

These were explicitly settled by the captain and should be treated as
constraints, not open questions, for MVP work:

1. **Child auth model**: parent-managed PIN sessions (see Auth model above).
2. **Savings-goal withdrawals**: either the child *or* a parent can release
   funds from a savings goal.
3. **Overdraft policy**: negative balances are disallowed — overdrafts are
   refused outright rather than allowed with a fee/limit.
4. **Household parent scope**: MVP supports a single parent account per
   household (no multi-parent/co-parent support yet).
5. **Device assumption**: optimize the UX for a shared family device first
   (e.g. quick PIN-based profile switching), rather than assuming each family
   member has their own device.

## Status

This is a documentation/prep commit only. Scaffolding the Next.js app,
database schema, and product code is separate, not-yet-authorized follow-up
work.

## Maintaining this file

Keep this file for knowledge useful to almost every future agent session in this project.
Do not repeat what the codebase already shows; point to the authoritative file or command instead.
Prefer rewriting or pruning existing entries over appending new ones.
When updating this file, preserve this bar for all agents and keep entries concise.
