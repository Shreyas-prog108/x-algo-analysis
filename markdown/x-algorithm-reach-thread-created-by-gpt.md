# X Algorithm Reach Report - Copy/Paste Thread

**Created by GPT.**

Each numbered post is designed to stay under the normal 280-character X limit. Copy one block at a time.

---

## Post 1

I studied the open-source X For You algorithm repo.

The biggest takeaway:

X does not simply "boost viral posts."

It predicts which posts each viewer is likely to engage with, filters risky/repeated content, then ranks what survives.

1/16

---

## Post 2

The For You pipeline is roughly:

1. Understand the viewer
2. Retrieve candidate posts
3. Hydrate metadata
4. Filter ineligible content
5. Predict engagement
6. Rank, dedupe, and blend the feed

Reach is multi-stage. Failing any stage limits distribution.

2/16

---

## Post 3

The algorithm favors predicted positive actions:

- likes
- replies
- reposts
- shares
- clicks
- profile clicks
- video quality views
- dwell time
- quotes
- follows

So optimize for real response, not vanity likes alone.

3/16

---

## Post 4

Negative signals matter a lot.

The model also predicts:

- not interested
- mute
- block
- report
- not dwelled

If your content looks like something a viewer would hide, skip, mute, or report, it can be pushed down even if it gets some engagement.

4/16

---

## Post 5

Retrieval comes before ranking.

Your post first has to enter a candidate pool:

- in-network: people who follow you
- out-of-network: people whose history/topics match your content

This is why niche clarity matters so much.

5/16

---

## Post 6

Out-of-network reach appears structurally harder than in-network reach.

The repo applies an OON multiplier in ranking.

Translation:

Followers are not just an audience. They are also a distribution base that can seed wider discovery.

6/16

---

## Post 7

Freshness matters.

The code has age filtering, recent post stores, and post-age features in the model.

Old content can lose eligibility or score context.

Post when your audience is active, and make the first engagement window count.

7/16

---

## Post 8

The system likes topic consistency.

Phoenix retrieval uses user history and content/author embeddings.
Topic sources use followed or inferred topics.

If you post about 10 unrelated things, the model has a harder time knowing who should see you.

8/16

---

## Post 9

Dwell is a real signal path.

The repo models dwell and continuous dwell-time.

This means structure matters:

- strong first line
- readable formatting
- useful payoff
- good media
- no empty bait

Make people stay because the post is worth staying for.

9/16

---

## Post 10

Video can help only when it creates real watch quality.

The repo has explicit video quality view paths and duration eligibility checks.

So filler video is not the point.

The goal is watchable, relevant, high-retention video.

10/16

---

## Post 11

Do not spam replies.

The repo includes Grox paths for reply spam detection and reply ranking.

High-signal replies to relevant conversations can help.

Copy-paste replies, tag bait, and hijacking unrelated large accounts can hurt.

11/16

---

## Post 12

Duplicates and repetition get controlled.

The code dedupes:

- same post IDs
- retweets of the same content
- previously seen/served posts
- repeated conversation branches

Do not flood the feed with near-identical posts.

12/16

---

## Post 13

Author diversity exists.

Repeated posts from the same author can be attenuated inside a single feed response.

Posting more is not always better.

Posting distinct, high-signal ideas consistently is better than flooding.

13/16

---

## Post 14

Safety and policy risk can kill reach after ranking.

The repo includes visibility filtering, safety labels, brand-safety tiers, spam checks, NSFW/gore/violence labels, and do-not-amplify style labels.

If broad reach is the goal, stay policy-clean.

14/16

---

## Post 15

Practical playbook:

1. Pick a clear niche
2. Earn early engagement from the right followers
3. Write for replies, reposts, dwell, follows
4. Avoid mute/block/report triggers
5. Stay fresh and original
6. Use media only when it improves retention

15/16

---

## Post 16

Final takeaway:

X reach is not one hack.

It is:

retrieval fit + positive predicted engagement + low negative feedback + freshness + safety + diversity.

If you want reach, become highly relevant to a specific audience and consistently make posts they won't want to skip.

16/16

