# Loyalty Points System - Owner's Guide

This document provides a detailed explanation of how the Loyalty Points System works, focusing on how an Owner can add or subtract loyalty points for users, the various types of points (codes), and the logic behind them. This is not an API documentation, but rather a functional guide on the points system itself.

## Types of Loyalty Codes

Owners can issue different types of loyalty codes that dictate how users can earn points. Each code type has specific behaviors regarding how points are added, modified, or restricted.

### 1. ONE_FIXED
- **Behavior**: This code type allows users to earn a fixed number of loyalty points once.
- **Example**: If an owner issues a code with a value of 100 points, users can claim this exactly one time.
- **Owner Usage**: The owner can issue these codes for promotions where they want users to claim a one-time reward.

### 2. FIXED
- **Behavior**: Users earn a fixed number of loyalty points every time the code is used. The user can claim this code multiple times.
- **Example**: A code with 50 points can be claimed multiple times, adding 50 points to the user's total each time.
- **Owner Usage**: Ideal for loyalty programs where users receive the same reward multiple times, such as weekly rewards.

### 3. ONE_VARIABLE
- **Behavior**: This code type allows users to claim a variable amount of points once. The number of points depends on the value entered by the owner when adding points.
- **Example**: If a user makes a purchase of $100 and the code gives 1 point per dollar, they can claim 100 points but only once.
- **Owner Usage**: Use for one-time promotions where the reward is based on variable criteria, such as the purchase amount.

### 4. VARIABLE
- **Behavior**: Users earn variable loyalty points based on a specified rate, and they can claim it multiple times.
- **Example**: If the code gives 1 point for every $10 spent, a purchase of $100 gives the user 10 points. This code can be used repeatedly.
- **Owner Usage**: Ideal for ongoing loyalty programs where the points vary based on the user's activity, such as spending or participation.

### 5. ADMIN_ADD
- **Behavior**: This is an administrative action that allows the owner to add any custom number of points to a user's total. It can be used any number of times and doesn't require a code.
- **Example**: If an owner wants to reward a loyal user with 500 bonus points, they can use this operation.
- **Owner Usage**: Use for special cases, such as granting bonus points, rewards, or manually correcting user balances.

### 6. ADMIN_SUBTRACT
- **Behavior**: This is an administrative action that allows the owner to subtract a custom number of points from a user's total. It can be used any number of times and doesn't require a code.
- **Example**: If a user needs points deducted due to a refund or incorrect allocation, the owner can subtract 200 points from the user's balance.
- **Owner Usage**: Use for cases where points need to be adjusted downwards, such as error corrections or refunds.

## How Points are Added or Subtracted

### General Flow for Adding Points

**Fixed/Variable Codes**: When an owner issues a loyalty code (either ONE_FIXED, FIXED, ONE_VARIABLE, or VARIABLE), the system:

1. Checks if the user has already claimed the code (in the case of one-time codes like ONE_FIXED or ONE_VARIABLE).
2. Adds points based on the code type:
   - ONE_FIXED and FIXED add fixed points.
   - ONE_VARIABLE and VARIABLE add variable points based on the input value.
3. Updates the user's total loyalty points and stores the usage of the code to prevent re-use (for one-time codes).

**Admin Actions (Adding/Subtracting Points)**:

- **ADMIN_ADD**: The owner directly adds the specified number of points to the user's total. This action is unrestricted, meaning it can be repeated any number of times, and doesn't check for prior usage of any codes.
- **ADMIN_SUBTRACT**: The owner directly subtracts points from the user's total, again without any restriction or limit on the number of times this can be done.

### Detailed Example of Point Addition:

**Scenario**:
- An owner issues a FIXED loyalty code with 100 points.
- The user applies the code multiple times by engaging in eligible activities.

**What Happens**:
- Each time the code is applied, the system adds 100 points to the user's total.
- After multiple uses, the user's total points grow based on how many times they used the code.

## Admin-Specific Operations

As an owner, you have special administrative actions that allow you to directly control the loyalty points for any user:

### ADMIN_ADD
- This operation allows you to add points directly to the user's total, bypassing the normal code-based checks.
- No restrictions on how many times you can add points.
- Points can be added for any reason, such as special promotions, bonuses, or manual adjustments.

### ADMIN_SUBTRACT
- This operation allows you to subtract points from a user's total.
- Like ADMIN_ADD, it bypasses the normal loyalty code process and can be repeated multiple times.
- Useful for scenarios like correcting errors, removing points due to refunds, or adjusting balances for any other reason.

## Points Calculation

Whenever points are added or subtracted (either through loyalty codes or admin actions), the system calculates the total points for each user. The total points are stored and updated automatically after every transaction.

- **Adding Points**: Total points increase based on the value of the code or the ADMIN_ADD input.
- **Subtracting Points**: Total points decrease based on the value of the ADMIN_SUBTRACT input.

**Important**: The total points calculation does not interfere with previously used codes or points added through other types of codes. Each point addition or subtraction is independent, ensuring accurate tracking of a user's overall loyalty balance.

## Key Points for Owners

- ONE_FIXED and ONE_VARIABLE codes can only be used once by each user. Once claimed, the code cannot be reused.
- FIXED and VARIABLE codes can be used multiple times, adding more points to the user's total with each use.
- ADMIN_ADD and ADMIN_SUBTRACT allow owners to directly add or subtract points from a user's total, without any limitations or code reuse checks.
- The system automatically calculates and updates the total loyalty points for each user based on the actions taken.