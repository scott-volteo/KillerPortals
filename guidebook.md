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

First we'll look at **Usage Overview** to gather quantitative data about user's behaviors on the portal. Here you can see the most popular *search terms*, *pages*, *knowledge article*, and more...

1. Log in to your instance
1. In the App Navigator locate **Service Portal \> Usage Overview**
1. Review the Service Portal Search Terms

### Think About

> What are the most popular search terms?
>
> Are people typing in terms that do not correlate to data in your catalog?
>
> Are there popular search terms to just do not make sense?

## 1.2 - Survey Results

To learn more about the current state of your company's portal, we ran a survey last month with a sample of *50* users. Let's review what those users had to say

1. Navigate to **Surveys \> View Surveys**
1. Open the record *Room Service Portal Survey*
1. Click **View Scorecard**

### Think About

> What are the weakest attributes of the portal based on the survey data?
>
> Are there any interesting comments that can inform your path forward?

**Note:** We recommend this survey as a way for customers to assess the current state of their portal. You can download the [update set](files/survey.xml) with the survey.

## 1.3 - Usability Test

Now we want to collect qualitative feedback by observing how someone interacts with the current portal. For this lab, you'll be pairing off with a partner and each assuming a different role.

![usability test](images/usabilityTest.png)

1. Pair off with another lab participant
1. Introduce yourselves - Name, Role, Location
1. Whoever traveled the **FURTHEST** to get here will be the *Participant*. The other will play the role of *Facilitator*
1. The facilitator's job is to observe how the participant completes the task(s) assigned.
1. The presenters will share the task with you.
1. The participant's job is to try and complete the assigned task(s).
1. The facilitator should take notes as they observe how the tasks are completed.

### Think About

Was the participant able to easily complete the tasks presented to them?
If not, where did they encounter issues?
How can we better leverage the platform to reduce the friction the participant encountered?

# Lab 2 - Information Finds the User

## Goal

In this lab, we'll be leveraging a set of capabilities to effectively bring information to the user. By leveraging what the platform knows about the user, the Portal can present information that is uniquely relevant to them. These are just a few ways this information can be used; when working with your customers, think about how they might leverage these capabilities to create a tailored experience.

## 2.1 - Vegetarians Don't Eat Meat - Use User Criteria to filter their Menu

One of the things we noticed in our usability test was that guests with certain food allergies, had a hard time finding menu items that met their dietary needs. Let’s use User Criteria to filter what these guests see.

1. Open the User Profile for *FIRST LAST* and review the Groups they belong to. One of their groups should be **Vegetarians**
1. Now, navigate to **Maintain Items** and identify all the meat-based "menu" items
1. Select an item and scroll down the the *Related Lists* and select **Not Available For Group**
![Not Available for Group selected](images/notAvailableFor.png)
1. Click **Edit** and add the group *Vegetarians* from the slush bucket.
1. Save your changes
1. Repeat for the remaining meat items.

### Let's test this

1. Impersonate Jane Doe
1. Go to the portal and make sure you don't see the meat-based catalog items.

### **CHALLENGE**

For KB articles, you can only user Criteria at the Category level. How might you hide all meat recipes from a vegetarian user?

## 2.2 Vegetarians also like to hear news about new menu offerings

The market of plant-based alternatives to beef and chicken continues to expand, and with that our restaurant's menu is constantly evolving. How might we target vegetarians with announcements about menu updates?

1. Navigate to **Targeted Communications \> Create New Publication**
1. Configure the publication
    Field | Value
    ------|-------
    **Short Description** | Introducing new Impossible Burgers&trade; to the menu!
    **Content** | This month, we are excited to introduce a new addition to our Vegetarian Menu, the Impossible Burger&trade;. All of our mouth-watering burger specials can now be had with the delicious plant-based patty. In addition, we are introducing 2 new burgers that feature the Impossible Burger; the Predictably Impossible and the Impossibly Sweet Burgers. Enjoy the savory juiciness in our new offerings.
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

# Lab 3 - Consumers != Providers

## Goal

Often times, when creating content for a portal, customers create it from the perspective of the fulfiller and don't recognize that the user that will consume the content has a different level of knowledge, set of expectations and experiences as it relates to the issue. This often means that catalog items are confusing and users opt to call for help instead of self serving. In this lab, we'll take what we learned from the usability study and try and improve site content.

## Lab 3.1 - This form has so many options, I'd rather go hungry. - Form Design

<!-- TODO -->
Something about what you saw in the usability tests. How can we improve the form to better serve our guests knowledge

1. Open the Hamburger catalog item from the Maintain Items Application Module
1. Delete the Toppings checkbox variables from the item.
1. Create a new variable and set it up as follows
    Field | Value
    ------|-------
    **Type** | List Collector
    **Question** | What toppings would you like?
    **Name** | toppings
    **Order** | 100
1. Switch to the *Type Specifications* tab
1. Set the *List Table* field to **x_snc_todo** <!-- TO DO -->
1. Click Submit
1. Open the **Internal Temperature** variable
1. Update the form according to the table
    Field | Value
    ------|-------
    **Type** | Select Box
    **Question** | How would you like your meat cooked?
    **Name** | doneness
1. Save the Record
1. Scroll down to the *Question Choices*
1. Create the following choices
   Text | Value | Order
   ----- | ----- | ----
   Rare | 120 | 100
   Medium Rare | 135 | 200
   Medium | 140 | 300
   Medium Well | 155 | 400
   Well Done | 160 | 500
