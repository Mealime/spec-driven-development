# Spec Driven Development Guide

## Step-by-Step Process

### Step 1: Setup
Clone the Spec Driven Development repository:
```
https://github.com/Mealime/spec-driven-development
```

### Step 2: Define User Stories
Write initial user stories that capture the core requirements:
- As a budget-conscious shopper, I want to input how many meals I need and my total budget, so that I can receive a plan that fits my financial goals.
- As a user, I want to see a “Plan X meals under $X” wizard, so I can quickly generate a meal plan that meets my budget without manual searching.
- As a user, I want to shuffle meal options within my budget, so I can explore different combinations without exceeding my limit.
- As a user, I want to refine my preferences (e.g., vegetarian, gluten-free, no seafood), so the recommendations are more relevant to my needs.
- As a user, I want to see a real-time “Final Cost” as I add or remove items, so I can stay within budget while building my list.
- As a user, I want to receive alerts when I’m approaching or exceeding my budget, so I can make informed trade-offs.
- As a user, I want to add all selected meals and items to my shopping list or cart with one tap, so I can check out quickly.

### Step 3: Explore Codebase
In a new agent window:
1. Use `Cmd+L` to open the agent
2. Copy/paste the user stories
3. Ask Cursor to explore the codebase to find relevant existing code for focused context
4. Make note of useful folders/files
5. Ask Cursor to explain code if uncertain about functionality

### Step 4: Generate Requirements
Write requirements generation prompt:
- Include `@spec-driven-development` folder as context
- Instruct agent to use it as a template
- **Recommendation**: Use Claude Opus on Max Mode for best results


Use @spec-driven-development/  to develop requirements doc for the following requirements.

Focus on using code context from 
@swagger.json and @mobile/ to inform requirements.

v2 Dynamic Budget Cart Builder user stories:
- As a budget-conscious shopper, I want to input how many meals I need and my total budget, so that I can receive a plan that fits my financial goals.
- As a user, I want to see a “Plan X meals under $X” wizard, so I can quickly generate a meal plan that meets my budget without manual searching.
- As a user, I want to shuffle meal options within my budget, so I can explore different combinations without exceeding my limit.
- As a user, I want to refine my preferences (e.g., vegetarian, gluten-free, no seafood), so the recommendations are more relevant to my needs.
- As a user, I want to see a real-time “Final Cost” as I add or remove items, so I can stay within budget while building my list.
- As a user, I want to receive alerts when I’m approaching or exceeding my budget, so I can make informed trade-offs.
- As a user, I want to add all selected meals and items to my shopping list or cart with one tap, so I can check out quickly.

The user facing interface will be dependent on a new backend optimization engine that uses an optimization algo (greedy bag etc) to intelligently combine recipes and products to maximize value of a users budget by combining recipes to use up whole products and reduce food waste.





### Step 5: Review & Refine generated requirements:


# Requirements Document: v2 Dynamic Budget Cart Builder

## Document Information

- **Feature Name**: v2 Dynamic Budget Cart Builder
- **Version**: 1.0
- **Date**: 2024-01-10
- **Author**: Development Team
- **Stakeholders**: Product Management, Engineering, UX Design, Data Analytics

## Introduction

The v2 Dynamic Budget Cart Builder is an intelligent meal planning feature that helps budget-conscious shoppers create optimized meal plans within their financial constraints. This feature enhances the existing budget functionality by introducing an optimization engine that maximizes value, reduces food waste, and provides a guided wizard experience for meal planning.

### Feature Summary
An AI-powered meal planning wizard that generates optimized shopping lists based on user budget and meal count preferences, intelligently combining recipes to minimize waste and maximize value.

### Business Value
- **User Retention**: Provides unique value proposition for budget-conscious shoppers
- **Cart Size Increase**: Encourages bulk purchasing through intelligent recipe combinations
- **Reduced Food Waste**: Optimizes ingredient usage across multiple recipes
- **Competitive Advantage**: Differentiates from simple recipe aggregation tools

### Scope
**Included:**
- Budget-based meal plan generation wizard
- Backend optimization engine for recipe/product combinations
- Real-time budget tracking and alerts
- Dietary preference filtering
- One-tap cart addition
- Meal plan shuffling within budget

**Excluded:**
- Nutritional optimization (future phase)
- Meal scheduling/calendar integration (future phase)
- Social sharing features (future phase)

## Requirements

### Requirement 1: Budget and Meal Input Wizard

**User Story:** As a budget-conscious shopper, I want to input how many meals I need and my total budget, so that I can receive a plan that fits my financial goals.

#### Acceptance Criteria

1. WHEN user navigates to meal planning section THEN system SHALL display "Plan X meals under $X" wizard entry point
2. WHEN user taps wizard entry THEN system SHALL present input form with meal count selector (1-21 meals) and budget input field
3. IF user enters budget less than $10 THEN system SHALL display minimum budget warning message
4. WHEN user enters valid inputs and taps continue THEN system SHALL store budget configuration and proceed to preference selection
5. IF user has previously set budget (from existing `IBudget` interface) THEN system SHALL pre-populate budget field with stored value
6. WHEN input form is displayed THEN system SHALL show estimated cost per meal based on entered values

