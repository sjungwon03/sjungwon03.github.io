---
layout: page
title: About
lang: en
alt_url: /ko/about/
lede: I work on backend systems and cloud infrastructure.
description: Jungwon Son — backend and cloud infrastructure engineer. 2 years 3 months of experience.
---

For two years and three months I owned the backend of a government-funded vocational training LMS. In that domain, course progress is the basis for tuition reimbursement and instructor settlement figures are the basis for actual payroll. That shaped a habit: before asking whether a feature works, ask whether the numbers are right.

I handled deployment and operations alongside development. I watched learners lose their viewing progress every time we shipped, so I treat zero-downtime deployment as a data-integrity requirement rather than a nice-to-have.

## How I work

- **I assume a full rewrite is off the table.** Most of the services I touched were already running and already earning. So half the job was deciding where to cut first. I lean on the same sequence repeatedly: pin down the pattern in a rehearsal environment, then apply it to production in one pass.
- **I roll things back when the premise turns out to be wrong.** I introduced refresh-token rotation, then found it only holds if there are no concurrent requests — two browser tabs break it — and removed it. In a side project I cut the server-side crawler after concluding that a scheduled collector is the most expensive part to run alone.
- **I write down the reasoning and the alternatives I rejected.** Including the steps I failed to automate, in order. The point is that whoever comes next doesn't fall into the same hole.
- **I put tests where failure is silent.** Bugs that throw get found anyway. What's dangerous is a value that quietly goes wrong — an enum and an external code table drifting apart until a recommendation score silently reads zero.

## Now

After leaving, I earned the AWS Solutions Architect – Associate and HashiCorp Terraform Associate certifications and completed a cloud infrastructure engineering program. As infrastructure lead on the final project, I designed and built a hybrid environment connecting an on-premise Kubernetes cluster across four physical servers to AWS.

I also ship and operate two mobile apps as a solo developer — planning, server-side purchase verification, store releases, all of it. Doing every part alone keeps testing the same question: what shape of system can one person actually carry?

More detail is on the [résumé]({{ '/resume/' | relative_url }}) page.

## Contact

- Email — [sjungwon03@gmail.com](mailto:sjungwon03@gmail.com)
- GitHub — [github.com/sjungwon03](https://github.com/sjungwon03)
