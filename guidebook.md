# Introduction

## Goal

The goal of this lab is the reinforce the Best Practices and Key Capabilities from the presentation today. In it you will leverage key ServiceNow capabilities to design a portal that is contextual to the user; with relevant content and catalog items, visually different; with the application of a simple or complex theme change, and representative of a portal that helps a customer's journey to self-service

### Getting Started - Log on to Your Training Instance

1. Navigate to the unique instance URL provided to you.
1. Log on with the provided credentials
1. Change your password to something memorable just in case you get logged out of your instance.

# Lab 1 - Understanding the Current State

## Goal

In this lab we are going to get a better understanding of the current state of the portal. To do this we want to look at capabilities the platform provides but also get feedback from users

## 1.1 - Usage Overview

First we'll look at **Usage Overview* to gather quantitative data about user's behaviors on the portal. Here you can see the most popular *search terms*, *pages, *knowledge article*, and more...

1. Log in to your instance
1. In the App Navigator locate Service Portal  Usage Overview
1. Review the Service Portal Search Terms

### Think About

What are the most popular search terms?
Are people typing in terms that don’t correlate to data in your catalog
Are there popular search terms to just don’t make sense?

## 1.2 - Survey Results

To learn more about the current state of your company's portal, we ran a survey last month with a sample of *50* users. Let's review what those users had to say

1. Navigate to **Surveys&rarr;View Surveys**
1. Open *Room Service Portal Survey*
1. Click on **View Scorecard**

### Think About

What are the weakest attributes of the portal based on the survey data?
Are there any interesting comments that can inform your path forward?

>**Note:** We recommend this survey as a way for customers to assess the current state of their portal. You can download the [update set](files/survey.xml) with the survey.

## 1.3 - Usability Test

Now we want to collect qualitative feedback by observing how someone interacts with the current portal. For this lab, you'll be pairing off with a partner and each assuming a different role.

![usability test](images/usabilityTest.png)

1. Pair off with another lab participant
1. Introduce yourselves - Name, Role, Location
1. Whoever traveled the **FURTHEST* to get here will be the *Participant*. The other will play the role of *Facilitator*
1. The facilitator's job is to observe how the participant completes the task(s) assigned.
1. The presenters will share the task with you.
1. The participant's job is to try and complete the assigned task(s).
1. The facilitator should take notes as they observe how the tasks are completed.

### Think About

Was the participant able to easily complete the tasks presented to them?
If not, where did they encounter issues?
How can we better leverage the platform to reduce the friction the participant encountered?

# Information Finds the User

In this lab, we'll be leveraging a set of capabilities to effectively bring information to the user. By leveraging what the platform knows about the user, the Portal can present information that is uniquely relevant to them. These are just a few ways this information can be used; when working with your customers, think about how they might leverage these capabilities to create a tailored experience.

## 2.1 - Vegetarians Don't Eat Meat - Use User Criteria to filter their Menu

One of the things we noticed in our usability test was that guests with certain food allergies, had a hard time finding menu items that met their dietary needs. Let’s use User Criteria to filter what these guests see.

1. Open the User Profile for *FIRST LAST* and review the Groups they belong to. One of their groups should be **Vegetarians**
1. Now, navigate to **Maintain Items* and identify all the meat-based "menu" items
1. Select an item and scroll down the the *Related Lists* and select **Not Available For Group**
![Not Available for Group selected](images/notAvailableFor.png)
1. Click **Edit** and add the group *Vegetarians* from the slush bucket.
1. Save your changes
1. Repeat for the remaining meat items.

## Let's test this

1. Impersonate Jane Doe
1. Go to the portal and make sure you don't see the meat-based catalog items.

## **CHALLENGE**

For KB articles, you can only user Criteria at the Category level. How might you hide all meat recipes from a vegetarian user?

## 2.2 Vegetarians also like to hear news about new menu offerings

The market of plant-based alternatives to beef and chicken continues to expand, and with that our restaurant's menu is constantly evolving. How might we target vegetarians with announcements about menu updates.

1. Navigate to **Targeted Communications&rarr;Create New Publication**
1. Configure the publication
    Field | Value
    ------|-------
    **Short Description** | Introducing new Impossible Burgers&tmark; to the menu!
    **Content** | This month, we are excited to introduce a new addition to our Vegetarian Menu, the Impossible Burger&tmark;. All of our mouth-watering burger specials can now be had with the delicious plant-based patty. In addition, we are introducing 2 new burgers that feature the Impossible Burger; the Predictably Impossible and the Impossibly Sweet Burgers. Enjoy the savory juiciness in our new offerings.
    **Content Type** | HTML
    **Category** | Information
    **Publish Date** | Jan 23, 2020
    **Expiry Date** | Jan 30, 2020
    **Email Template** | ImpossibleEmails

1. Open up the *Recipient List* and create a new list.
1. Modify the setup to the following

    Field | Value
    ------|-------
    **Method** | Dynamic Condition
    **Table** | sys_user_grmember
    **User Field** | user
    **Condition** | group IS vegetarians

    ![Recipient List Configuration](images/recipientList.png)

1. Submit the Publication
1. **TODO* Any more steps? TKTKTKTK

## Lab 2.3 When they read about the Room Service policies, they want information relevant to them - Knowledge Blocks

To wrap up this lab, we are going to configure some articles to show content based on User Criteria. This will use *Knowledge Blocks* to provide dynamic information, based on the user's profile.

1. Step 1
1. Step 2

# Consumers != Providers

Often times, when creating content for a portal, customers create it from the perspective of the fulfiller and don't recognize that the user that will consume the content has a different level of knowledge, set of expectations and experiences as it relates to the issue. This often means that catalog items are confusing and users opt to call for help instead of self serving. In this lab, we'll take what we learned from the usability study and try and improve site content.

## Lab 3.1 - All I want is a sandwich, but now you are asking me to be a cook? - Variable Sets

Different chefs added menu items to the catalog and ask for information about the menu options in different ways. Let's use variable sets to improve how we get guests' preferences for their order.

1. Step 1
1. Step 2

<!-- TO DO IDEA FOR LAB 3 -->

## Lab 3.2 - Is there something else we can do for this topic

# Don't Follow the Org Chart

Similar to the previous lab, customers don't always know how to communicate to their end users. They use internal naming conventions, acronmyns, and 