1. Click Update

## Lab 3.2 - All I want is a sandwich, but now you are asking me to be a cook? - Variable Sets

<!-- TO DO -->
During the usability testing we ran, participants complained that the same questions were asked in many different ways and the order of options was never consistent. This caused them to make mistakes in filling out the forms. Lets use Variable Sets to ensure consistency across similar catalog items

1. Reopen the Hamburger catalog item
1. Switch to the *Variable Sets* related list
1. Click **New**
1. Click **Single-Row Variable Set**
1. Set the **Title** to *Common Beef Items*
1. Click Submit
1. Switch to the *Variables* related list
1. Select the *How would you like your meat cooked?* variable
1. Clear out the *Catalog Item* field
1. Hit tab to leave the field
1. A new field will show up, titled *Variable Set*
1. Select **Common Beef Items** reference
1. Click **Update**
1. Repeat Steps 8-13 for the *What toppings would you like?* variable
1. Add the *Common Beef Items* variable set to the Cheesteak catalog item.


# Lab 4 - Don't Follow the Org Chart

## Goal

Similar to the previous lab, customers don't always know how to communicate to their end users. They use internal naming conventions, acronyms, and

## Lab  4.1 - Card Sort

Praesent sapien tortor, euismod ut posuere non, accumsan sit amet mi. Donec accumsan aliquet lacus, sed feugiat mauris elementum eu. Sed a risus sapien. Vestibulum feugiat efficitur elit, sollicitudin finibus nunc semper eget. Etiam nec nisl turpis. Quisque faucibus tincidunt lectus congue viverra. In lorem nisl, mattis non mattis congue, vestibulum vitae turpis. Donec lacinia porttitor condimentum. Vestibulum malesuada ante vel lobortis mollis. Suspendisse dolor tortor, blandit eget semper in, fringilla at nunc. Phasellus dignissim ante non lorem molestie, a accumsan lectus interdum. Quisque sit amet risus eu urna tristique efficitur. Nullam leo velit, posuere ut orci ac, sollicitudin commodo ex. Phasellus sit amet tellus enim.

## Lab 4.2 - Update Catalog

Quisque placerat varius libero ut aliquet. Integer pulvinar, massa a lacinia placerat, erat lectus aliquet purus, nec imperdiet nisi est et velit. Donec fermentum consectetur finibus. Maecenas interdum lobortis eleifend. Pellentesque ultrices vitae enim quis congue. Phasellus quis tempor arcu, rhoncus porttitor orci. Maecenas luctus lobortis nisl, ac rutrum est aliquam ac. Quisque sollicitudin ullamcorper urna. Nulla facilisi. Nullam non tristique felis. Maecenas gravida dui et venenatis consequat. Curabitur fermentum volutpat risus a interdum. Aenean vehicula, metus in fermentum molestie, mi neque condimentum orci, feugiat interdum leo tellus quis lectus.

# Lab 5 - Keep the Portal in Context

## Goal

Portals that don't follow corporate style guides make users confused as to where they are. Use Portal themeing to change out color schemes to match a company brand. Or, go beyond with a template to completely change the look and feel of a Portal to make it more closely match a desired design.

## Lab 5.1 - Apply a Bootswatch Theme

Suspendisse sodales sagittis feugiat. Donec ut urna vel lectus congue fringilla. Nullam a enim dictum, commodo ex ut, tristique nibh. Sed consectetur nulla eu lectus mollis aliquet. Vivamus vitae ante eget felis tincidunt mollis. Phasellus bibendum purus vel cursus vulputate. Suspendisse ut metus sit amet massa tempor placerat iaculis dictum elit. Praesent eu augue eu risus dapibus interdum. Pellentesque commodo sapien ac quam egestas, id dapibus enim mollis. Nullam tellus felis, eleifend at est sollicitudin, aliquam dignissim lectus. Sed ultricies posuere felis non rhoncus. Nulla massa nisl, sagittis a urna sit amet, ornare laoreet tortor. Mauris dolor massa, eleifend vitae magna in, scelerisque vulputate sapien. Sed sit amet gravida purus, at finibus quam. Proin non nisi ut sapien porta viverra id nec ipsum.

## Lab 5.2 - Challenge Lab - Apply the Bondi theme

Integer eu purus convallis, efficitur odio sed, malesuada nisl. Aliquam vitae pulvinar lorem. Suspendisse sollicitudin imperdiet ligula sit amet mattis. Nullam aliquet neque ut mi fermentum varius. Suspendisse pellentesque metus elit, at vestibulum felis volutpat in. Curabitur maximus magna id nulla laoreet scelerisque. Aliquam enim nisl, fringilla ac magna at, varius posuere elit. Nulla hendrerit gravida felis, sit amet viverra neque egestas id. Sed commodo rhoncus enim, in semper massa pellentesque in. Proin dapibus velit et nisi vehicula cursus. Fusce feugiat efficitur varius. Maecenas non sapien fringilla, porta felis eleifend, luctus dui.

1. Go to the [ServiceNow Innovation](http://servicenowinnovation.com) site
1. Click **Library** in the header
1. Click **Portal Templates**
1. Click **Bondi** (*Note*: there are other records called **Bondi Theme**, but we want the one just called **Bondi** as that is a template)
1. KEEP GOING