#### Additional Details
- **Priority**: High
- **Complexity**: Medium
- **Dependencies**: Extends existing `IBudget` interface with meal count tracking
- **Assumptions**: Minimum viable budget is $10 for practical meal planning

### Requirement 2: Dietary Preference Refinement

**User Story:** As a user, I want to refine my preferences (e.g., vegetarian, gluten-free, no seafood), so the recommendations are more relevant to my needs.

#### Acceptance Criteria

1. WHEN budget input is complete THEN system SHALL display dietary preference selection screen
2. IF user has saved dietary preferences in profile THEN system SHALL pre-select those options
3. WHEN preference screen loads THEN system SHALL display toggles for: Vegetarian, Vegan, Gluten-Free, Dairy-Free, No Seafood, No Nuts
4. WHERE user selects conflicting preferences (e.g., Vegan + includes dairy recipes) THEN system SHALL display compatibility warning
5. WHEN user completes preference selection THEN system SHALL pass constraints to optimization engine
6. IF user changes preferences after generation THEN system SHALL offer to regenerate plan with new constraints

#### Additional Details
- **Priority**: High
- **Complexity**: Medium
- **Dependencies**: User profile dietary preferences, recipe categorization system
- **Assumptions**: Recipe data includes accurate dietary tags

### Requirement 3: Optimization Engine Integration

**User Story:** As a user, I want the system to intelligently combine recipes to maximize my budget value by using whole products and reducing waste.

#### Acceptance Criteria

1. WHEN meal plan generation is triggered THEN optimization engine SHALL execute greedy knapsack algorithm considering:
   - Recipe prices from `IClientVariant.price` and `basePrice`
   - Product unit sizes from `ShopProduct` data
   - Ingredient overlap between recipes
   - Waste minimization score

2. IF multiple recipes share ingredients THEN engine SHALL prioritize combinations that use full product units
3. WHEN calculating optimization THEN engine SHALL factor in:
   - Price per serving
   - Ingredient utilization rate (% of purchased product used)
   - Recipe variety score
   - Dietary constraint compliance

4. WHERE ingredient overlap exists THEN engine SHALL calculate true incremental cost of adding recipes
5. IF optimal solution exceeds budget by <5% THEN engine SHALL provide option to view slightly over-budget plan
6. WHEN optimization completes THEN engine SHALL return ranked recipe combinations with waste metrics

#### Additional Details
- **Priority**: High
- **Complexity**: High
- **Dependencies**: Recipe ingredient data, product size data, pricing API
- **Assumptions**: Product size and unit data is available for >80% of ingredients

### Requirement 4: Real-time Budget Tracking Display

**User Story:** As a user, I want to see a real-time "Final Cost" as I add or remove items, so I can stay within budget while building my list.

#### Acceptance Criteria

1. WHEN meal plan is displayed THEN system SHALL show total cost calculation using `ShopPriceResponse` data
2. IF user modifies recipe list THEN system SHALL update total cost within 500ms
3. WHERE budget exists THEN system SHALL display progress bar showing (current total / budget limit)
4. WHEN cost calculation occurs THEN system SHALL include:
   - Recipe subtotals from selected variants
   - Shared ingredient deduplication
   - Applied offers/coupons if available

5. IF real-time price fetch fails THEN system SHALL display cached prices with staleness indicator
6. WHILE user modifies plan THEN system SHALL maintain running total in header/footer

#### Additional Details
- **Priority**: High
- **Complexity**: Medium
- **Dependencies**: Price calculation service, real-time data updates
- **Assumptions**: Price data is available for selected store location

### Requirement 5: Budget Threshold Alerts

**User Story:** As a user, I want to receive alerts when I'm approaching or exceeding my budget, so I can make informed trade-offs.

#### Acceptance Criteria

1. WHEN total cost reaches 90% of budget THEN system SHALL display amber warning banner "Approaching budget limit"
2. IF total cost exceeds 100% of budget THEN system SHALL display red alert banner with overage amount
3. WHEN user attempts to add item that exceeds budget THEN system SHALL show modal with options:
   - Remove other items (with suggestions)
   - Increase budget
   - Proceed over budget

4. WHERE budget is exceeded THEN system SHALL highlight highest-cost recipes for potential removal
5. IF user is over budget THEN "Add to Cart" button SHALL show warning state with overage amount

#### Additional Details
- **Priority**: High
- **Complexity**: Low
- **Dependencies**: Budget tracking state, UI notification system
- **Assumptions**: Users want proactive budget management assistance

### Requirement 6: Meal Plan Shuffle Feature

**User Story:** As a user, I want to shuffle meal options within my budget, so I can explore different combinations without exceeding my limit.

#### Acceptance Criteria

