# AI Elicitation Audit

## AI Tool Used

Microsoft Copilot

## Prompt Used

" I am designing a Food Waste Reducer app. The purpose of the app is to help users reduce food waste by tracking food in their pantry and refrigerator, monitoring expiration dates, recommending recipes based on available food, maintaining a grocery list, and showing food and money savings. Please elicit the functional and non-functional requirements for this application. Ask any important questions you need to clarify the requirements, and then provide user stories with acceptance criteria and non-functional requirements."

## What Copilot Got Right

Copilot got several of the main ideas of my app correct.

- Understood that users need to be able to keep track of food in their pantry and refrigerator. It included adding, viewing, editing, and removing food items.
- Included expiration tracking and reminders. This matches my goal of helping users use their food before it expires.
- Included recipe recommendations based on the food that the user already has.
- Included a grocery list where users can add and remove items.
- Included tracking what happens to food after it is in the inventory. This is related to my requirement for marking food as used.
- Included a dashboard for showing food outcomes and money saved.

These parts were helpful because they matched the main features I had already planned for my app.

## What Copilot Missed

Even though Copilot understood the main idea of my app, it missed some specific requirements that I had already included.

### 1. The 3-Day Expiration Rule

My requirement says that food within 3 days of its expiration date should be marked as needing attention.

Copilot only said that the app should identify food with "approaching" dates. It did not give a specific number of days.

This is important because "approaching expiration" could mean 1 day, 3 days, 7 days, or something else. My 3-day rule makes the requirement clear and easy to test.

### 2. Required Food Information

My requirements say that the food name and expiration date are required. If either one is missing, the item should not be saved.

Copilot included food names and dates, but it did not clearly state this same rule about rejecting an item when required information is missing.

### 3. Saving Data After Closing the App

My requirements say that saved inventory and grocery-list items should still be there after the application is closed and reopened.

Copilot focused more on syncing information between web and mobile devices. It did not specifically include my requirement about making sure the data is still there after restarting the application.

## What Copilot Added That I Did Not Ask For

Copilot also added several features that were not part of my original idea.

### 1. Receipt Scanning

Copilot suggested letting users scan grocery receipts to automatically add food.

I did not ask for this feature. It would make the app more complicated because it would need technology to read and understand receipts.

### 2. User Accounts

Copilot added account creation, login, logout, and account recovery.

I did not originally say that users needed accounts. Adding this would require additional work for passwords, security, and storing user information.

### 3. Cross-Device Syncing

Copilot suggested that the app should work on both web and mobile and keep the information synced between devices.

I did not ask for this feature. It would add more development work and is not necessary for the basic version of my app.

### 4. Dietary Preferences and Allergens

Copilot added dietary preferences and allergen settings for recipes.

I did not include these features in my original requirements because they are not necessary for the main purpose of reducing food waste.

### 5. Push Notifications

Copilot added push notifications for expiration reminders.

I only required users to be able to see which food needs attention. I did not specifically ask for phone notifications.

### 6. AI-Generated Recipes

Copilot added a feature where the user can ask AI to create a recipe.

My requirement was only to recommend recipes based on the food the user already has. I did not ask for AI-generated recipes.

### 7. Donated and Discarded Food

Copilot expanded my "mark food as used" feature to include food that is donated or discarded.

I did not originally plan to track these separate categories.

### 8. Partial Quantities

Copilot added the ability to use or discard only part of a food item.

For example, a user could have 5 apples and mark only 2 as used. I did not include this level of quantity tracking in my original requirements.

## What I Had Not Thought About

Even though Copilot added too many features, it also brought up some questions that I had not really thought about before.

Some of these questions were:

- How exactly should the app calculate money saved?
- What should happen if a food item's expiration date is unknown?
- Should users be able to edit an expiration date?
- What should happen when a recipe uses ingredients that the user does not have?
- What should happen if the recipe service is unavailable?
- Should the app work on multiple devices?
- How long should food information be stored?

These questions could be useful if I continue developing the app, even though I would not necessarily add all of the features Copilot suggested.

## Overall Judgment

I think Copilot was useful for getting ideas and identifying the main features of my app. It correctly understood the basic idea of tracking food, expiration dates, recipes, grocery lists, and savings.

However, I would not use its response as my final requirements document.

The biggest problem was that Copilot added a lot of features that I never asked for, such as receipt scanning, accounts, push notifications, AI-generated recipes, and cross-device syncing. These features would make the project much bigger than I originally planned.

Copilot also missed some of my specific requirements, especially the 3-day expiration rule and the requirement to reject food items when required information is missing.

This showed me that AI can be helpful when coming up with requirements, but I still need to review the results and decide what actually belongs in my project.
