# Food Waste Reducer: Requirements Elicitation

## Purpose and Scope

Food Waste Reducer helps an individual household user track food in a pantry and refrigerator, use food before it spoils, plan meals from available ingredients, maintain a grocery list, and understand food and money saved.

The initial product targets web and mobile experiences. It supports manual inventory entry and receipt scanning, but receipt-extracted data must be reviewed and confirmed by the user. Recipe discovery combines a recipe catalog with AI-generated suggestions. The app distinguishes best-before dates from use-by dates and tracks food as used, donated, or discarded.

## Stakeholders and Users

- **Primary user:** An individual managing household groceries and meals.
- **Product operator:** Maintains application availability, integrations, and user support.
- **External services:** Receipt text extraction, recipe/catalog data, optional AI recipe generation, and push notification delivery.

Shared household accounts and member roles are out of the initial scope.

## Assumptions and Decisions to Confirm

- A user can use the app on web and mobile with the same account and synchronized data.
- Receipt scanning extracts candidate products and dates where available; it does not silently add unreviewed inventory.
- A best-before date describes quality, while a use-by date is treated as a safety-sensitive date. The app will not claim to determine whether food is safe to eat.
- Recipe suggestions respect stored dietary preferences and allergen exclusions. AI suggestions are clearly identified and are not guaranteed to be nutritionally or medically safe.
- Savings are reported from user-recorded outcomes and cost data where available. Estimates are labeled and their calculation is explainable.
- Push notifications require user permission; in-app alerts remain available when permission is denied.
- Pricing, target jurisdictions, supported currencies/languages, receipt-image retention, and specific recipe/AI providers remain to be selected.

## Functional Requirements

### Account and Preferences

- **FR-01:** The system shall allow a user to create an account, sign in, sign out, and recover access.
- **FR-02:** The system shall synchronize a user's inventory, preferences, recipes, grocery list, and savings data across supported web and mobile clients.
- **FR-03:** The user shall be able to configure dietary preferences, allergens to exclude, notification settings, and preferred measurement units.

### Food Inventory

- **FR-04:** The user shall be able to add, view, edit, and remove food items.
- **FR-05:** An inventory item shall support a name, quantity, unit, storage location (pantry or refrigerator), optional purchase date, optional cost, date type (best-before or use-by), and date value.
- **FR-06:** The user shall be able to search, sort, and filter inventory by name, location, date, and status.
- **FR-07:** The system shall identify items with approaching or passed dates and prioritize use-by items distinctly from best-before items.
- **FR-08:** The user shall be able to mark an item or quantity as used, donated, or discarded and record the date and optional reason or cost/value information.
- **FR-09:** The system shall support partial quantities being consumed or discarded without requiring the whole item to be removed.
- **FR-10:** Where a date is unknown, the system may offer an estimated reminder date. It shall label the date as an estimate and allow the user to edit or remove it.

### Receipt Scanning

- **FR-11:** The user shall be able to capture or upload a grocery receipt for item extraction.
- **FR-12:** The system shall present extracted items and confidence/uncertainty for user review before inventory is changed.
- **FR-13:** The user shall be able to edit, remove, or confirm extracted items and assign storage location and date information when missing.
- **FR-14:** The system shall report scanning failures and allow the user to retry or enter items manually.

### Reminders and Alerts

- **FR-15:** The system shall show in-app alerts for items approaching or past their recorded dates.
- **FR-16:** The system shall send push notifications for qualifying alerts when the user has enabled them and granted platform permission.
- **FR-17:** The user shall be able to configure alert timing and disable push notifications without losing in-app alerts.
- **FR-18:** Alerts shall identify the item, its storage location, its date type and date, and a relevant next action, without asserting that an item is safe or unsafe to consume.

### Recipe Recommendations

- **FR-19:** The system shall recommend recipes using inventory the user has on hand and prioritize recipes that use items approaching their dates.
- **FR-20:** Each catalog recipe shall show required ingredients, preparation instructions, and which ingredients are missing or available.
- **FR-21:** The user shall be able to filter or rank recipe results by available ingredients, preparation time, dietary preference, and excluded allergens.
- **FR-22:** The user shall be able to request an AI-generated recipe based on selected available ingredients and preferences.
- **FR-23:** AI-generated suggestions shall be labeled as generated, identify ingredient quantities and preparation steps where available, and allow the user to report an unsuitable result.
- **FR-24:** The user shall be able to add missing recipe ingredients to the grocery list.

### Grocery List

