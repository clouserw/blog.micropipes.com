---
layout: post
title: Mozilla Accounts password hashing upgrades
tags:
- Mozilla
- software
---

We've recently finished two significant changes to how Mozilla Accounts handles
password hashes which will improve security and increase flexibility around
changing emails.  The changes are entirely transparent to end-users and are
applied automatically when someone logs in.

## Randomizing Salts

If a system is going to store passwords, best practice is to hash the password
with a unique salt per row.  When accounts was first built we used an account's
email address as the unique salt for password hashing.  This saved a column in
the database and some bandwidth but overall I think was a poor idea.  It meant
[people couldn't re-use their email
addresses](https://github.com/mozilla/fxa/issues/14178) and it leaves <abbr
title="Personally Identifiable Information">PII</abbr> sitting around
unnecessarily.

Instead, a better idea is just to generate a random salt.  We've now
transitioned Mozilla Accounts to random salts.

## Increasing Key Stretching Iterations

Eight years ago [Ryan Kelly](https://www.rfk.id.au/) filed [bug
1320222](https://bugzilla.mozilla.org/show_bug.cgi?id=1320222) to review
Mozilla Accounts' client-side key stretching capabilities and sparked a
spirited conversation about iterations and the priority of the bug.  Overall,
this is routine maintenance - we expect any amount of stretching we do will
have to be revisited periodically due to hardware improving and the value we
choose is a compromise between security and time to login, particularly on
older hardware.

Since we were generating new hashes for the random salts already we took the
opportunity to increase our PBKDF2 iterations from 1000 to 650000 -- a number
we're seeing others in the industry using.  This means logging in with slower
hardware (like older mobile phones) may be noticeably slower.  Below is an
excerpt from the analysis we did showing a Macbook from 2007 will take an
additional ~3 seconds to log in:


| Key Stretch Iterations | Overhead on 2007 Macbook | Overhead on 2021 MacBook Pro M1 |
| ---------------------- | ------------------------ | ------------------------------- |
| 100,000                | 0.4800024 seconds        | 0.00000681 seconds              |
| 200,000                | 0.9581234 seconds        | 0.00000169 seconds              |
| 300,000                | 1.4539928 seconds        | 0.00000277 seconds              |
| 400,000                | 1.9337903 seconds        | 0.00029750 seconds              |
| 500,000                | 2.4146366 seconds        | 0.00079127 seconds              |
| 600,000                | 2.9482827 seconds        | 0.00112186 seconds              |
| 700,000                | 3.3960513 seconds        | 0.00117956 seconds              |
| 800,000                | 3.8675677 seconds        | 0.00117956 seconds              |
| 900,000                | 4.3614942 seconds        | 0.00141616 seconds              |



## Implementation

[Dan Schomburg](https://github.com/dschom) did the heavy lifting to make this a
smooth and successful project.  He built the v2 system alongside v1 so both
hashes are generated simultaneously and if the v2 exists the login system will
use that.  This lets us roll the feature out slowly and gives us control if we
need to disable it or roll back.

We tested the code for several months on our staging server before rolling it
out in production.  When we did enable it in production it was over the course
of several weeks via small percentages while we watched for unintended
side-effects and bug reports.

I'm pleased to say everything appers to be working smoothly.  As always, if you
notice any issues please [let us know](https://github.com/mozilla/fxa/issues).
