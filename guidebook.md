# Introduction

## Scenario

The customer, SN Suites, is a luxury regional hotel chain with significant presence in Las Vegas. In 2019, they went through a digital transformation to modernize their IT systems and deployed ServiceNow across multiple areas including general IT Service Management and Hotel Customer Service Management. In addition, they use ServiceNow for Restaurant Workflow Management and created a self-service portal for ordering room service. It has been deployed for the last 6 months to mixed guest feedback about the experience. While many guests appreciate being able to order from the comfort of their room without needing to talk on the phone, some common complaints include confusion around dietary restrictions, difficulty finding and submitting the desired meal choices, and a lack of brand cohesion between the portal and the SN Suites' public facing site.

As a result, SN Suites is reconsidering the renewal of their subscription for their custom Restaurant Workflow Management application. They say that without a plan to improve their Portal it is not providing enough value to justify their continued investment. The account team is looking to you to determine and implement tweaks to the Portal to provide SN Suite guests a better experience and therefore alleviate the customer's concerns.

## Goal

The goal of this lab is the reinforce the Best Practices and Key Capabilities from the presentation today. In it you will leverage key ServiceNow capabilities to design a portal that is contextual to the guest; with relevant content and catalog items, visually different; with the application of a simple or complex theme change, and representative of a portal that helps a customer's journey to self-service

### Getting Started - Log on to Your Training Instance

1. Navigate to the unique instance URL provided to you.
1. Log in with the provided credentials
1. Change your password to something memorable just in case you get logged out of your instance.

# Exercise 1 - Understanding the Current State

## Goal

This lab will help you get a better understanding of the current state of the portal. To do this, the platform provides built-in capabilities but it is also useful to get direct feedback from guests.

## 1.1 - Usage Overview

The first place to look is **Usage Overview** to gather quantitative data about guests behaviors on the portal. Here you can see the most popular *search terms*, *pages*, *knowledge article*, and more...

1. Log in to your instance
1. In the App Navigator locate **Service Portal \> Usage Overview**
1. Review the Service Portal Search Terms

### Think About

> What are the most popular search terms?
>
> Are guests typing in terms that do not correlate to data in the catalog?
>
> Are there popular search terms that just do not make sense?
>
> Not all search terms are visible in the bar chart. The table that stores these is `sp_log`. What other terms are guests using?

## 1.2 - Survey Results

When the portal was deployed, the implementation team created a basic survey to capture guest sentiment about the portal. It looks like a number of guests have filled out the survey, so this is a good place to check for their thoughts on the portal.

1. Navigate to **Surveys \> View Surveys**
1. Open the record *Service Portal Improvement Survey*
1. Click **View Scorecard**

### Think About

> What are the weakest attributes of the portal based on the survey data?
>
> Are there any interesting comments that can inform your path forward?

**Note:** A survey like this is recommended as a way for customers to assess the current state of their portal. You can download the [update set](files/survey.xml) with the survey.

## 1.3 - Usability Study

Another way to collect qualitative feedback is by observing how someone interacts with the current portal. For this lab, the group will be broken up into pairs; one person will be the Facilitator and the other the Participant.

![usability study](images/usabilityTest.png)

1. Pair off with another lab participant
1. Introduce yourselves - Name, Role, Location
1. Whoever traveled the **FURTHEST** to get here will be the *Participant*. The other will play the role of *Facilitator*
1. The facilitator's job is to observe how the participant completes the task(s) assigned.
1. The task is "Please go to the Room Service Portal and order a cheeseburger, cooked how you like with your favorite toppings."
1. The participant's job is to try and complete the assigned task(s).
1. The facilitator should take notes as they observe how the tasks are completed.

### Think About

> Was the participant able to easily complete the tasks presented to them?
>
> If not, where did they encounter issues?
>
> How could the platform be leveraged to reduce the friction the participant encountered?

### Resources