- **FR-25:** The user shall be able to add, edit, check off, and remove grocery-list items.
- **FR-26:** The system shall allow missing ingredients from a selected recipe to be added to the list.
- **FR-27:** The user shall be able to move a purchased grocery-list item into inventory, entering or confirming quantity, storage location, and date information.
- **FR-28:** The system shall identify likely duplicates when an item is added to the grocery list or inventory and let the user decide whether to merge them.

### Dashboard and Savings

- **FR-29:** The dashboard shall summarize current inventory, items needing attention, and recent food outcomes.
- **FR-30:** The system shall report quantities and counts of food marked used, donated, and discarded over a user-selected period.
- **FR-31:** The system shall calculate money saved only when required cost data or an explicitly labeled estimate is available; it shall show the basis and period for each total.
- **FR-32:** The user shall be able to correct or undo a recorded food outcome so that dashboard totals remain accurate.

## User Stories and Acceptance Criteria

### US-01: Maintain Inventory Manually

As a user, I want to record food in my pantry or refrigerator so that I can see what I already have.

- Given I am adding an item, when I provide its name and confirm, then it is saved and appears in my inventory.
- Given an item is saved, when I edit its quantity, location, or date information, then the updated values appear across my signed-in clients.
- Given an item has a partial quantity, when I record that some quantity was used, then only that quantity is deducted and the remainder stays in inventory.
- Given I enter an invalid quantity or date, when I attempt to save, then the app explains the issue and does not silently save invalid data.

### US-02: Scan a Receipt

As a user, I want to scan a receipt so that I can add groceries without entering every name manually.

- Given I submit a readable receipt, when extraction completes, then I see proposed line items before any are added to inventory.
- Given an extracted item is uncertain or incomplete, when I review it, then I can correct it or omit it.
- Given I confirm selected items, when the scan is committed, then only confirmed items are added and missing location/date fields can be completed.
- Given extraction fails, when the result is shown, then I can retry or switch to manual entry without losing control of my inventory.

### US-03: Find Food to Use Soon

As a user, I want to see food approaching its date so that I can plan to use it in time.

- Given an item has a recorded date, when it falls within my alert window, then it appears in an attention view with its date type and date.
- Given an item has a use-by date, when it is displayed or alerted, then it is distinguished from a best-before item.
- Given an item's date is estimated, when it is displayed, then the estimate is labeled and can be edited.
- Given a date has passed, when the item is displayed, then the app prompts me to review its status and does not make a safety determination.

### US-04: Record Food Outcomes

As a user, I want to record whether food was used, donated, or discarded so that I can understand what happens to my groceries.

- Given an inventory item exists, when I record it as used, donated, or discarded, then its outcome and date are saved.
- Given only part of an item was used or discarded, when I enter that amount, then the remaining quantity is adjusted accurately.
- Given I record an outcome by mistake, when I correct or undo it, then inventory and outcome summaries reflect the correction.
- Given I have not provided cost data, when savings are shown, then the app does not present an unsupported precise monetary saving.

### US-05: Get Relevant Recipe Ideas

As a user, I want recipe suggestions based on food I have, especially food needing attention, so that I can use it in meals.

- Given I have inventory, when I view recommendations, then recipes using available items are shown and items needing attention influence their priority.
- Given a recipe requires unavailable ingredients, when I view its details, then missing ingredients are clearly identified.
- Given I have configured dietary preferences or allergen exclusions, when recipes are recommended or generated, then those settings are applied and exclusions are visible.
- Given I request an AI-generated recipe, when the result is returned, then it is labeled as generated and I can reject or report it.
- Given recipe generation or catalog lookup is unavailable, when I open recommendations, then the app reports the limitation and preserves access to my inventory.

### US-06: Manage a Grocery List

As a user, I want to maintain a shopping list and add missing recipe ingredients so that I can shop efficiently.

- Given I add an item to my list, when I save it, then it appears as an unchecked item and remains until completed or removed.
- Given a recipe has missing ingredients, when I choose to add them, then selected ingredients appear on my list without duplicating existing entries unnoticed.
- Given I purchase a listed item, when I mark it as purchased, then I can add it to inventory with quantity, location, and date details.

### US-07: Receive Useful Alerts

As a user, I want configurable reminders about food needing attention so that I can act before it is forgotten.

- Given push notifications are enabled and permission is granted, when an item meets my configured alert timing, then I receive a notification containing the item and its date type/date.
- Given permission is denied or notifications are disabled, when an item qualifies, then it remains visible in the in-app attention view.
- Given I change notification timing or disable a category, when the preference is saved, then subsequent alerts follow the new settings.

### US-08: Review Food and Money Impact

As a user, I want to see food outcomes and money saved over time so that I can understand the impact of my actions.

