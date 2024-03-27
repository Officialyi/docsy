---
title: Lifecycle Campaigns
description: The following is a generalized replication of a previous lifecycle campaign for a software product.
weight: 3
---

### Scenario
The growth team was entrusted with analyzing opportunities for customer acquisition and conversion for a subscription based software product. The product is well utilized by the community and has a strong reputation and user base. However, as a backbone of the company's products, data regarding product "S" (as we'll refer to it), was primarily anedoctal. The Product Manager and Product Marketing Mananger have concluded the ICPs of the product based on conversations with the community over many years. Growth was able to identify digital information and user journeys as an opportunity to enhance our understanding of customers and their needs. Here are the steps taken in order to build out a comprehensive user journey that enables a PLG motion for Product S.

### MVP
Although Product S is well established in the market, the sales model for S would be transitioning from a Perpetual product to a Subscription based product. Coupled with the maturity of data available for product S, the team decided to start with a foundational assessment of Product S to determine its categories of minimal viability and to inventory what touchpoints were existant for current users. 

#### PLG Readiness Assessment
Starting off with a PLG Readiness Assessment, Product S is analyzed according to a few factors.
* Define existing product milestones. 
* User assessment - Define attributes of active users. 
* Determine Engagement Indicators.
* Create nudge nurture flows to lead users along the key milestones. 
* Define free-to-paid signals. 

As we assess the product itself, we take inventory on existing resources and technical content for users. From an information perspective, we asessed available data across exisiting assets to identify where gaps may exist in the user journey. This involves demand generation, web assets, product telemetry data, commercial data, and campaigns. Where gaps may exist, we start to inventory and lay the foundation for proper attribution and tracking through a unified CID. 

We identified that Product S contains a plethora of disjoined information (an amalgamation of old campaigns) without a defined user journey that brought a user from awareness → consideration → conversion → retention. 

#### Establishing a Customer Journey
The Current Acquisition model: A Trial is in place for users to try the product with no awareness around the quality and quantity of downloads. As this product is well known, the product is also merchandised through an ecommerce instance with paid media leading to a LP that merchandises the product, separate of the .com PDP.

From the initial analysis on engagement indicators and product milestones that may lead to a conversion, we set the organic (not including inorganic non-brand keyword campaigns) flow to integrate as follows:

Product Page → Free Trial Download → Installation + Onboarding → In product nudges → Product evaluation → Purchase → Nurtures for inactivity threshold → Retention through perpetual subscription.

| Asset | Notes  | 
|-------------------|-----------------|
| Product Page   | The product page is well detailed with various use cases and product features. For additional information, more in depth guides are available and so are technical resources. Users are prompted to purchase the product or trial the product as a primary CTA. However, a consistent guide is not available and the product page is primarily catered towards merchandising. | 
| Trial | Users are able to download a free 30 day trail immediately from page. Product is ungated with trial lifespan measured by internal machine clock. Users are not required to log in or provide information to use the product. Telemetry Data for product utilization and trial abandonment is limited. | 
| Onboarding Nurtures | User Generated Content is available as installation guides. Technical product guides exist in separate resource pages. However, formal onboarding documentation and nurture campaigns are non-existent. | 
| In Product Nudges | In product nudges are timed to note the remaining duration of a users trial. However, specific nudges to convert are not made and there is no SRC tracking in place to indicate a user's source destination is a trial. Therefore, there is a gap in information with regards to purchases and attribution. | 
| Commercial Product Page | Product is transacted through Magento/Digital River payments. Users have access to their licenses through the internal CDP post purchase. The purchase flow for product pages are well laid out, but a gap exists in attribution among purchases. | 
| Email Campaigns | Emails are sent sporadically and primarily as promotions to announce new features and promotional pricing. | 
| Ongoing Retention | No nurture campaigns exist to support user communities. | 

#### Always On Program

