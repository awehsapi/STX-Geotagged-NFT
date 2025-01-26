# Stacks Geotagged NFT Rewards Smart Contract

## Overview
The Geotagged NFT Rewards Smart Contract enables users to earn reward points by completing location-based activities. These points can be redeemed for unique non-fungible tokens (NFTs). The contract ensures robust data validation and error handling, making it secure and reliable for use in blockchain applications.

---

## Features

### Key Functionalities
- **Location Management**: Admins can add, enable, or disable geotagged locations with associated activities and rewards.
- **Activity Completion**: Users can complete activities tied to specific locations and earn reward points based on proximity and location status.
- **NFT Minting**: Users can redeem points to mint unique NFTs if they meet the required threshold.
- **Points Transfer**: Users can transfer earned points to other participants.

### Robust Validation
- Coordinates are validated to ensure they are within realistic bounds (latitude and longitude).
- Error handling prevents invalid transactions, duplicate activity completions, and unauthorized actions.
- Limits are imposed on location data, points, and NFT IDs for added security.

---

## Data Structures

### Non-Fungible Token
- **Token Name**: `geotagged-nft`
- **ID Type**: `uint`

### Constants
- **`contract-owner`**: The principal who deploys the contract.
- **`min-distance`**: Minimum allowed distance for activity completion.
- **`points-threshold`**: Required points to mint an NFT.
- **`max-lat` & `max-long`**: Maximum latitude and longitude values for location validation.
- **`max-locations`**: Maximum number of locations the contract can support.
- **`max-points-per-activity`**: Maximum reward points for a single activity.

### Errors
- **Owner-only operations**: Restricts certain functions to the contract owner (e.g., `err-owner-only`).
- **Invalid data or actions**: Handles issues like invalid coordinates, insufficient points, and unauthorized transfers.

### Maps
1. **`locations`**: Stores location details (name, coordinates, activity, and reward points).
2. **`user-completions`**: Tracks completed activities per user.
3. **`user-points`**: Maintains a user's reward points.
4. **`location-count`**: Counts the total number of locations.
5. **`minted-nfts`**: Tracks minted NFT IDs.
6. **`location-status`**: Manages the active/inactive status of locations.

---

## Core Functions

### 1. **Admin Functions**
#### `add-location`
Adds a new geotagged location.
- Parameters: `id`, `name`, `lat`, `long`, `activity`, `points`
- Validates input and ensures the location is unique.

#### `set-location-status`
Enables or disables a location.
- Parameters: `location-id`, `active`

---

### 2. **User Functions**
#### `complete-activity`
Marks an activity as completed for a specific location.
- Parameters: `location-id`, `user-lat`, `user-long`
- Validates user coordinates, checks location status, and calculates proximity.
- Awards reward points if conditions are met.

#### `mint-nft`
Mints an NFT for users who have accumulated enough points.
- Parameters: `token-id`
- Deducts points and prevents duplicate minting for the same token ID.

#### `transfer-points`
Transfers points between users.
- Parameters: `recipient`, `amount`
- Validates recipient and ensures sufficient sender balance.

---

### 3. **Read-Only Functions**
#### `get-location`
Retrieves details of a specific location.
- Parameters: `id`

#### `get-user-points`
Returns the points balance for a user.
- Parameters: `user`

#### `get-completion-status`
Checks if a user has completed an activity at a location.
- Parameters: `user`, `location-id`

#### `is-nft-minted`
Determines if an NFT has already been minted.
- Parameters: `token-id`

#### `get-location-status`
Returns the active/inactive status of a location.
- Parameters: `location-id`

#### `get-user-stats`
Provides a summary of a user’s points balance and NFT mint eligibility.
- Parameters: `user`

---

## Error Codes
| Code | Description |
|------|-------------|
| `u100` | Owner-only access violation |
| `u101` | Activity already completed |
| `u102` | Invalid location ID |
| `u103` | Insufficient points for action |
| `u104` | Invalid coordinates |
| `u105` | Location limit exceeded |
| `u106` | Invalid points value |
| `u107` | Invalid token ID |
| `u108` | Empty location name |
| `u109` | Empty activity description |
| `u110` | NFT already minted |
| `u111` | Zero transfer amount |
| `u112` | Self-transfer not allowed |
| `u113` | Invalid user principal |
| `u114` | Location not found |
| `u115` | Zero token ID |
| `u116` | Maximum token ID exceeded |
| `u117` | Location is disabled |

---

## Usage Examples

### Adding a New Location (Admin Only)
```clojure
(add-location u1 "Park" u12345678 u87654321 "Jogging" u50)
```

### Completing an Activity
```clojure
(complete-activity u1 u12345670 u87654310)
```

### Minting an NFT
```clojure
(mint-nft u1)
```

### Transferring Points
```clojure
(transfer-points 'SP2RECIPIENT u100)
```

---

## Security Considerations
- All critical functions are guarded with extensive validation and error handling.
- Admin-only operations are restricted to the contract owner.
- User-specific actions require proper authentication.

---

## Future Improvements
- Dynamic point scaling based on activity difficulty or user engagement.
- Integration with external APIs for real-world geotag validation.
- Enhanced NFT customization with metadata based on user activity history.

---

## Conclusion
The Geotagged NFT Rewards Smart Contract is designed to incentivize real-world engagement through blockchain technology. Its robust structure ensures fairness, security, and scalability, making it suitable for applications in gaming, fitness, and location-based services.

