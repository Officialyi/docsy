---
title: Decision Making Optimization Resources
description: Here are a few resources regarding testing tools and the decision making optimization framework.
# categories: [testing, experimentation]
weight: 5
---

A few resources to consider within Decision Making Optimization: 
DMO: draw insights and learnings that lead to better decision making

| Use Case | Platforms  | Notes | 
|-------------------|-----------------|------|
| Web Experimentation   | [Adobe Target](https://experienceleague.adobe.com/en/docs/target/using/activities/abtest/test-ab) </br>[Optimizely](https://www.optimizely.com/contentassets/e4f428c83d04499b985bd8a44221c121/test-and-learn.pdf/)</br> [VWO](https://help.vwo.com/hc/en-us/articles/360019419534-What-is-VWO-Experience-Optimization-Platform) |  |
| Email            | Marketo & many other email automation platforms | Testing is integral within many email campaigns. The basic structure is done through creating different flows and conditions such as which category a user subscribed to. Generally A/B tests in Email are split with 20/80, meaning that 20% of traffic is split for a period of time and of the 20%, the best experience is then projected to the rest of the audience (80%). This time delay should be kept in mind if a test is to be implemented on content. |
| Search Marketing | Google Optimize - Experiments and Variants (sunsetted. See above on Web Resources) | Optimize has some granular targeting options that enable customized experiences </br> </br>To my understanding, Google ads responsive search ads natively cycle and optimize headlines and ad copy to propose the ideal copy for users; however, this doesn't isolate specifics and learnings are minimal though performance can be increased. See notes on General Framework for Tests. |
| Social Media | Built in: [Facebook Ad Manager](https://www.facebookblueprint.com/student/path/219763-how-conversion-ab-and-brand-lift-tests-help-your-business-decisions) Aggregate: [Sprout Social](https://sproutsocial.com/insights/testing-on-social-media/)  | A/B v. Split Testing: A/B is where you would isolate one specific variable to identify its impact on your audience. Split testing can be a split in traffic across 2 very different experiences. <br></br> Best Practices in social:</br> - Set a specific goal to best identify audience impact (i.e. timing, message, partners, platforms).</br> - Aim to learn about your audience and their perception, rather than which provides higher numbers. |
| Programmatic Display [[how to]](https://martech.org/how-to-test-your-programmatic-creatives-like-a-pro/) | DSPs | Metrics to isolate and improve: </br> - ID Providers, isolate builders, auction timeouts, server/client side demand partners, audience segmentation, bid adjustment, ad frequency, creatives, placement, time of day, devices, ad formats, channels.  |

Experimentation Case Study on Testing Wrapper Solutions [link](https://pubmatic.com/wp-content/uploads/2020/11/9GAG-CaseStudy.pdf)

General Framework for a good test
* Identify an objective [generally] your KPI
* While you can monitor multiple metrics for performance, I'd recommend using the next direct step as your experiment indicator. 

I.e. If I were to run a search campaign, theres multiple factors (campaign targeting, ad groups, keywords, ad copy, landing pages, etc). If I decide to test different ad groups across the same ad copy and similar headlines/descriptions (i.e. a STAG v. SKAG), I'll focus on how that influences ad opens. I'd like to have an idea on ad copy and conversions, but that's a step further than what would provide me actionable insight without speculation. Once I identify the keyword groups that best align to that specific campaign audience, then I can drill down into optimizing headlines (not descriptions). Once I find the perfect combination of ad copy, I can move to testing landing page variants to increase conversion. Through each of these, I now have a better understanding of this audience and how we can message to them best through other campaigns as well (smile). 


#### Tools & Services

[A/B Testing Calculator](https://cxl.com/ab-test-calculator/)

Concurrent tests? [Interaction Effect Calculator](https://www.lukasvermeer.nl/xy/)