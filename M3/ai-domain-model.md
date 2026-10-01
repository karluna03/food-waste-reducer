# Food Waste Reducer Domain Model

## Purpose and Scope

This model describes the core information the application manages: a user's active food inventory, grocery-list entries, recipe recommendations, and the usage history used to report food saved and estimated money saved. It is a conceptual model; implementation details such as database tables and UI components are intentionally left open.

## Domain Concepts

### User

The person who maintains food inventory and a grocery list.

- `userId`: unique identifier
- Owns food items and grocery-list entries
- Can view inventory, reminders, recipe recommendations, and savings information

### FoodItem

One tracked item of food. A food item is distinct from a grocery-list entry. When marked used, it is removed from the active inventory but its record is retained for history and savings calculations.

- `foodItemId`: unique identifier
- `name`: required, non-empty food name
- `expirationDate`: required date
- `storageLocation`: required; `Fridge` or `Pantry`
- `status`: `Active`, `Used`, or `Removed`
- `addedAt`: date/time the item was added
- `usedAt`: date/time the item was marked used; set only for `Used` items
- `estimatedCost`: optional amount, available when the user or system has enough information to estimate savings

### GroceryListItem

An item the user intends to purchase. It is not an inventory item and does not have an expiration date or storage location unless future requirements add those concepts.

- `groceryListItemId`: unique identifier
- `name`: required item name
- `addedAt`: date/time it was added to the list

### Recipe

A recipe that can be shown to the user as a possible way to use available food.

- `recipeId`: unique identifier
- `name`: recipe name
- `instructions`: preparation information
- `ingredients`: the ingredients and quantities needed

### RecipeIngredient

An ingredient requirement associated with a recipe.

- `name`: ingredient name
- `quantity`: amount required, when known
- `unit`: measurement unit, when known

### RecipeRecommendation

A recipe presented to a user based on the user's active inventory. It can be ranked to prioritize use of food approaching expiration.

- `matchedFoodItems`: the user's inventory items that can satisfy recipe ingredients
- `priority`: derived ranking; higher when the recipe uses one or more items needing attention
- `generatedAt`: date/time the recommendation was generated

## Relationships and Cardinalities

` ``mermaid
erDiagram
    USER ||--o{ FOOD_ITEM : tracks
    USER ||--o{ GROCERY_LIST_ITEM : maintains
    USER ||--o{ RECIPE_RECOMMENDATION : receives
    RECIPE ||--|{ RECIPE_INGREDIENT : requires
    RECIPE ||--o{ RECIPE_RECOMMENDATION : appears_in
    RECIPE_RECOMMENDATION }o--o{ FOOD_ITEM : matches
` ``

- A user may have zero or many food items; each food item belongs to exactly one user.
- A user may have zero or many grocery-list entries; each entry belongs to exactly one user.
- A recipe has one or more ingredient requirements. An ingredient can be required by many recipes.
- A recommendation is for one recipe and one user. It may match zero or many of that user's active food items.
- Food items and grocery-list entries are separate concepts and collections. Adding or removing a grocery-list entry does not change inventory.

## Derived Food Conditions

These are calculated from an active food item's `expirationDate` and the current date; they do not replace its lifecycle `status`.

| Condition | Rule |
| --- | --- |
| Expired | `expirationDate` is earlier than today |
| Needs attention | Not expired and `expirationDate` is today or within the next 3 days |
| Not approaching expiration | `expirationDate` is more than 3 days away |

The application should present expired items separately from items that are still usable. Only active items belong in the current inventory. Used and removed items remain available as historical records, not active inventory.

## Core Business Rules

1. A food item cannot be created without a non-empty name, an expiration date, and a storage location. Invalid entries are rejected and an error is shown.
2. A newly created food item has `status = Active` and appears in its owner's inventory.
3. Marking an active food item as used sets `status = Used` and records `usedAt`. The item no longer appears in active inventory.
4. Whether an item was used before expiration is derived from its usage time and expiration date. With date-only precision, it qualifies when `usedAt` falls on a calendar date earlier than `expirationDate`.
5. The dashboard's food-saved information is derived from qualifying used-item history. Estimated money saved is shown only when sufficient cost information is available; otherwise it is unavailable rather than assumed.
6. Recipe recommendations are based on the user's active inventory. Recommendations using items that need attention receive higher priority, and recipe details and required ingredients are available before the user decides to make one.
7. Inventory changes when a food item is added, removed, or marked used. Grocery-list changes do not count as inventory changes.

## Requirements Mapped to the Model

| Requirement | Domain support |
| --- | --- |
| Add and view food | `FoodItem`, required fields, owner relationship, and active inventory |
| Expiration reminders | Derived food conditions based on `expirationDate` |
| Recipe recommendations | `Recipe`, `RecipeIngredient`, and inventory-matched recommendations |
| Grocery list | Separate `GroceryListItem` collection owned by the user |
| Mark food as used | `FoodItem.status`, `usedAt`, and retained history |
| Waste and savings dashboard | Derived usage outcomes and optional `estimatedCost` |
| Persistence | Successfully saved food and grocery-list records must survive application restarts |
| Response time | Updated inventory should be displayed within 2 seconds after a food-item change |

The persistence and response-time requirements constrain the system rather than defining additional domain entities.

## Open Modeling Decisions

- Should users be able to edit an item's name, expiration date, or storage location after adding it?
- Should `estimatedCost` represent the cost of the whole tracked item, a unit price, or a user-entered estimate? A consistent basis is needed before calculating money saved.
- Should the model track quantities for food items so recipes can distinguish a partial ingredient match from a sufficient amount?
- Is `Removed` needed as a distinct lifecycle state, or should removing an item be treated as a permanent deletion? Retaining it is useful only if audit history is desired.