##### 1.Identifying Known Users
The area with the highest business impact would start with improving measurement for user assessment. Quantitative demographic information could be collected through implementation of a form prior to downloading the asset. Although its noted that [gating B2B Assets is a common industry practice](https://blog.scoop.it/2014/08/14/b2b-content-marketing-stats/), the PM had a few reservations. The product itself is created as a low barrier into the company's ecosystem of products. Among the known development community, additions of gates may not yield a positive response. Furthermore, the trial download is often tied to direct source APIs. Therefore we decided to test the implementation of the gate while retaining the download link so as to not impact APIs.

**Testing a form**

Our first step in creating a test was to align on the KPIs. Our primary KPI to monitor would be the total downloads of the trial. The intent would be to have a baseline for how many users are downloading the trial and how many users, when faced with a gated Landing Page to download the trial asset would bounce. While setting up the infrastructure for the test, we worked with the analytics team to create a report on engagement with the trial page. We noted that the page itself drew +400K visits/month and after establishing tracking on the download links, a projected ~320K trial downloads. With a 50/50 test projected to run for 2 weeks here's some key notes that determined our future direction. 

* There was a drop of ~40% in downloads for the Variant.
* 60% of information collected from the form were actionable leads.
* A concrete ICP was determined with a percentage mix of customer industry attributes. 

A 40% drop in downloads is non-marginal and requires additional analysis. We paused the test after the projected volume to reach significance. FullStory (DXI) sessions were monitored to identify opportunities to optimize the experience among users. Ideas included an embedded form, moving the test up funnel and directing users to the asset landing page, and a few others. 

As the product is primarily merchandised through the ecommerce platform, a direct correlation to trial downloads and purchases could be made. From the period the test ran and was concluded, a 30/60/90 day period was monitored for the product line. It was concluded that although clicks asset downloads dropped 40% in the test, purchases of the product were unaffected. When filtered for repeat downloads and robots, the gate provided minimal impact into the merchandising of the product. Considering the benefit of MQLs generated and nurtures that could be established, it was determined alongside the business stakeholders to <b>implement the gated asset.</b> This being said, had downloads of the assets been affected dramatically and revenue been impacted in correlation, this experience would be considered unsucessful and we would determine other strategies further down funnel to identify users.

**Nurturing Prospects**

While indentifying users, we're able to collect Job Title from our users. This allows us to bucket our users by affinity and potential use cases. Working with the technical marketing team, assets were collected and generated into a cohesive installation guide and series of onboarding documents. 

Through emails collected and the connected Marketo form, we created an automated onboarding email with the installation and 'jump start' instructions. After bucketing our users by their attribute, we were able to create use-case specific nurture campaigns. 

**In Trial Nudges**

Through the trial we were able to identify key product milestones. Through these key product milestones, we're able to create nurtures and in product guides to encourage further utilization of the products. Toward the end of the trial period, we're able to set time based nudges to purchase the product with CID tracking from the trial enabled. 

**Further Optimizations**

With key product milestones established, we were able to set baseline metrics and continue optimization of copy, positioning, timing, and other factors to increase conversion rate through each step. 

In summary, the steps to creating the Always On Programs for user growth:

* Identify known users through a gated asset. (We tested this to ensure that there was no significant impact on our bottom line. 40% drop in downloads, but there was no impact 30/60/90 days on our purchases.) 
* Establish onboarding for users through marketo drip campaigns
* Set triggers for key product milestones and nudges to encourage future utilization
* Time based nudge with CID tracking to identify trial based purchases.
* Create value attribution on the trial and optimize the CVR for ongoing testing and optimization.

### Integration of Inorganic Strategy

While the primary focus was on establishing a user journey among organic assets, an extension of the user journey would be through creating consistency in our demand generation strategy and non-owned media. Some outlets include: 
* Working with partners to trial products and create awareness among target audience watering holes. 
* Redesign landing pages based on keyword intent. 

Those in the consideration stage may be directed to a product feature comparison table and use cases to encourage purchase. 
Those in the awareness stage may be directed to the main PDP + encouraged to trial the product. 

