---
title: "AB Testing: Splitting the Data"
description: "A quick method to split data in different buckets for the purpose of AB Testing"
pubDate: "June 17 2022"
heroImage: "/splitting_the_data/buckets.webp"
badge: "AB Testing"
tags: ["AB Testing", "Python"]
---
### The problem? I can AB test, but I need to split my data first!

AB testing is probably one of the most iconic and intuitive uses of data to drive business decisions. There are tons of resources to learn how to AB test, usually, with pre-labelled “A” and “B” data. But, when I wanted to implement an AB test in real life, I hit a wall:

How do we decide which users to show an “A” version or a “B” version while they navigate the website?

How can we split users in a way that is random?

How can we split users so that they are shown the same version of the AB test each different time they log on?

How can users be split to enable us performing a ABC test, and continue testing new versions?

---

### The solution? Buckets and hashes!

Not the physical ones, but the digital ones. Let’s think about it, if we have 2 groups — buckets — of customers, we can divide them 50/50 pretty easily. We could simply label those buckets A and B, but we could also create more buckets, allowing us to divide in different proportions, add a C to the test, or even perform new tests very easily. By dividing customers in say, 24 buckets, we can divide them in 2 groups, 3 groups, 4 groups, etc.

We can also keep a few buckets aside to see the long term effect of compounding tests.

We are looking for a way to convert our user unique identifier (user id) from a string into an integer between 1 and 24 (or between 0 and 23).

If the user id was already an integer, it would be simple to use modulus operation (base 24) to “map” users into 24 different groups. Assuming that a user id is random, the result would also be random. This would also ensure that a user would always be assigned the same bucket every time they are coming on the website.

One way to convert strings to integer, is to use hashes. On a fairly high level, hashes are… functions. They take an input and map them onto another dimension. They are also deterministic, so they will keep our results consistent. For all intents and purposes for what we are doing, they are also “random” (there should not be a pattern in the resulting hashes). Which is a good news, even if the original user id’s had some sort of patterns in them!

In python, one can then take their user id string and:
1. Encode it using utf-8,
2. Use an hash function on the result (eg. Sha1),
3. Then, represent the encoded data into bytes (eg using .hexdigest() ),
4. Transform the byte representation to an integer one (using int()),
5. Finally, use a modulus operation to map the integer into the one of 24 buckets (or however many you want) (using %).

It would look like this (using the sha1 hash function):

`int(hashlib.sha1(user_id.encode("utf-8")).hexdigest(), 16) % 24
`

---

### Final Words

That’s it! Now, each user will be represented by a random integer from 0 to 23. One can easily build list of buckets and conditional statements to show the desired output to each customer.

These are also computed fast, so they allow to split users on the fly, while consistently showing the same users the same versions.

Enjoy your AB testing!