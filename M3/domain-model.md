# Food Waste Reducer Domain Model

My domain model shows the main things my Food Waste Reducer app needs to keep track of. The main entities are **User, FoodItem, GroceryListItem, Recipe, and RecipeIngredient**.

## 1. User

The **User** is the person who uses the app.

The user has their own food inventory and grocery list.

**Attribute:**

- userId – identifies the user

**Relationships:**

- One user can have many food items.
- One user can have many grocery-list items.

## 2. FoodItem

The **FoodItem** represents food that the user has in their fridge or pantry.

This is an important part of the app because the user needs to add food, see their food, and mark food as used.

**Attributes:**

- foodItemId – identifies the food item
- name – the name of the food
- expirationDate – when the food expires
- storageLocation – whether the food is in the fridge or pantry
- status – whether the food is active or has been used
- usedAt – when the food was marked as used
- estimatedCost – optional cost information that can be used to estimate money saved

**Relationships:**

- Each food item belongs to one user.
- One user can have many food items.

The expiration date can also be used to tell if food is expired or if it needs to be used soon.

## 3. GroceryListItem

The **GroceryListItem** represents something the user wants to buy.

I kept grocery-list items separate from food items because the requirements say that items on the grocery list should be separate from food already in the inventory.

**Attributes:**

- groceryListItemId – identifies the grocery item
- name – the name of the item

**Relationships:**

- Each grocery-list item belongs to one user.
- One user can have many grocery-list items.

## 4. Recipe

The **Recipe** represents a recipe that the app can suggest to the user.

The app can use the food in the user's inventory to help decide which recipes to recommend.

**Attributes:**

- recipeId – identifies the recipe
- name – the name of the recipe
- instructions – how to make the recipe

**Relationships:**

- Each recipe has one or more ingredients.

## 5. RecipeIngredient

The **RecipeIngredient** represents an ingredient needed to make a recipe.

**Attributes:**

- name – the name of the ingredient
- quantity – how much of the ingredient is needed, if known
- unit – the measurement unit, if known

**Relationships:**

- Each ingredient belongs to a recipe.
- A recipe can have multiple ingredients.

## Information the App Can Calculate

Not everything in the app needs to be its own entity. Some information can be calculated using the information already stored.

For example, the app can use a food item's expiration date to figure out its status:

- **Expired:** The expiration date has passed.
- **Needs attention:** The food expires today or within the next 3 days.
- **Not approaching expiration:** The food expires more than 3 days from now.

The app can also create recipe recommendations by looking at the food the user currently has. Recipes that use food that is close to expiring can be shown first.

The savings dashboard can also use information from FoodItems. When a user marks food as used, the app can check if it was used before it expired. If there is enough cost information, the app can also estimate how much money the user saved.

## Why I Chose These Entities

I chose these entities because they are connected to the requirements from M2. **FoodItem** is needed for the food inventory, expiration reminders, marking food as used, and the savings dashboard. **GroceryListItem** is needed for the grocery list. **Recipe** and **RecipeIngredient** are needed for the recipe recommendation feature.

I did not make separate entities for reminders, recipe recommendations, or the dashboard because they do not need to be stored as separate objects. The app can create this information using the data it already has.

Overall, I kept my domain model simple and focused on the information the app actually needs. This avoids adding extra entities that are not required by my M2 requirements.