- Given I recorded outcomes, when I select a reporting period, then the dashboard shows separate used, donated, and discarded totals for that period.
- Given cost data exists, when monetary savings are calculated, then the dashboard identifies the data basis, currency, and time period.
- Given the displayed money total includes estimates, when I view it, then it is labeled as an estimate and its method is available.
- Given there is insufficient data, when I view savings, then the app explains that no reliable total is available rather than showing zero as a measured saving.

### US-09: Use the App Across Devices

As a user, I want my information available on web and mobile so that I can update it at home or while shopping.

- Given I sign in on another supported client, when synchronization completes, then my latest inventory, list, and preferences are available.
- Given a client is temporarily offline, when I view previously synchronized data, then the app communicates its offline state and avoids falsely claiming unsaved changes are synchronized.
- Given conflicting edits occur on separate clients, when synchronization resumes, then the app preserves user data and communicates or resolves the conflict predictably.

## Non-Functional Requirements

- **NFR-01 Usability:** Core tasks (add an item, record an outcome, add a grocery item) shall be achievable on small mobile screens and with keyboard navigation on web. Forms shall identify required fields and provide actionable validation messages.
- **NFR-02 Accessibility:** Web and mobile interfaces shall target WCAG 2.2 AA where applicable, including screen-reader labels, visible focus, sufficient contrast, scalable text, and non-color-only status indicators.
- **NFR-03 Performance:** Under normal network conditions, common inventory and list views shall become usable within 2 seconds at the 95th percentile; user-initiated saves shall acknowledge success or failure within 2 seconds at the 95th percentile, excluding external service processing.
- **NFR-04 Availability and resilience:** The service shall target 99.5% monthly availability for account, inventory, and list functions. Temporary failure of receipt, recipe, AI, or push services shall not prevent access to core inventory data.
- **NFR-05 Data integrity:** Confirmed inventory and outcome changes shall not be silently lost. Synchronization and retries shall avoid duplicate receipt imports or duplicate outcome records.
- **NFR-06 Security:** Data shall be encrypted in transit and at rest. Authentication secrets shall be stored using industry-standard password hashing or a trusted identity provider. Access controls shall prevent one user's data from being read or changed by another.
- **NFR-07 Privacy:** The product shall disclose what receipt, inventory, dietary, and usage data is collected and why. Users shall be able to request account/data deletion. Receipt image retention and third-party data sharing shall be explicit and configurable or documented before launch.
- **NFR-08 Interoperability:** The same account data and core workflows shall be supported on agreed web and mobile platforms. Date, quantity, currency, and unit formatting shall follow user locale settings without changing underlying values.
- **NFR-09 Maintainability:** External receipt, recipe, AI, and notification providers shall be isolated behind replaceable interfaces. Automated tests shall cover inventory calculations, date alert rules, receipt confirmation, and savings calculations.
- **NFR-10 Explainability and safety:** Estimates and AI-generated recipe content shall be identified. The app shall not represent date labels or generated content as a food-safety guarantee or medical/dietary advice.
- **NFR-11 Scalability:** The service shall support growth in users and inventory without material degradation to the performance targets; deployment capacity and load assumptions shall be measured before launch.
- **NFR-12 Compatibility:** Supported browser versions, mobile operating systems, and minimum device capabilities shall be published and agreed before release.

## Out of Scope for Initial Release

- Shared household accounts, multiple member roles, or household-level permissions.
- Automatic retailer account/order integrations or automatic purchasing.
- Guaranteed barcode-based product recognition (not selected for the MVP).
- Automated determination that food is safe to eat.

## Remaining Product Decisions

1. Which web framework, mobile delivery approach, and minimum browser/OS versions are required?
2. Should users authenticate with email/password, a third-party identity provider, or both?
3. What receipt languages, layouts, extraction provider, confidence threshold, and image-retention policy are acceptable?
4. Which recipe catalog and AI provider may be used, and what should the app do when a dietary/allergen constraint cannot be verified?
5. What alert windows and default notification schedule should apply, including quiet hours and time zone handling?
6. How should money saved be defined (for example, purchase cost of food used versus estimated avoided replacement cost), and which currencies are in scope?
7. Which units, languages, and jurisdictions are in scope for the first release?
8. What account deletion, data export, consent, and privacy policy requirements apply in target jurisdictions?
9. What user volume, data-retention period, recovery objectives, and operational support targets should the service meet?

## Elicitation Notes

Initial answers: cross-platform web and mobile; single user; manual entry and receipt scanning; distinguish best-before and use-by dates; allow approximate reminders; combine catalog and AI recipes; in-app and push alerts; track food as used, donated, or discarded. No additional privacy, integration, localization, or accessibility constraints were specified, so the quality requirements above are proposed baselines for confirmation.