1. WHEN meal plan is displayed THEN system SHALL show "Shuffle" button/icon
2. WHEN user taps shuffle THEN system SHALL:
   - Request new recipe set from optimization engine
   - Maintain same budget and meal count constraints
   - Exclude previously shown recipes from top results
   - Animate transition to new recipe set

3. IF shuffle is triggered >5 times THEN system SHALL expand recipe pool to include previously shown options
4. WHERE dietary preferences are set THEN shuffle SHALL maintain those constraints
5. WHEN shuffle completes THEN system SHALL track analytics event with shuffle count

#### Additional Details
- **Priority**: Medium
- **Complexity**: Medium
- **Dependencies**: Optimization engine multiple solution support
- **Assumptions**: Engine can generate multiple valid solutions for same constraints

### Requirement 7: One-Tap Cart Addition

**User Story:** As a user, I want to add all selected meals and items to my shopping list or cart with one tap, so I can check out quickly.

#### Acceptance Criteria

1. WHEN meal plan is finalized THEN system SHALL display prominent "Add All to Cart" button
2. WHEN user taps add all THEN system SHALL:
   - Batch all recipe items using existing `ShopRecipesResponse` structure
   - Apply ingredient deduplication
   - Calculate final quantities
   - Track analytics via `trackCartAddAction`

3. IF cart addition includes >20 unique items THEN system SHALL show progress indicator
4. WHERE items are unavailable THEN system SHALL add available items and show summary of skipped items
5. WHEN addition completes THEN system SHALL navigate to cart with success message
6. IF addition fails THEN system SHALL maintain meal plan state for retry

#### Additional Details
- **Priority**: High
- **Complexity**: Medium
- **Dependencies**: Batch cart API, shopping service integration
- **Assumptions**: Cart API supports batch operations efficiently

## Non-Functional Requirements

### Performance Requirements
- WHEN optimization engine runs THEN system SHALL return initial results within 3 seconds for up to 21 meals
- IF user modifies plan THEN price recalculation SHALL complete within 500ms
- WHEN shuffle is triggered THEN new results SHALL display within 2 seconds

### Scalability Requirements
- WHEN peak usage occurs THEN system SHALL support 10,000 concurrent optimization requests
- IF cache miss occurs THEN system SHALL gracefully degrade to basic recipe suggestions

### Usability Requirements
- WHEN displaying prices THEN system SHALL format consistently with existing app patterns
- IF mobile keyboard appears THEN budget input SHALL remain visible
- WHERE error occurs THEN system SHALL provide actionable recovery options

### Reliability Requirements
- WHEN network connection is lost THEN system SHALL maintain current plan state
- IF optimization engine fails THEN system SHALL fallback to pre-computed popular combinations
- WHERE price data is stale (>1 hour) THEN system SHALL display freshness indicator

## Constraints and Assumptions

### Technical Constraints
- Must integrate with existing recipe/variant data structure (`IClientVariant`)
- Must use established shopping service APIs (`ShopRecipesResponse`)
- Must maintain compatibility with current budget storage (`IBudget`)
- Analytics must use existing `trackCartAddAction` patterns

### Business Constraints
- Initial launch limited to stores with >90% product data coverage
- Optimization must complete within API gateway timeout limits (30s)
- Must not increase infrastructure costs by >15%

### Assumptions
- Recipe ingredient data is >95% complete and accurate
- Product size/unit data available for >80% of frequently purchased items
- Users understand concept of "meal" as main dish serving 
- Existing price calculation services can handle batch requests efficiently

## Success Criteria

### Definition of Done
- [ ] All acceptance criteria are met and tested
- [ ] Optimization engine achieves <10% food waste on average
- [ ] Feature handles 1-21 meals with $10-500 budgets
- [ ] Analytics tracking implemented for all user interactions
- [ ] Performance benchmarks met under load testing

### Acceptance Metrics
- Generate valid meal plans for 95% of budget/meal combinations
- Average optimization time <3 seconds
- Food waste reduction of 25% vs. random recipe selection
- User satisfaction score >4.2/5 in testing
- Cart addition success rate >98%

## Glossary

| Term | Definition |
|------|------------|
| Meal Plan | Collection of recipes that together form a shopping list |
| Optimization Engine | Backend service using algorithms to combine recipes efficiently |
| Food Waste Score | Percentage of purchased ingredients that would be unused |
| Budget Threshold | User-defined maximum spending limit for meal plan |
| Recipe Variant | Specific serving-size version of a recipe with associated pricing |
| Greedy Knapsack | Algorithm type for optimizing value within constraints |
| Ingredient Overlap | When multiple recipes share common ingredients |
| Shuffle | Generate alternative meal plan with same constraints |

---

## Next Steps

After requirements approval:
1. Create detailed design document with API specifications
2. Define optimization algorithm implementation details
3. Design UI/UX mockups for wizard flow
4. Plan phased rollout strategy
5. Establish success metrics and A/B test framework
