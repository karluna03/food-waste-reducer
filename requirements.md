# Food Waste Reducer Requirements

## User Stories

### 1. Add Food Items

As a user, I want to add food items to my pantry or refrigerator so that I can keep track of the food I have available.

#### Acceptance Criteria

- The user can enter the food item's name
- The user can enter an expiration date
- The user can identify whether the item is stored in the fridge or pantry
- The added item appears in the user's food inventory
- The system does not add an item if required information is missing

### 2. View Food Inventory

As a user, I want to view the food in my pantry and refrigerator so that I know what food I currently have.

#### Acceptance Criteria

- The system displays the user's stored food items
- Each food item displays its name and expiration date
- The user can distinguish between refrigerator and pantry items
- The inventory updates when a food item is added or removed

### 3. Expiration Reminders

As a user, I want to receive reminders about food that is approaching its expiration date so that I can use it before it goes to waste.

#### Acceptance Criteria

- The system should identify food items that are within 3 days of their expiration date as needing attention
- The user can see which items need to be used soon
- Expired items are identified separately from items that are still usable

### 4. Recipe Recommendations

As a user, I want to receive recipe suggestions based on the food I already have so that I can use ingredients before they expire.

#### Acceptance Criteria

- The system uses food in the user's inventory when generating recipe suggestions
- Recipes identify the ingredients needed
- Recipes using food that is approaching expiration are prioritized
- The user can view the recipe information before deciding what to make

### 5. Grocery List

As a user, I want to create a grocery list so that I can keep track of food I need to purchase

#### Acceptance Criteria

- The user can add an item to the grocery list
- The user can remove an item from the grocery list
- The user can view the current grocery list
- Items on the grocery list are separate from items in the food inventory

### 6. Mark Food as Used

As a user, I want to mark food as used so that my inventory stays accurate and my food-saving information can be updated.

#### Acceptance Criteria

- The user can mark an item as used
- A used item is removed from the active food inventory
- The system records that the item was used before its expiration date when applicable
- The user's food-saving information is updated after an item is marked used

### 7. Food Waste and Savings Dashboard

As a user, I want to see how much food and money I have saved so that I can understand the impact of using food before it goes to waste

#### Acceptance Criteria

- The dashboard displays information about food that was used before expiration
- The dashboard displays an estimate of money saved when enough information is available
- The dashboard updates when relevant food items are marked as used
- The information is presented in an easy-to-read format

## Non-Functional Requirements

### 1. Response Time

The application should display the updated food inventory within 2 seconds after a user adds, removes, or updates a food item.
How to test: Perform the operation 10 times and verify that the updated inventory appears within 2 seconds each time.

### 2. Data Persistence

The application should preserve all successfully saved food inventory and grocery-list items after the application is closed and reopened.
How to test: Add items, close the application, reopen it, and verify that all saved items are still present.

### 3. Input Validation

The application should reject a food-item entry when the food name or expiration date is missing and display an error message to the user.
How to test: Attempt to add an item with each required field missing and verify that the item is not saved.
