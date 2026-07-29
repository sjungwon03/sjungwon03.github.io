---
title: Deploys that don't corrupt data
description: Learners lost their viewing progress on every deploy. Notes on treating that as an integrity requirement rather than a feature.
tags: [backend, infrastructure, zero-downtime]
lang: en
alt_url: /ko/posts/2026/07/30/deploys-that-do-not-corrupt-data/
---

While I owned the backend of a government-funded vocational training LMS, every deployment dropped the connections of learners who were mid-lecture — and the progress they'd accumulated at that moment vanished with them.

At first I read this as a UX problem. Playback stutters for a second; refresh and carry on. But in this service, **course progress is the basis for government tuition reimbursement.** When progress disappears, it isn't an inconvenience. The settlement is wrong.

## Naming the problem differently

The same symptom leads somewhere different depending on what you call it.

- "Deploying interrupts playback" → improve the reconnection logic
- "Deploying destroys data" → guarantee persistence at the moment of shutdown

Once I started using the second phrasing, the work became obvious. No amount of reconnection polish brings back progress that's already gone.

## There wasn't one exit path

Pulling tracking out of the monolith into its own service, I counted every way a session ends.

1. The user stops playback
2. The connection drops
3. A duplicate login occurs
4. **The server goes down**

The first three still have a live socket object. The fourth doesn't. But the termination handler was a single function. Make the socket an optional field and you have to read the code to know which paths actually have one — and when you get it wrong, it fails at runtime.

I split it into a discriminated union keyed on the reason for termination, so code that would touch a socket on the path where none exists is caught at compile time. The type does the documenting.

## Persist everyone on the termination signal

On the termination signal, the service walks the entire session cache, persists progress for everyone currently watching, then exits. There's a timeout, and it's paired with the process manager's shutdown grace period and zero-downtime restart.

This bought one constraint. The session cache is in-memory, so **the service can only run as a single instance.** Rather than hide that, I wrote it down along with the reason. Whoever next tries to raise the instance count should be able to find out why they can't.

Later, building a real-time feature in a side project, I attached a Redis adapter from day one — while the user count was still tiny — so that scaling out wouldn't mean revisiting the architecture. I wouldn't have made that call without having lived with the earlier constraint.

## The same principle on the deploy side

Having hit this in the application, I started asking the same question of the deployment pipeline: **if this step fails, what's left?**

Implementing blue/green on a single EC2 instance without adding hardware, I ordered it like this:

1. Deploy to the idle port
2. Health check five times, ten seconds apart
3. Switch the proxy **only** on success
4. On failure, don't switch — roll back

A process being up and a service being ready are different things. Because step 3 is conditional, a version that fails to come up never takes traffic; the old one keeps serving. The point of the structure is that a failed deploy isn't an outage.

## What stuck

When I look at infrastructure now, a question arrives before any availability figure does.

> When this dies, what disappears with it?

Zero-downtime deployment turned out not to be a line on a feature list. It was the answer to that question.
