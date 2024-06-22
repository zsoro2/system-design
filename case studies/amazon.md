# Amazon

- 350.000.000 (350Million) products -> lets say its 1 billion
- 10 million orders per day -> 100 orders per second
- 1MB / product

Total:

1 billion x 1MB = 1 PB


## Products Database

- We need to partition, because its too big 1PB
- Single Leader replication is fine

## Cart and WishList

For managing the Cart and WishList features, we have two services: Cart Service and WishList Service. Both use MySQL and provide similar APIs to fetch, update, and delete items. MySQL is chosen for its ACID properties, ensuring atomicity and consistency.

```sql
CREATE TABLE Users (
    UserID INT PRIMARY KEY,
    UserName VARCHAR(255) NOT NULL
);

CREATE TABLE CartItems (
    CartItemID INT PRIMARY KEY,
    UserID INT,
    ProductID INT,
    Quantity INT,
    ItemName VARCHAR(255) NOT NULL,
    CONSTRAINT fk_user FOREIGN KEY (UserID) REFERENCES Users(UserID)
);
```
**Importance of Atomicity**

To maintain data integrity, operations like inserting into CartItems are performed within transactions:

```sql
START TRANSACTION;
INSERT INTO CartItems (UserID, ProductID, Quantity, ItemName) VALUES (1, 101, 1, 'Product A');
COMMIT;
```

If the insert fails, the transaction ensures the database remains consistent by rolling back the changes.

**Separate Tables for Cart and WishList**

Cart and WishList tables are kept separate to handle different scaling needs, especially during high-traffic events like Black Friday or Diwali sales. This allows for independent scaling of each service, meeting functional requirements more efficiently.


## Services

- Seller Onboarding Service
- Product Onboarding Service
- Notification Service API
- Search Service API
- Image Processing Service


## Resources

[!ref target="blank" text="High-Level System Design for Amazon"](https://medium.com/@vaibhavkansagara/high-level-system-design-for-amazon-1aa18f3efd15)
[!ref target="blank" text="Youtube - Instagram + Twitter + Facebook + Reddit"](https://www.youtube.com/watch?v=S2y9_XYOZsg)


