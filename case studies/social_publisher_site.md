# Social sites


## Calculations

- Daily active user: 200 million
- Each user post avarage: 5 times a day
- Post data / day: 200M x 5 = 1.000.000.000 (1Billion) 
- 100 charaters / post = 100 bytes
- 100 charaters / metadata = 100 bytes

Total:
Daily storage: 1B x 200 = 200GB
Yearly storage: 1B * 200 * 365days/year = 73000 TB  = 73PB

- Request / Sec: 1B / (24 hrs * 3600 seconds) = 12K Request / sec


## Timeline read

### Fanout on Write
**Description**: Pre-compute the news feed during write time.

**Pros**:
- Real-time feed generation, instantly pushing new posts to friends' caches.
- Fast feed fetching due to pre-computation.

**Cons**:
- Slow and resource-intensive for users with many friends.
- Wastes resources on inactive users.

### Fanout on Read
**Description**: Generate the news feed during read time.

**Pros**:
- Efficient for inactive users, saving computing resources.
- Avoids the hotkey problem.

**Cons**:
- Slower feed fetching since it's computed on-demand.

### Hybrid Approach
**Push Model**:
- Used for most users.
- Pre-compute and cache the news feed during write time.

**Pull Model**:
- Used for users with many followers (e.g., celebrities).
- Fetch and merge recent posts on-demand during read time.

**Consistent Hashing**:
- Distributes requests and data evenly to mitigate the hotkey problem.

## Services

- User Service API
- Feed Service API
- Notification Service API
- Search Service API
- Messaging Service API


## Resources

[!ref target="blank" text="Twitter system design"](https://github.com/karanpratapsingh/system-design?tab=readme-ov-file#twitter)
[!ref target="blank" text="Facebook system design"](https://www.geeksforgeeks.org/design-facebook-system-design/)
[!ref target="blank" text="Youtube - Instagram + Twitter + Facebook + Reddit"](https://www.youtube.com/watch?v=S2y9_XYOZsg)
