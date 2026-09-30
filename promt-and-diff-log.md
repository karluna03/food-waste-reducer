# Prompt-and-Diff Log — Food Waste Reducer

## AI Tool

Microsoft Copilot

## Prompt

" I am designing a Food Waste Reducer app. The purpose of the app is to help users reduce food waste by tracking food in their pantry and refrigerator, monitoring expiration dates, recommending recipes based on available food, maintaining a grocery list, and showing food and money savings. Please elicit the functional and non-functional requirements for this application. Ask any important questions you need to clarify the requirements, and then provide user stories with acceptance criteria and non-functional requirements."

## Comparison

| Area             | My Requirements                                            | Copilot's Requirements                                                         | Difference                                                                   |
| ---------------- | ---------------------------------------------------------- | ------------------------------------------------------------------------------ | ---------------------------------------------------------------------------- |
| Add food         | Enter name, expiration date, and storage location          | Added name, quantity, unit, location, purchase date, cost, date type, and date | Copilot added several fields I did not ask for                               |
| View inventory   | View food in the pantry and refrigerator                   | View, search, sort, and filter inventory                                       | Copilot added extra ways to organize inventory                               |
| Expiration       | Food within 3 days needs attention                         | Food with approaching or passed dates                                          | Copilot missed my specific 3-day rule                                        |
| Recipes          | Recommend recipes using food the user has                  | Recommend recipes and generate recipes with AI                                 | Copilot added AI-generated recipes                                           |
| Grocery list     | Add and remove grocery items                               | Add, edit, check off, remove, and move items into inventory                    | Copilot added extra features                                                 |
| Mark as used     | Mark food as used and remove it from active inventory      | Track used, donated, discarded, and partial quantities                         | Copilot expanded the feature                                                 |
| Dashboard        | Show food used before expiration and estimated money saved | Track used, donated, discarded, and money saved                                | Copilot added more types of food outcomes                                    |
| Validation       | Reject an item if food name or expiration date is missing  | Validate quantities and dates                                                  | Copilot did not clearly match my validation rule                             |
| Performance      | Inventory updates within 2 seconds                         | Views and saves within 2 seconds at the 95th percentile                        | Both included performance requirements, but they used different measurements |
| Data persistence | Data stays after closing and reopening the app             | Data syncs between web and mobile                                              | Copilot focused on a different type of data storage                          |
| Notifications    | Users can see food that needs attention                    | Push notifications and in-app alerts                                           | Copilot added push notifications                                             |

## Things Copilot Missed

The biggest things Copilot missed were:

1. My specific 3-day expiration rule.
2. The exact rule that missing food name or expiration date prevents an item from being saved.
3. My requirement that saved inventory and grocery-list items remain after closing and reopening the application.

## Things Copilot Added

Copilot added several things that were not in my original requirements:

1. Receipt scanning.
2. User accounts and login.
3. Cross-device syncing.
4. Dietary preferences and allergen settings.
5. Push notifications.
6. AI-generated recipes.
7. Tracking donated and discarded food.
8. Partial food quantities.
9. Best-before and use-by dates.
10. Search, sorting, and filtering.

## Things I Had Not Thought About

Copilot also made me think about some questions that I had not considered before, such as:

- How should money saved be calculated?
- What should happen when an expiration date is unknown?
- Should users be able to edit expiration dates?
- What should happen if a recipe needs ingredients that are not in the inventory?
- What should happen if a recipe service is unavailable?
- Should the app work across multiple devices?

## Final Judgment

Overall, Copilot was helpful for brainstorming because it found the main features of my app and brought up some questions I had not considered.

However, it also added many features that were outside my original scope. Because of this, I would use Copilot's response as a starting point instead of using it as my final requirements.

The comparison showed me that AI can make assumptions about what an app should include. I still need to review the AI's suggestions, remove features I do not need, and make my own requirements specific and testable.
