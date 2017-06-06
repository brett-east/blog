---
layout: post
title: 'The complexities of a/b testing'
excerpt_separator: <!--- more --->
comments: true
description: 'A guide to some of the complexities involved in a/b testing'
twitterdescription: 'The complexities of a/b testing - by Brett East'
tags: ['ab testing', 'user experience', 'web development', 'web design']
---

*This post was first appeared on [Medium](https://medium.com/@BrettEast/the-complexities-of-a-b-testing-6fdac53ecf7a)*

Recently we made some visual changes to our homepage and in one of our meetings the question came up “Let’s a/b test this”. As a huge supporter of a/b testing I was thrilled that it looked like we might actually get to do some on this project.<!--- more --->

![A ridiculous use case - ab testing a bug fix](/images/a-b-test.png){: .img-responsive style="margin: 0 auto 40px;"}

So naturally my first response was “Yes, that’s great” and my follow up question was “What’s our hypothesis?”, then my heart sank as I was met with blank expressions and it appeared this announcement to a/b test hadn’t been all that thought through.

As a result I was inspired to write this article about some of the complexities of a/b testing. While I’d say I’m a fan of a/b testing I’ve also seen firsthand how the incorrect implementation of tests can lead to poor decisions being made based on faulty results, I’ve also experienced a/b test overload where every piece of minutia is tested for weeks on end, or even worse — where, what are essentially, bug fixes are tested.
Not every change should be a/b tested as not every change lends itself to that kind of testing, but importantly, if you are going to a/b test, there are a few things you need to consider beforehand.

## What is our hypothesis?

As I mentioned in the intro, the lack of a hypothesis poses a real road block when wanting to get valuable data out of an a/b test. If you’ve made a change, you likely had a reason and a bit of an expectation on what effect that change will have to the site, that ‘expectation’ is your hypothesis, and it’s usually the driving force behind wanting to make a change in the first place.

From the design decision “Let’s remove the need for a compulsory phone number from our checkout process, I think it will increase checkouts” we can then get our hypothesis “Removing the phone number will increase sales” (I realise this example skims over some steps before coming to this design decision and the hypothesis doesn’t map 100% to the change, but it helps to bring out some of the considerations and mistakes mentioned in this article).

This is great, it gives us something we can measure and we know what we can expect, we’re expecting our sales to increase with users that are using the changed layout. This way we know what metric to measure and we’re not just looking at results at the end of the test trying to find differences between our two tests. Having a hypothesis before measuring a change is much better than trying to work out after the fact why a change occurred between two designs. For something like sales this might seem obvious, but it becomes important if we were making a change to static content site. Say we’re measuring a whole lot of metrics and user funnels, and we decide to move some content on the page and just ‘run’ an a/b test, then we blindly compare metrics like ‘time on page’, and ‘bounce rate’ — who knows what we might miss! After running the test, we’re now running around trying to see what’s changed and then scratching our heads as to why things may or may not have changed — not to say that we might not end up doing that anyway. It’s just much easier to track metrics that we think will change and then look at secondary metrics.

## Running your test

### Statistical significance

“Wow, that new button placement has a 20% increase in widget sales” — It’s funny how you can get the numbers to tell different stories.

Maybe one test did see an increase of 20% in widget sales, but if you only ran the test for a day, or ran it for 4 weeks, and only sold 5 widgets in the ‘a’ test and 6 in the ‘b’ test, then those results aren’t telling you too much. All too often I’ve seen an a/b test run without enough consideration into other factors, statistical significance being one of them and the effect on other parts of the site being another. You can look into [statistical significance here](https://www.optimizely.com/optimization-glossary/statistical-significance/), but most modern day a/b testing suites like [Optimizely](https://www.optimizely.com/) and [Optimal Workshop](http://optimalworkshop.com/) are more than equipped to report back on this information — but when running tests it helps to have a bit of an understanding as to why this is important.

Just because there is a 3% change in something doesn’t mean that it accounts for anything. A statistically significant result is one, that to a high degree of certainty means that your change impacted the metric that you’re measuring — not just that someone randomly happened to buy an extra few widgets.

### Splitting users

This step can often depend on what your testing and what your hypothesis might be. Initial reactions might be to split your audience 50/50, as ‘split testing’ or ‘a/b testing’ seems to imply. But what if you’re worried that the changes might have a negative effect, or what if you’re not sure the change is valid?

If you had a negative outcome you would then have to roll back the ‘b’ test for 50% of users. For a big change that would mean altering the user experience for half of your users, only to change it back again — this is potentially quite disruptive.

If you have enough users to get a statistically significant result in a few weeks, then I would suggest running the b test with 10% of users, there’s no need to test against 50% of users and most testing software will automatically adjust your a and b test results for an even comparison. Sometimes though, you might be testing a feature that isn’t used by many users and you need a bigger split in your audience to be able to get a timely result.

Another consideration when splitting users for a test is to consider ‘Existing-user bias’ — if you can, you should be running tests with new users only. This isn’t always feasible, and sometimes you can’t make this happen, but you need to be aware of it. Imagine you’ve simplified a ‘process flow’ on your website, and want to compare it with the existing, complicated process by measuring time on task and success rate. If you compare with existing users, your ‘a’ pool of testers will already be familiar with the process, and this might speed up their time on task in a way that is skewing your results. Using all new users helps to start the test with a level playing field.

### Length of test

How long are you going to run this test for and when are you going to make a decision either way? Like many things, you need to find the sweet spot in the middle, not enough time and your results may not account for how users interact with your site on weekends, too much time and you potentially block yourself from running other tests or making other changes to the site.

Many testing platforms will let you know how long a test is likely to take to have statistically significant results, and you can set them up to stop once they reach a result. I would say, if there’s no harm in doing so, then try and aim for between 2–4 weeks for your test length. Each test is different, but consider what events you might like to occur during your testing cycle, is there an email newsletter that is going out soon, how might that have an effect on things? If you see a behaviour pattern or cycle in your users (peaks and troughs in visits over weekdays and weekends is a common one), ask if you should make sure that your test includes a full ‘cycle’ of this behaviour.

### Comparing the right things

This is less of an a/b test thing and more of a “Let’s change something and then see how it compares with last month” thing. This occurs when people try to ‘retro fit’ a test to a design that they’ve rolled out, like trying to compare the performance of a button on a checkout flow by looking at the month’s sales before and after implementing the change. In this case you’re not comparing apples to apples, there are too many other variables at play, maybe this month is always better for sales, or maybe last month you ran a promotion. Most are aware that the entire point of an a/b test is so that you can run them in unison, but in the real world, you occasionally will have someone else ask how this compared with something outside of the test and it’s helpful to know that there are just so many variables involved.

## Tracking and running multiple tests

Make sure you track your tests, even in small teams there is the potential for tests to overlap one another. I’ve previously worked in a small teams where, devs and designers are running UI a/b tests while the marketing team is using another piece of software to run tests on content or landing pages — this has the potential to corrupt your data if you’re team is running tests that clash.

Tracking tests that are currently running, and having awareness of them is important, but as is historical tracking, particularly if you find some unexpected data in your tests. If in a year’s time, someone wants to make a change, it shouldn’t be up to one dev, who happened to be around for the last test, to say “I remember we tested that last year, and went with what we have now, but I can’t remember why” — documenting decisions not only saves time and confusion, but can help to dictate future decisions. If one particular design pattern tested well, then maybe we can use it as our default for future designs, and if we’ve documented it then we know why it works and where it might not work.
That’s not to say that just because you ran a test a year ago, you shouldn’t run it again, hypotheses can change, users might change and these can be valid reasons to recheck your tests — but if your hypothesis is the same, knowing that you’ve already run a test, can save duplicate work.

I spoke briefly there about tests clashing, and other than tracking tests, it’s worth mentioning that running multiple tests can skew your results or give you incorrect data, especially if your measuring a process or flow, and running multiple tests on different steps in the process.

## Choosing a winner

### Baselining

Awareness of the impacts of your changes is such a big part of where a/b testing can go wrong, especially if you miss when one change improves a part of the site to the detriment of another. Running a test that shows a change to the checkout improves mobile sales by 5% might seem like a clear cut winner, but if you were aware of the fact that desktop sales have dropped by 3% that decision might not be so clear cut, especially if three-quarters of all sales come from desktop.

This is where tracking baseline data for every test can help. While it’s not a ‘catch all’ for every piece of data, it can help with deciding on a winning test by showing you how major metrics have changed (if at all), across your site. Outlining some major metrics that you want to track can really help to show other areas that your change might have impacted. Continuing with our ecommerce example, you may want to check sales, abandoned carts, ‘added to cart’, newsletter signups — additionally you may need to check these across platforms or users, if you segment your user types (e.g. buyers/sellers).

Think of this as a sanity check for your a/b test outcomes, just ensuring that you haven’t broken anything, and always consider what may have broken and isn’t included in your baseline suite of metrics to check.

### A losing test doesn’t mean what you already have is the best option

If it turns out that the b test didn’t perform as expected, that doesn’t mean that ‘a’ is the best option, conversely, if your ‘b’ test wins, that doesn’t mean there isn’t a better option out there. Back to our early example of removing the phone number field on mobile checkout — we ran our tests and it turned out we did get more sales, but that we also had to spend more chasing up customers via email and our shipping partner was sometimes was unable to get in contact with customers when making deliveries, whereas they used to just call them. We decided that all things considered, it wasn’t worth removing the phone number field — but that doesn’t mean that keeping a compulsory phone number field is the correct answer either. Instead our hypothesis has changed, and we think that prompting users for an optional phone number is in fact better. In the end neither ‘a’ nor ‘b’ from our first test was what was best for the site, and it was in a third option — an optional phone number field, with a message “adding a phone number helps us to contact you should there be an issue delivering your order” — that performed best (who knows, there might be a better option yet).

---

As for our homepage a/b test, thankfully it just needed a little more discussion. We had originally decided to make the change based on user research we’d conducted, and were able to use that to come up with our hypothesis.