- [Usability Study Tips and Sample Questions](https://sc.service-now.com/snideation?page=3&direct=true&title=Gather%20guest%20Feedback&sys_id=b5dd22bfdbb9db803eb8f4bbaf96194f)

- [Recent Usability Study Report](https://ts20killerportal.service-now.com/kb_view.do?sysparm_article=KB0010002)

# Exercise 2 - Information Finds the User

## Goal

This lab will leverage a set of capabilities to effectively bring information to the guest. By using what the platform knows about the guest, the Portal can present information that is uniquely relevant to them. These are just a few ways this information can be used; when working with customers, think about how they might leverage these capabilities to create a tailored experience.

## 2.1 - Vegetarians Don't Eat Meat - Use User Criteria to filter their Menu

One of the things that stood out in the usability study was that guests with certain dietary restrictions, had a hard time finding menu items that met their dietary needs. Let’s use User Criteria to filter what these guests see.

1. Open the User Profile for *Dosie Do* and review the Groups they belong to. One of their groups should be **Vegetarians**
1. Use the Application Switcher to switch to the **TS20 Killer Portal** application.
1. Now, navigate to **Service Catalog \> Maintain Items** and open the Hamburger item.
1. Select an item and scroll down the the *Related Lists* and select **Not Available For**.
![Not Available For selected](images/notAvailableFor.png)
1. Click **Edit** and add the group *Vegetarian Guests* from the slush bucket.
1. Save the changes
1. Repeat for catalog items *Juicy Lucy* and *New York Strip*

### Let's test this

1. Impersonate *Dosie Do*
1. Go to the portal and make sure *Dosie Do* does not see the meat-based catalog items.

**Note** There is a link to the portal in the Application Navigator under the Room Service module.

### **CHALLENGE**

For KB articles, guest Criteria only applies at the Category level. How might one hide all meat recipes from a vegetarian guest?

## 2.2 Vegetarians also like to hear news about new menu offerings

The market of plant-based alternatives to beef and chicken continues to expand, and with that the restaurant's menu is constantly evolving. How can the platform be used to target vegetarians with announcements about menu updates?

1. Switch back to the admin user.
1. Navigate to **Content Delivery \> Portal Content**.
1. Click **New**
1. Fill out the form

    Field | Value
    ------|-------
    **Title** | New Impossible Burgers
    **Content Type** | Styled Content
    **Heading text** | Introducing new Impossible Burgers to the menu!
    **Rich Text** | This month, we are excited to introduce a new addition to our Vegetarian Menu, the Impossible Burger. All of our mouth-watering burger specials can now be had with the delicious plant-based patty. In addition, we are introducing 2 new burgers that feature the Impossible Burger; the Predictably Impossible and the Impossibly Sweet Burgers. Enjoy the savory juiciness in our new offerings.

1. *Save the content*
1. Under *Schedule Content*, click **New**
1. Fill out the form

    Field | Value
    ------|-------
    **Page** | rs_index
    **Widget Instance** | Latest News
    **Availability start date** | January 22, 2020 08:00
    **Availability end date** | January 30, 2020 08:00

1. Unlock the *Audience* slush bucket
1. Click on the magnifying glass
1. Create a new Audience
1. Fill out the form

    Field | Value
    ------|-------
    **Name** | Vegetarian Guests
    **Audience type** | User Criteria
    **User Criteria** | Vegetarian Guests

1. **Submit** the new record
1. **Submit** the Schedule Content form
1. Impersonate *Dosie Doe* and navigate to the `/room_service` portal.
1. You should see the content in the *Latest News* widget

## 2.3 When they read about the Room Service policies, they want information relevant to them - Knowledge Blocks

Guests are complaining that they are seeing too much non-pertinent information within Knowledge articles. To wrap up this lab, use *Knowledge Blocks* to provide dynamic information based on the guest's profile.

1. Go to **Knowledge \> Articles \> All** in the Application Navigator
1. Open the article: **Impossible Meat Ingredient Information**
   > Notice there is content for EVERY allergy issue possible in their recipe. Instead, it would be better to only show guests information related to their specific allergies
1. Remove the content between the Allergy Info heading and the Nutrition Facts heading and save your article
1. Navigate to **Knowledge \> Knowledge Blocks \> Create new Block** in the Application Navigator
1. Fill out the the form per the table below

    Field | Value
    ------|-------
    **Knowledge Base** | Room Service
    **Can Read** | Guests with Soy Allergies
    **Short Description** | Soy Allergen Info
    **Article Body** | The Impossible Burger contains Soy.

1. Save and Publish the block
1. Repeat steps 4-6, changing the Can Read, Short Description, and Article Body fields per the table below

    Knowledge Base | Can Read | Short Description | Article Body
    ------- |------- | ------------- | --------
    Room Service |Guests with Coconut Oil Allergy | Coconut Oil Allergen Info | The Impossible Burger contains Coconut Oil (the FDA classifies coconuts as tree nuts for food labelling purposes, but refined coconut oil is not considered an allergen).
    Room Service | Guests with Potato Allergy | Potato Allergen Info | The Impossible Burger also contains potato protein. If you have an allergy to either raw or cooked potatoes, you should not consume the Impossible Burger.

1. Return to the Knowledge Article edited earlier **“Impossible Meat Ingredient Information”**
1. Click the **Add Blocks** UI Action
1. In the Add Blocks panel search for “soy”
1. Put your cursor on a newline after the “Allergy Info” heading
1. Click **Insert** on the Soy block you created
1. Repeat steps 12-13 for “coconut oil” and “potato”
1. After the last Knowledge Block, add the following content
    >Impossible Burgers do not contain dairy, eggs, fish, peanuts, shellfish, or wheat, and it’s safe for those with alpha-gal syndrome.
1. Click **Publish**
1. Underneath “Related Links” click **Preview Article with Blocks**
1. Change the View As to *Dosie Do* (vegetarian with no allergies) and *Susie Su* (vegetarian with potato allergy) to how the article changes. Only Susie should see one of the Knowledge Blocks we just created.

# Exercise 3 - Consumers != Providers

## Goal

Often times, when creating content for a portal, customers create it from the perspective of the fulfiller and do not recognize that the guest that will consume the content has a different level of knowledge, set of expectations and experiences as it relates to the issue. This often means that catalog items are confusing and guests opt to call for help instead of self serving. This lab will take what was learned from the usability study and try and improve site content.

## 3.1 - This form has so many options, I would rather go hungry. - Form Design

In the usability studies, participants struggled to complete their orders. They specifically pointed out that the forms felt really long and confusing for each menu item they wanted to add. How could the form inputs be improved to make it more approachable for guests?

1. Open the **Hamburger** catalog item from the **Service Catalog \> Maintain Items** Application Module
1. Delete all the Toppings checkbox variables from the item.
1. Delete the Toppings label variable.
1. Create a new variable and set it up as follows

    Field | Value
    ------|-------
    **Type** | List Collector
    **Order** | 100
    **Question** | What toppings would you like?
    **Name** | *autofill*

1. Switch to the *Type Specifications* tab
1. Set the *List Table* field to *x_snc_ts20_portal_toppings*
1. Set the *Reference Qualifier* to `type=other`
1. Click **Submit**

Guests also have very specific preferences for their cheese, so the next step is to separate that from the rest of the toppings

1. Create a new variable and set it up as follows

    Field | Value
    ------|-------
    **Type** | List Collector
    **Order** | 200
    **Question** | What type of cheese would you like?
    **Name** | *autofill*

1. Switch to the *Type Specifications* tab
1. Set the *List Table* field to *x_snc_ts20_portal_toppings*
1. Set the *Reference Qualifier* to `type=cheese`
1. Click **Submit**

Guests also complain about selecting the temperature of their burgers, so the last step is to improve that experience

1. Open the **Internal Temperature** variable
1. Update the form according to the table

    Field | Value
    ------|-------
    **Type** | Select Box
    **Question** | How would you like your meat cooked?

1. **Save** the Record
1. Scroll down to the *Question Choices*
1. Create the following choices
  
   Text | Value | Order
   ----- | ----- | ----
   Rare | 120 | 100
   Medium Rare | 135 | 200
   Medium | 140 | 300
   Medium Well | 155 | 400
   Well Done | 160 | 500

1. Click **Update**

## 3.2 - All I want is a sandwich, but now you are asking me to be a cook? - Variable Sets

During the usability study, participants complained that the same questions were asked in many different ways and the order of options was never consistent. This caused them to make mistakes in filling out the forms. *Variable Sets* help to ensure consistency across similar catalog items.

1. Reopen the **Hamburger** catalog item.
1. Switch to the *Variable Sets* related list.
1. Click **New**.
1. Click **Single-Row Variable Set**.
1. Set the **Title** to *Common Beef Items*.
1. Click **Submit**.
1. Switch to the *Variables* related list.
1. Select the *How would you like your meat cooked?* variable.
1. Clear out the *Catalog Item* field.
1. Hit tab to leave the field.
1. A new field will show up, titled *Variable Set*.

    ![Move a variable into a variable set](images/variableToVariableSet.gif)

1. Select **Common Beef Items** reference.
1. Click **Update**.
1. Repeat Steps 8-13 for the *What toppings would you like?* and *What type of cheese would you like?* variables.
1. Add the *Common Beef Items* variable set to the **Philly Cheese Steak** catalog item.
1. Go to the `/room_service` on your instance and open one of the catalog items that was just edited. Does it have the new variables?

>**Take Away** How did the changes make the experience easier for guests to put in their order?

# Exercise 4 - Don't Follow the Org Chart

## Goal

Similar to the previous lab, customers do not always know how to communicate to their guests. They use internal naming conventions, acronyms, and organize content based on their org chat. That does not always map to how guests talk about the services and articles a portal provides. This lab will explore how to learn about how guests organize information and then use that insight to improve the catalog.

## 4.1 - Discussion of Card Sort

During the presentation, everyone participated in an *Open Card Sort*. In small groups, discuss how you might interpret the results to update your catalog. The [results](https://www.optimalworkshop.com/optimalsort/84e88w66/ts2020/shared-results/fgf7281h770mq5lbup755d4147873q2a). are available online. <!-- TODO Update the URL -->

1. Break off into groups of 3-4, with the people sitting around you.
1. Pull up the [results](https://www.optimalworkshop.com/optimalsort/84e88w66/ts2020/shared-results/fgf7281h770mq5lbup755d4147873q2a) on someone's laptop <!-- TODO Update the URL -->
1. Navigate to the Analysis>Categories tab to see the results
1. Discuss with your group how to reorganize the menu based on the card sort data.
1. Move on to Lab 4.2 after 5 minutes.

## 4.2 - Update Catalog

Based on the discussions in Lab 4.1, it is now time to update the catalog based on your findings. In the interest of time, let's make changes to the following 3 items

- The **Impossible&trade; Burger** is the most popular menu item in the last month. Let's keep it that way; make sure it is in the right category(ies) based on your research
- The chef is surprised more people are not ordering the **Quesadilla** and thinks its in the wrong place. What does the data say?
- A **Chicken Cheese Steak** was just added to the menu, based on the data, where should it go?

1. Navigate to **Service Catalog \> Maintain Items**
1. Open each item and update using the *Categories* related list

## 4.3 - Improve the Meta Data

One of the findings in the usability studies was that participants struggled to find cheeseburgers in the catalog because there is no specific catalog item called **"Cheeseburger"**. It is just a hamburger with cheese as a variable. One option would be to create a separate catalog item, but to keep reporting consistent it was decided to improve the search results through meta data. <!-- TODO Add a note about how card sort led to this as well -->

1. Navigate to **Service Catalog \> Maintain Items** in the Application Navigator.
1. Open up the **Hamburger** catalog item.
1. Make sure you are on the *Item Details* form section tab.
1. Add the following terms to the *Meta* field:

    `cheeseburger, beefburger, burger, hamburg, cheeseburg, beef sandwich`

1. Click **Update** to save your changes.
1. Switch to Service Portal `/room_service` and try a search for *cheeseburger*. Does your catalog item come back?

> Note: It is very important to understand how the search engine works on ServiceNow. The following fields on a catalog item are searchable out of the box: `Name, Meta, Short Description, Description`. [Read more about catalog items and search](https://docs.servicenow.com/bundle/newyork-it-service-management/page/product/service-catalog-management/task/search-catalog-item.html)
>
> It can be a good idea to include common misspellings of words in the Meta tags (e.g. hamburg)
>
> If the item is not returned in the last step, it could be that the system has not finished re-indexing the catalog

# Exercise 5 - Keep the Portal in Context

## Goal

Portals that do not follow corporate style guides make guests confused as to where they are. Use Portal themes to change out color schemes to match a company brand. Or, go beyond with a template to completely change the look and feel of a Portal to make it more closely match a desired design.

## 5.1 - Apply a Bootswatch Theme

Since Service Portal is built on the [Bootstrap v3](https://getbootstrap.com/docs/3.3/) framework, the Solution Innovation team challenged itself last year to port over a bunch of Bootstrap themes from the folks at [Bootswatch](https://bootswatch.com/3/) and see if they would work in the portal. These were packaged as update sets and are available for public use. They are only CSS modifications; therefore they do not introduce new widgets, layouts, or scripts. Let's try applying one to your portal

1. Navigate to <http://www.servicenowinnovation.com> and navigate to the Library>Portal Templates>Themes>Bootswatch Themes.

    ![How to get the Bootswatch themes](images/getBootswatch.gif)

1. Click the link to download **tpl-bootswatch-themes.u-update-set.xml** to be taken to GitHub
1. Right-click on the **Raw** button and choose to **Save** the Update Set XML to a file on your computer

    ![How to download from GitHub](images/downloadFromGitHub.png)

1. Commit the Update Set to your instance via **System Update Sets > Retrieved Update Sets > Import Update Set from XML**
1. Navigate to Portals in the Application Navigator.
1. Open the **Room Service** portal.
1. Click on the magnifying glass next to the *Theme* field.
1. Now you should see 9 additional themes in the list. Select any one of the 9 themes, they are all prefixed with `BS_`

    ![List of Bootswatch Themes](images/themes.png)

1. Click **Update** to save your changes.
1. Switch to Service Portal `/room_service`. Do you noticed a change?

### Think About / Challenge

> What else might you change to make the theme look better?
>
> What else can you do to make this theme tailored to your customer?

## 5.2 - Apply SN Suites Branding

One of the easiest way to take your portal demo experience to the next level is to match customer branding as close as possible. Simple changes in branded colors and fonts can make a big impact. During this portion of the lab we will be referencing our customers website for a custom branded look.

1. In a separate tab navigate to the [SN Suites](http://snsuites.com) site.

    >Observe the SN Suites site. What are the main colors and differences you see? Think of details we could easily apply to our portal as well.

1. Now navigate to the [Stylify Me](http://stylifyme.com) site. Insert the URL for SN Suites.

    >This site will pull specific details for us to use in branding our portals. If this style generator is missing a color or anything you see. Use your inspect tools to get to those details. Cmd+Opt+I to open the Developer Tools with MAC. F12, or Ctrl+Shift+I to open the Developer Tools with Windows/Linux.

1. Back in your instance navigate to Service Portals > Service Portal Configuration.
1. Click on the **Branding Editor**, choose the **Room Service** Portal from the drop down menu.
1. Upload a new image for the logo from the SN Suites site.
1. Under the **Theme Colors** tab. Use the colors from the stylify me generator to change the branding and match the SN Suites Site.
1. Now go to your Room Service Portal and observe the branding.

### Think About

> What other small ways could you modify a portal to create impact?

<!-- TODO better critical thinking questions, simple changes = big impact-->

## Exercise 5.3 - Challenge Lab - Apply the Bondi theme

Sometimes customers want to see more than different colors and and fonts applied to the portal. They want to see how far they can "push" the boundaries of Service Portal to reflect their brand or a generally more modern design. The Solution Innovation team created the Bondi template in early 2019 to reflect a dramatically different view into Service Portal. The team has applied it to custom looking IT and CSM portals as well as the Employee Service Center.

1. Go to the [ServiceNow Innovation](http://servicenowinnovation.com) site
1. Click **Library** in the header and go to **Portal Templates**.
1. Click **Bondi** (*Note*: there are other records called **Bondi Theme**, but the one to look for is just called **Bondi** as that is a template).
1. Save the **Bondi** update set and load it into your instance.
1. Open up the **Room Service** portal record and change the theme for the record to **Bondi**.
1. View your Room Service Portal and observe the changes.

<!-- TODO Possibly add fun code snippets to change the bondi theme? or show them the Bondi portal ? -->