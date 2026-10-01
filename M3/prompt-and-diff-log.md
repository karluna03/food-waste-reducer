# Prompt-and-Diff Log

## Prompt I Used

I gave my M2 requirements to an AI tool and asked it to make a domain model for my Food Waste Reducer app.

I used this prompt:

" Based on my M2 requirements for my Food Waste Reducer app, create a domain model. List the main classes, their attributes, and how they are connected. Only include things that are needed for my requirements. "

I saved the AI's first response without making any changes.

## Changes I Made

| AI Model             | My Model         | Why I Changed It                                                                                                                                                 |
| -------------------- | ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| User                 | User             | I kept User because the food inventory and grocery list belong to the user.                                                                                      |
| FoodItem             | FoodItem         | I kept this because the app needs to keep track of the food the user has.                                                                                        |
| GroceryListItem      | GroceryListItem  | I kept this because the grocery list is separate from the food inventory.                                                                                        |
| Recipe               | Recipe           | I kept this because the app needs to give the user recipe suggestions.                                                                                           |
| RecipeIngredient     | RecipeIngredient | I kept this because the user needs to see what ingredients a recipe requires.                                                                                    |
| RecipeRecommendation | Removed          | I removed this because the app can create recipe suggestions using the food the user already has. It does not need to save each recommendation as its own class. |
| `addedAt`            | Removed          | I removed this because my requirements do not say that I need to keep track of when an item was added.                                                           |
| `generatedAt`        | Removed          | I removed this because I do not need to keep track of when a recipe suggestion was created.                                                                      |
| `Removed` status     | Removed          | I removed this because my requirements do not say that I need a separate status for removed food.                                                                |
| `matchedFoodItems`   | Not included     | I decided this can be figured out by comparing the user's food with the recipe ingredients.                                                                      |
| `priority`           | Not included     | I decided the app can figure out which recipes should come first by checking expiration dates.                                                                   |

## Biggest Change

The biggest change I made was removing **RecipeRecommendation**.

The AI made it its own class, but I don't think it needs to be. My requirements only say that the app should recommend recipes based on the food the user has. The app can do this when the user asks for recommendations, so there is no reason to save each recommendation separately.

## Why I Made These Changes

I wanted my domain model to be simple and only include things that my app actually needs. The AI added some extra information that could possibly be useful later, but it is not needed for the requirements I have right now.

My final classes are:

- User
- FoodItem
- GroceryListItem
- Recipe
- RecipeIngredient

Things like expiration reminders, recipe recommendations, and the savings dashboard can be figured out using the information in these classes. They do not need to be separate classes.

## Final Result

The AI's model was helpful as a starting point, but I simplified it so that my domain model matches my M2 requirements more closely. I mainly removed things that were not necessary instead of adding more classes.
